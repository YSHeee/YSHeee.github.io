# FastAPI Best Practice

### 🔨🔨🔨🔨🔨수정중...🔨🔨🔨🔨🔨

## 1. Project Structure. Consistent & predictable
일관성 있고 예측 가능한 프로젝트 구조
```
fastapi-project
├── alembic/
├── src
│   ├── auth
│   │   ├── router.py
│   │   ├── schemas.py  # pydantic models
│   │   ├── models.py  # db models
│   │   ├── dependencies.py
│   │   ├── config.py  # local configs
│   │   ├── constants.py
│   │   ├── exceptions.py
│   │   ├── service.py
│   │   └── utils.py
│   ├── aws
│   │   ├── client.py  # client model for external service communication
│   │   ├── schemas.py
│   │   ├── config.py
│   │   ├── constants.py
│   │   ├── exceptions.py
│   │   └── utils.py
│   └── posts
│   │   ├── router.py
│   │   ├── schemas.py
│   │   ├── models.py
│   │   ├── dependencies.py
│   │   ├── constants.py
│   │   ├── exceptions.py
│   │   ├── service.py
│   │   └── utils.py
│   ├── config.py  # global configs
│   ├── models.py  # global models
│   ├── exceptions.py  # global exceptions
│   ├── pagination.py  # global module e.g. pagination
│   ├── database.py  # db connection related stuff
│   └── main.py
├── tests/
│   ├── auth
│   ├── aws
│   └── posts
├── templates/
│   └── index.html
├── requirements
│   ├── base.txt
│   ├── dev.txt
│   └── prod.txt
├── .env
├── .gitignore
├── logging.ini
└── alembic.ini
```

1. `src` Folder : 모든 도메인 디렉터리 저장
    - `src/` : highest level of an app, contains common models, configs, and constants, etc.
    - `src/main.py` : root of the project, which inits the FastAPI app

2. 각각의 package는 router, schema, model 등으로 구성
    - `router.py` : Is a core of each module with all the endpoints
    - `schemas.py` : For pydantic models
    - `models.py` : For DB models
    - `service.py` : Module specific business logic
    - `dependencies.py` : Router dependencies
    - `constants.py` : Module specific constants and error codes
    - `config.py` : e.g. Env vars
    - `utils.py` : Non-business logic functions (response normalization, data enrichment, ...)
    - `exceptions` : Module specific exceptions (PostNotFound, InvalidUserData, ...)

3. 패키지에 "다른 패키지 service/dependency/constant"가 필요한 경우라면, Import them with an explicit module name
``` python title="Example"
from src.auth import constants as auth_constants
from src.notifications import service as notification_service
# 각 패키지의 constants module에 Standard ErrorCode가 있는 경우
from src.posts.constants import ErrorCode as PostsErrorCode
```

## 2. Excessively use Pydantic for data validation

Pydantic은 데이터를 검증하고 변환할 수 있는 풍부한 기능을 지원한다

- Regular features like required & non-required fields with default values
- Comprehensive data processing tools like regex
- Enums for limited allowed options
- Length validation
- Email validation
- etc ...
``` python title="Example"
from enum import Enum
from pydantic import AnyUrl, BaseModel, EmailStr, Field, constr

class MusicBand(str, Enum):
   AEROSMITH = "AEROSMITH"
   QUEEN = "QUEEN"
   ACDC = "AC/DC"

class UserBase(BaseModel):
    first_name: str = Field(min_length=1, max_length=128)
    username: constr(regex="^[A-Za-z0-9-_]+$", to_lower=True, strip_whitespace=True)
    email: EmailStr
    age: int = Field(ge=18, default=None)  # must be greater or equal to 18
    favorite_band: MusicBand = None  # only "AEROSMITH", "QUEEN", "AC/DC" values are allowed to be inputted
    website: AnyUrl = None
```

## 3. Use dependencies for data validation vs DB
Pydantic은 **Client input**만 검증할 수 있다

따라서, 전자 메일이 이미 존재하거나 사용자를 찾을 수 없는 등등..<br>
데이터베이스 제약조건에 대한 데이터 유효성 검증은 Dependency를 사용한다
```python title="Example"
# dependencies.py
async def valid_post_id(post_id: UUID4) -> Mapping:
    post = await service.get_by_id(post_id)
    if not post:
        raise PostNotFound()

    return post


# router.py
@router.get("/posts/{post_id}", response_model=PostResponse)
async def get_post_by_id(post: Mapping = Depends(valid_post_id)):
    return post


@router.put("/posts/{post_id}", response_model=PostResponse)
async def update_post(
    update_data: PostUpdate,
    post: Mapping = Depends(valid_post_id),
):
    updated_post: Mapping = await service.update(id=post["id"], data=update_data)
    return updated_post


@router.get("/posts/{post_id}/reviews", response_model=list[ReviewsResponse])
async def get_post_reviews(post: Mapping = Depends(valid_post_id)):
    post_reviews: list[Mapping] = await reviews_service.get_by_post_id(post["id"])
    return post_reviews
```

## 4. Chain dependencies
Dependency는 다른 dependency를 사용할 수 있고, 유사 logic에 대한 코드 반복을 피할 수 있다
```python title="Example"
# dependencies.py
from fastapi.security import OAuth2PasswordBearer
from jose import JWTError, jwt

async def valid_post_id(post_id: UUID4) -> Mapping:
    post = await service.get_by_id(post_id)
    if not post:
        raise PostNotFound()

    return post


async def parse_jwt_data(
    token: str = Depends(OAuth2PasswordBearer(tokenUrl="/auth/token"))
) -> dict:
    try:
        payload = jwt.decode(token, "JWT_SECRET", algorithms=["HS256"])
    except JWTError:
        raise InvalidCredentials()

    return {"user_id": payload["id"]}


async def valid_owned_post(
    post: Mapping = Depends(valid_post_id),
    token_data: dict = Depends(parse_jwt_data),
) -> Mapping:
    if post["creator_id"] != token_data["user_id"]:
        raise UserNotOwner()

    return post

# router.py
@router.get("/users/{user_id}/posts/{post_id}", response_model=PostResponse)
async def get_user_post(post: Mapping = Depends(valid_owned_post)):
    return post
```

## 5. Decouple & Reuse dependencies. Dependency calls are cached
Dependency는 여러 번 재사용할 수 있지만, 재검토되지는 않는다<br>
FastAPI는 request 범위 내에서 dependency 결과를 cache화 하는 것이 default 설정이기 때문이다

만약, Service-`get_post_by_id`를 호출하는 dependency의 경우, 해당 dependency를 호출할 때마다 DB를 검색하지 않는다 <br>
첫번째 호출시에만 DB를 검색한다

이를 알면, Multiple smaller function에 대한 dependency를 쉽게 분리할 수 있다

- `valid_owned_post`
- `valid_active_creator`
- `get_user_post`
but `parse_jwt_data` is called only once, in the very first call

```python title="Example"
# dependencies.py
from fastapi import BackgroundTasks
from fastapi.security import OAuth2PasswordBearer
from jose import JWTError, jwt

async def valid_post_id(post_id: UUID4) -> Mapping:
    post = await service.get_by_id(post_id)
    if not post:
        raise PostNotFound()

    return post


async def parse_jwt_data(
    token: str = Depends(OAuth2PasswordBearer(tokenUrl="/auth/token"))
) -> dict:
    try:
        payload = jwt.decode(token, "JWT_SECRET", algorithms=["HS256"])
    except JWTError:
        raise InvalidCredentials()

    return {"user_id": payload["id"]}


async def valid_owned_post(
    post: Mapping = Depends(valid_post_id),
    token_data: dict = Depends(parse_jwt_data),
) -> Mapping:
    if post["creator_id"] != token_data["user_id"]:
        raise UserNotOwner()

    return post


async def valid_active_creator(
    token_data: dict = Depends(parse_jwt_data),
):
    user = await users_service.get_by_id(token_data["user_id"])
    if not user["is_active"]:
        raise UserIsBanned()

    if not user["is_creator"]:
       raise UserNotCreator()

    return user


# router.py
@router.get("/users/{user_id}/posts/{post_id}", response_model=PostResponse)
async def get_user_post(
    worker: BackgroundTasks,
    post: Mapping = Depends(valid_owned_post),
    user: Mapping = Depends(valid_active_creator),
):
    """Get post that belong the active user."""
    worker.add_task(notifications_service.send_email, user["id"])
    return post
```

## 6. Follow the REST
Restful API는 다음과 같은 경로에서 dependency를 쉽게 재사용할 수 있다

- `GET /courses/:course_id`
- `GET /courses/:course_id/chapters/:chapter_id/lessons`
- `GET /chapters/:chapter_id`

단, 경로에 동일한 변수 이름을 사용해야 한다

```python title="Example"
# src.profiles.dependencies
async def valid_profile_id(profile_id: UUID4) -> Mapping:
    profile = await service.get_by_id(post_id)
    if not profile:
        raise ProfileNotFound()

    return profile

# src.creators.dependencies
async def valid_creator_id(profile: Mapping = Depends(valid_profile_id)) -> Mapping:
    if not profile["is_creator"]:
       raise ProfileNotCreator()

    return profile

# src.profiles.router.py
@router.get("/profiles/{profile_id}", response_model=ProfileResponse)
async def get_user_profile_by_id(profile: Mapping = Depends(valid_profile_id)):
    """Get profile by id."""
    return profile

# src.creators.router.py
@router.get("/creators/{profile_id}", response_model=ProfileResponse)
async def get_user_profile_by_id(
     creator_profile: Mapping = Depends(valid_creator_id)
):
    """Get creator's profile by id."""
    return creator_profile
```

Use `/me` endpoints for users resources (`GET /profiles/me`,`GET /users/me/posts`)

- 사용자 ID의 존재 여부를 검증할 필요 없음 - 인증방법을 통해 이미 확인
- 사용자ID가 요청자의 것인지 확인할 필요 없음


## 7. Don't make your routes async, if you have only blocking I/O operations
Under the hood, FastAPI는 async&sync I/O 작업을 모두 효과적으로 처리할 수 있다.

- FastAPI runs `sync` routes in the threadpool and blocking I/O operations won't stop the event loop from executing the tasks.
- Otherwise, if the route is defined `async` then it's called regularly via `await` and FastAPI trusts you to do only non-blocking I/O operations.

The caveat is if you fail that trust and execute blocking operations within async routes, the event loop will not be able to run the next tasks until that blocking operation is done.

```python title="Example"
import asyncio
import time

@router.get("/terrible-ping")
async def terrible_catastrophic_ping():
    time.sleep(10) # I/O blocking operation for 10 seconds
    pong = service.get_pong()  # I/O blocking operation to get pong from DB

    return {"pong": pong}

@router.get("/good-ping")
def good_ping():
    time.sleep(10) # I/O blocking operation for 10 seconds, but in another thread
    pong = service.get_pong()  # I/O blocking operation to get pong from DB, but in another thread

    return {"pong": pong}

@router.get("/perfect-ping")
async def perfect_ping():
    await asyncio.sleep(10) # non-blocking I/O operation
    pong = await service.async_get_pong()  # non-blocking I/O db call

    return {"pong": pong}
```

**What happens when we call:**

1. `GET /terrible-ping`
    * FastAPI 서버가 request를 수신하고, 처리를 시작한다
    * 서버의 event loop와 queue의 모든 작업이 `time.sleep()`이 끝날때까지 대기한다
        + 서버는 `time.sleep()`이 I/O 작업이 아니라 생각하므로, 완료될 때까지 기다린다
        + 서버는 대기하는 동안 새로운 request를 수락하지 않는다
    * event loop와 queue의 모든 작업이 `service.get_pong()`이 완료될 때까지 대기한다
        + 서버는 `service.get_pong()`이 I/O 작업이 아니라 생각하므로, 완료될 때까지 기다린다
        + 서버는 대기하는 동안 새로운 request를 수락하지 않는다
    * Server returns the response
        + After a response, server starts accepting new requests
2. `GET /good-ping`
    * FastAPI server receives a request and starts handling it
    * FastAPI sends the whole route `good_ping` to the threadpool, where a worker thread will run the function
    * `good_ping`이 실행되는 동안 event loop는 queue에서 다음 작업을 선택하고 작업한다 (ex: 새 요청 수락, db 호출 등)
        + Main thread와 관계없이 worker thread는 `time.sleep`가 완료될 때까지 기다리고, `service.get_pong`을 완료한다
        + Sync operation blocks only the side thread, not the main one
    * When `good_ping` finishes its work, server returns a response to the client
3. `GET /perfect-ping`
    * FastAPI server receives a request and starts handling it
    * FastAPI awaits `asyncio.sleep(10)`
    * Event loop selects next tasks from the queue and works on them (e.g. accept new request, call db)
    * When `asyncio.sleep(10)` is done, servers goes to the next lines and awaits `service.async_get_pong`
    * Event loop selects next tasks from the queue and works on them (e.g. accept new request, call db)
    * When `service.async_get_pong` is done, server returns a response to the client

:warning: Non-blocking awaitables|thread pool로 전송되는 작업은 I/O intensive task이어야 한다 (open file, db call, external api call ...)

- CPU-intensive task(heavy calculations, data processing, video transcoding)를 기다리는 것은 가치가 없다. CPU가 작업을 완료하기 위해 작동하기 때문이다. 반면 I/O 작업은 외부 작업이므로 서버는 해당 작업이 완료될 때까지 아무것도 하지 않아도 되므로 다음 작업으로 넘어갈 수 있다
- GIL로 인해 한 번에 하나의 thread만 작동할 수 있다
- CPU intensive task를 최적화하기 위해서는, multi-process로 가야한다

## 8. Custom base model from day 0
제어 가능한 global base model을 사용하면 app내의 모든 model을 커스터마이징할 수 있다.<br>
예시로 표준 datetime 형식을 갖거나, base model 의 모든 하위클래스에 대해 super method를 추가할 수 있다.
```python title="Example"
from datetime import datetime
from zoneinfo import ZoneInfo

import orjson
from fastapi.encoders import jsonable_encoder
from pydantic import BaseModel, root_validator


def orjson_dumps(v, *, default):
    # orjson.dumps returns bytes, to match standard json.dumps we need to decode
    return orjson.dumps(v, default=default).decode()


def convert_datetime_to_gmt(dt: datetime) -> str:
    if not dt.tzinfo:
        dt = dt.replace(tzinfo=ZoneInfo("UTC"))

    return dt.strftime("%Y-%m-%dT%H:%M:%S%z")


class ORJSONModel(BaseModel):
    class Config:
        json_loads = orjson.loads
        json_dumps = orjson_dumps
        json_encoders = {datetime: convert_datetime_to_gmt}  # method for customer JSON encoding of datetime fields

    @root_validator()
    def set_null_microseconds(cls, data: dict) -> dict:
       """Drops microseconds in all the datetime field values."""
        datetime_fields = {
            k: v.replace(microsecond=0)
            for k, v in data.items()
            if isinstance(k, datetime)
        }

        return {**data, **datetime_fields}

    def serializable_dict(self, **kwargs):
       """Return a dict which contains only serializable fields."""
        default_dict = super().dict(**kwargs)

        return jsonable_encoder(default_dict)
```

In the example above we have decided to make a global base model which:

- Uses orjson to serialize data
- Drops microseconds to 0 in all date formats
- Serializes all datetime fields to standard format with explicit timezone

## 9. Docs
API가 공개되지 않은 경우에는 Docs 또한 공개하지 않는다.
```python title="Example"
from fastapi import FastAPI
from starlette.config import Config

config = Config(".env")  # parse .env file for env variables

ENVIRONMENT = config("ENVIRONMENT")  # get current env name
SHOW_DOCS_ENVIRONMENT = ("local", "staging")  # explicit list of allowed envs

app_configs = {"title": "My Cool API"}
if ENVIRONMENT not in SHOW_DOCS_ENVIRONMENT:
   app_configs["openapi_url"] = None  # set url for docs as null

app = FastAPI(**app_configs)
```

Help FastAPI to generate an easy-to-understand docs

- Set `response_model`, `status_code`, `description`, ...
- If models and statuses vary, use `responses` route attribute to add docs for different responses

```python title="Example"
from fastapi import APIRouter, status

router = APIRouter()

@router.post(
    "/endpoints",
    response_model=DefaultResponseModel,  # default response pydantic model
    status_code=status.HTTP_201_CREATED,  # default status code
    description="Description of the well documented endpoint",
    tags=["Endpoint Category"],
    summary="Summary of the Endpoint",
    responses={
        status.HTTP_200_OK: {
            "model": OkResponse, # custom pydantic model for 200 response
            "description": "Ok Response",
        },
        status.HTTP_201_CREATED: {
            "model": CreatedResponse,  # custom pydantic model for 201 response
            "description": "Creates something from user request ",
        },
        status.HTTP_202_ACCEPTED: {
            "model": AcceptedResponse,  # custom pydantic model for 202 response
            "description": "Accepts request and handles it later",
        },
    },
)
async def documented_route():
    pass
```

## 10. Use Pydantic's BaseSettings for configs
Pydantic은 환경 변수를 분석하고, validators로 처리할 수 있는 도구를 제공한다.
```python title="Example"
from pydantic import AnyUrl, BaseSettings, PostgresDsn

class AppSettings(BaseSettings):
    class Config:
        env_file = ".env"
        env_file_encoding = "utf-8"
        env_prefix = "app_"

    DATABASE_URL: PostgresDsn
    IS_GOOD_ENV: bool = True
    ALLOWED_CORS_ORIGINS: set[AnyUrl]
```

## 11. SQLAlchemy: Set DB keys naming convention
데이터베이스 규칙에 따라 인덱스 이름을 설정하는 것이 SQLalchemy보다 더 좋다
```python title="Example"
from sqlalchemy import MetaData

POSTGRES_INDEXES_NAMING_CONVENTION = {
    "ix": "%(column_0_label)s_idx",
    "uq": "%(table_name)s_%(column_0_name)s_key",
    "ck": "%(table_name)s_%(constraint_name)s_check",
    "fk": "%(table_name)s_%(column_0_name)s_fkey",
    "pk": "%(table_name)s_pkey",
}
metadata = MetaData(naming_convention=POSTGRES_INDEXES_NAMING_CONVENTION)
```


## 12. Migrations. Alembic.
- Migration은 static하고 revertable하여야 한다
    * 만약 migration이 동적으로 생성된 데이터에 의존하는 경우, 동적인 것이 구조가 아니라 데이터 자체인지 확인
- descriptive names&slugs를 사용하여 migration을 생성한다. Slug가 필요하며 변경 사항을 설명해야 한다
- 새로운 migration에 대해 사용자가 읽을 수 있는 파일 템플릿을 설정한다
    * `*date*_*slug*.py` `(2022-08-24_post_content_idx.py)`

```python title="alembic.ini"
file_template = %%(year)d-%%(month).2d-%%(day).2d_%%(slug)s
```

## 13. Set DB naming convention
1. lower_case_snake
2. singular form (`post`, `post_like`, `user_playlist`)
3. group similar tables with module prefix (`payment_account`, `payment_bill`, `post`, `post_like`)
4. stay consistent across tables, but concrete namings are ok
    - use `profile_id` in all tables, but if some of them need only profiles that are creators, use `creator_id`
    - use `post_id` for all abstract tables like `post_like`, `post_view`, but use concrete naming in relevant modules like `course_id`in `chapters.course_id`
5. `_at` suffix for datetime
6. `_date` suffix for date

## 14. Set tests client async from day 0
DB와의 integration tests를 작성하면, 향후 event loop error가 발생할 가능성이 높다. 따라서 async test client를 즉시 설정해야한다
([async-asgi-testclient](https://github.com/vinissimus/async-asgi-testclient) OR [httpx](https://github.com/encode/starlette/issues/652))
```python title="Example"
import pytest
from async_asgi_testclient import TestClient

from src.main import app  # inited FastAPI app


@pytest.fixture
async def client():
    host, port = "127.0.0.1", "5555"
    scope = {"client": (host, port)}

    async with TestClient(
        app, scope=scope, headers={"X-User-Fingerprint": "Test"}
    ) as client:
        yield client


@pytest.mark.asyncio
async def test_create_post(client: TestClient):
    resp = await client.post("/posts")

    assert resp.status_code == 201
```

## 15. BackgroundTasks > asyncio.create_task
BackgroundTasks can effectively run both blocking and non-blocking I/O operations the same way FastAPI handles blocking routes
(`sync` tasks are run in a threadpool, while `async` tasks are awaited later)

- Don't lie to the worker and don't mark blocking I/O operations as `async`
- Don't use it for heavy CPU intensive tasks

```python title="Example"
from fastapi import APIRouter, BackgroundTasks
from pydantic import UUID4

from src.notifications import service as notifications_service


router = APIRouter()


@router.post("/users/{user_id}/email")
async def send_user_email(worker: BackgroundTasks, user_id: UUID4):
    """Send email to user"""
    worker.add_task(notifications_service.send_email, user_id)  # send email after responding client
    return {"status": "ok"}
```

## 16. Typing is important

## 17. Save files in chunks
Don't hope your clients will send small files

```python title="Example"
import aiofiles
from fastapi import UploadFile

DEFAULT_CHUNK_SIZE = 1024 * 1024 * 50  # 50 megabytes

async def save_video(video_file: UploadFile):
   async with aiofiles.open("/file/path/name.mp4", "wb") as f:
     while chunk := await video_file.read(DEFAULT_CHUNK_SIZE):
         await f.write(chunk)
```

## 18. Be careful with dynamic pydantic fields
If you have a pydantic field that can accept a union of types, be sure the validator explicitly knows the difference between those types
```python title="Example"
from pydantic import BaseModel


class Article(BaseModel):
   text: str | None
   extra: str | None


class Video(BaseModel):
   video_id: int
   text: str | None
   extra: str | None


class Post(BaseModel):
   content: Article | Video


post = Post(content={"video_id": 1, "text": "text"})
print(type(post.content))
# OUTPUT: Article
# Article is very inclusive and all fields are optional, allowing any dict to become validSolutions:
```
**Solutions:**

1. Input이 허용된 유효한 필드만 허용했는지 확인하고, 알수없는 필드가 제공된 경우 오류를 발생시킨다
```python title="Example"
from pydantic import BaseModel, Extra

class Article(BaseModel):
   text: str | None
   extra: str | None

   class Config:
        extra = Extra.forbid


class Video(BaseModel):
   video_id: int
   text: str | None
   extra: str | None

   class Config:
        extra = Extra.forbid


class Post(BaseModel):
   content: Article | Video
```

2. Use Pydantic's Smart Union (>v1.9) if fields are simple<br>
It's a good solution if the fields are simple like `int` or `bool`, but it doesn't work for complex fields like classes
```python title="Without Smart Union"
from pydantic import BaseModel

class Post(BaseModel):
   field_1: bool | int
   field_2: int | str
   content: Article | Video

p = Post(field_1=1, field_2="1", content={"video_id": 1})
print(p.field_1)
# OUTPUT: True
print(type(p.field_2))
# OUTPUT: int
print(type(p.content))
# OUTPUT: Article
```
```python title="With Smart Union"
class Post(BaseModel):
   field_1: bool | int
   field_2: int | str
   content: Article | Video

   class Config:
      smart_union = True


p = Post(field_1=1, field_2="1", content={"video_id": 1})
print(p.field_1)
# OUTPUT: 1
print(type(p.field_2))
# OUTPUT: str
print(type(p.content))
# OUTPUT: Article, because smart_union doesn't work for complex fields like classes
```

3. Fast Workaround
Order field types properly: from the most strict ones to loose ones
```python title="Example"
class Post(BaseModel):
   content: Video | Article
```

## 19. SQL-first, Pydantic-second
- 일반적으로 데이터베이스는 CPython 보다 훨씬 빠르고 개끗하게 데이터를 처리한다
- 복잡한 join과 간단한 데이터 조작 모두 SQL을 사용하여 수행하는 것이 좋다
- 중첩된 개체가 있는 응답에 대해 DB에서 json을 집계하는 것이 좋다

``` python title="Example"
# src.posts.service
from typing import Mapping

from pydantic import UUID4
from sqlalchemy import desc, func, select, text
from sqlalchemy.sql.functions import coalesce

from src.database import databse, posts, profiles, post_review, products

async def get_posts(
    creator_id: UUID4, *, limit: int = 10, offset: int = 0
) -> list[Mapping]:
    select_query = (
        select(
            (
                posts.c.id,
                posts.c.type,
                posts.c.slug,
                posts.c.title,
                func.json_build_object(
                   text("'id', profiles.id"),
                   text("'first_name', profiles.first_name"),
                   text("'last_name', profiles.last_name"),
                   text("'username', profiles.username"),
                ).label("creator"),
            )
        )
        .select_from(posts.join(profiles, posts.c.owner_id == profiles.c.id))
        .where(posts.c.owner_id == creator_id)
        .limit(limit)
        .offset(offset)
        .group_by(
            posts.c.id,
            posts.c.type,
            posts.c.slug,
            posts.c.title,
            profiles.c.id,
            profiles.c.first_name,
            profiles.c.last_name,
            profiles.c.username,
            profiles.c.avatar,
        )
        .order_by(
            desc(coalesce(posts.c.updated_at, posts.c.published_at, posts.c.created_at))
        )
    )

    return await database.fetch_all(select_query)

# src.posts.schemas
import orjson
from enum import Enum

from pydantic import BaseModel, UUID4, validator


class PostType(str, Enum):
    ARTICLE = "ARTICLE"
    COURSE = "COURSE"


class Creator(BaseModel):
    id: UUID4
    first_name: str
    last_name: str
    username: str


class Post(BaseModel):
    id: UUID4
    type: PostType
    slug: str
    title: str
    creator: Creator

    @validator("creator", pre=True)  # before default validation
    def parse_json(cls, creator: str | dict | Creator) -> dict | Creator:
       if isinstance(creator, str):  # i.e. json
          return orjson.loads(creator)

       return creator

# src.posts.router
from fastapi import APIRouter, Depends

router = APIRouter()


@router.get("/creators/{creator_id}/posts", response_model=list[Post])
async def get_creator_posts(creator: Mapping = Depends(valid_creator_id)):
   posts = await service.get_posts(creator["id"])

   return posts
```

If an aggregated data form DB is a simple JSON, then take a look at Pydantic's Jsonfield type, which will load raw JSON first.
```python title="Example"
from pydantic import BaseModel, Json

class A(BaseModel):
    numbers: Json[list[int]]
    dicts: Json[dict[str, int]]

valid_a = A(numbers="[1, 2, 3]", dicts='{"key": 1000}')  # becomes A(numbers=[1,2,3], dicts={"key": 1000})
invalid_a = A(numbers='["a", "b", "c"]', dicts='{"key": "str instead of int"}')  # raises ValueError
```

## 20. Validate hosts, if users can send publicly available URLs
예를 들어 다음과 같은 특정 endpoint가 있다:

- 사용자로부터 미디어 파일 수신
- 해당 파일에 대해 고유한 url 생성
- 사용자에게 url 반환
- `PUT /profiles/me` `POST/posts` 같은 다른 endpoint에서 사용
- 이러한 endpoint는 whitelisted host의 파일만 허용
- 이 이름과 일치하는 url을 사용하여 파일을 AWS에 업로드
- url 호스트를 whitelist에 추가하지 않으면, 잘못된 사용자가 위험한 링크를 업로드할 수 있음

```python title="Example"
from pydantic import AnyUrl, BaseModel

ALLOWED_MEDIA_URLS = {"mysite.com", "mysite.org"}

class CompanyMediaUrl(AnyUrl):
    @classmethod
    def validate_host(cls, parts: dict) -> tuple[str, str, str, bool]:
       """Extend pydantic's AnyUrl validation to whitelist URL hosts."""
        host, tld, host_type, rebuild = super().validate_host(parts)
        if host not in ALLOWED_MEDIA_URLS:
            raise ValueError(
                "Forbidden host url. Upload files only to internal services."
            )

        return host, tld, host_type, rebuild


class Profile(BaseModel):
    avatar_url: CompanyMediaUrl  # only whitelisted urls for avatar
```

## 21. Raise a ValueError in custom pydantic validators, if schema directly faces the client
It wil return a nice detailed response to users
```python title="Example"
# src.profiles.schemas
from pydantic import BaseModel, validator

class ProfileCreate(BaseModel):
    username: str

    @validator("username")
    def validate_bad_words(cls, username: str):
        if username  == "me":
            raise ValueError("bad username, choose another")

        return username


# src.profiles.routes
from fastapi import APIRouter

router = APIRouter()


@router.post("/profiles")
async def get_creator_posts(profile_data: ProfileCreate):
   pass
```

## 22. Don't forget FastAPI converts Response Pydantic Object to Dict then to an instance of ResponseModel then to Dict then to JSON
``` python title="Example"
from fastapi import FastAPI
from pydantic import BaseModel, root_validator

app = FastAPI()


class ProfileResponse(BaseModel):
    @root_validator
    def debug_usage(cls, data: dict):
        print("created pydantic model")

        return data

    def dict(self, *args, **kwargs):
        print("called dict")
        return super().dict(*args, **kwargs)


@app.get("/", response_model=ProfileResponse)
async def root():
    return ProfileResponse()
```

## 23. If you must use sync SDK, then run it in a thread pool.
- If you must use a library to interact with external services, and it's not `async`, then make the HTTP calls in an external worker thread <br>
- For a simple example, we could use our well-known `run_in_threadpool` from starlette

```python title="Example"
from fastapi import FastAPI
from fastapi.concurrency import run_in_threadpool
from my_sync_library import SyncAPIClient

app = FastAPI()


@app.get("/")
async def call_my_sync_library():
    my_data = await service.get_my_data()

    client = SyncAPIClient()
    await run_in_threadpool(client.make_request, data=my_data)
```

## 24. Use linters (black, isort, autoflake)
- With linters, you can forget about formatting the code and focus on writing the business logic
- Black is the uncompromising code formatter that eliminates so many small decisions you have to make during development. Other linters help you write cleaner code and follow the PEP8
- It's a popular good practice to use pre-commit hooks, but just using the script was ok for us

```bash
#!/bin/sh -e
set -x

autoflake --remove-all-unused-imports --recursive --remove-unused-variables --in-place src tests --exclude=__init__.py
isort src tests --profile black
black src tests
```


---
!!!quote
    - Best-Practice Github [zhanymkanov](https://github.com/zhanymkanov/fastapi-best-practices#1-project-structure-consistent--predictable)
    - Pydantic [Pydantic-Docs](https://docs.pydantic.dev)