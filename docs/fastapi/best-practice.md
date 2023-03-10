# FastAPI Best Practice

### π¨π¨π¨π¨π¨μμ μ€...π¨π¨π¨π¨π¨

## 1. Project Structure. Consistent & predictable
μΌκ΄μ± μκ³  μμΈ‘ κ°λ₯ν νλ‘μ νΈ κ΅¬μ‘°
```
fastapi-project
βββ alembic/
βββ src
β   βββ auth
β   β   βββ router.py
β   β   βββ schemas.py  # pydantic models
β   β   βββ models.py  # db models
β   β   βββ dependencies.py
β   β   βββ config.py  # local configs
β   β   βββ constants.py
β   β   βββ exceptions.py
β   β   βββ service.py
β   β   βββ utils.py
β   βββ aws
β   β   βββ client.py  # client model for external service communication
β   β   βββ schemas.py
β   β   βββ config.py
β   β   βββ constants.py
β   β   βββ exceptions.py
β   β   βββ utils.py
β   βββ posts
β   β   βββ router.py
β   β   βββ schemas.py
β   β   βββ models.py
β   β   βββ dependencies.py
β   β   βββ constants.py
β   β   βββ exceptions.py
β   β   βββ service.py
β   β   βββ utils.py
β   βββ config.py  # global configs
β   βββ models.py  # global models
β   βββ exceptions.py  # global exceptions
β   βββ pagination.py  # global module e.g. pagination
β   βββ database.py  # db connection related stuff
β   βββ main.py
βββ tests/
β   βββ auth
β   βββ aws
β   βββ posts
βββ templates/
β   βββ index.html
βββ requirements
β   βββ base.txt
β   βββ dev.txt
β   βββ prod.txt
βββ .env
βββ .gitignore
βββ logging.ini
βββ alembic.ini
```

1. `src` Folder : λͺ¨λ  λλ©μΈ λλ ν°λ¦¬ μ μ₯
    - `src/` : highest level of an app, contains common models, configs, and constants, etc.
    - `src/main.py` : root of the project, which inits the FastAPI app

2. κ°κ°μ packageλ router, schema, model λ±μΌλ‘ κ΅¬μ±
    - `router.py` : Is a core of each module with all the endpoints
    - `schemas.py` : For pydantic models
    - `models.py` : For DB models
    - `service.py` : Module specific business logic
    - `dependencies.py` : Router dependencies
    - `constants.py` : Module specific constants and error codes
    - `config.py` : e.g. Env vars
    - `utils.py` : Non-business logic functions (response normalization, data enrichment, ...)
    - `exceptions` : Module specific exceptions (PostNotFound, InvalidUserData, ...)

3. ν¨ν€μ§μ "λ€λ₯Έ ν¨ν€μ§ service/dependency/constant"κ° νμν κ²½μ°λΌλ©΄, Import them with an explicit module name
``` python title="Example"
from src.auth import constants as auth_constants
from src.notifications import service as notification_service
# κ° ν¨ν€μ§μ constants moduleμ Standard ErrorCodeκ° μλ κ²½μ°
from src.posts.constants import ErrorCode as PostsErrorCode
```

## 2. Excessively use Pydantic for data validation

Pydanticμ λ°μ΄ν°λ₯Ό κ²μ¦νκ³  λ³νν  μ μλ νλΆν κΈ°λ₯μ μ§μνλ€

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
Pydanticμ **Client input**λ§ κ²μ¦ν  μ μλ€

λ°λΌμ, μ μ λ©μΌμ΄ μ΄λ―Έ μ‘΄μ¬νκ±°λ μ¬μ©μλ₯Ό μ°Ύμ μ μλ λ±λ±..<br>
λ°μ΄ν°λ² μ΄μ€ μ μ½μ‘°κ±΄μ λν λ°μ΄ν° μ ν¨μ± κ²μ¦μ Dependencyλ₯Ό μ¬μ©νλ€
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
Dependencyλ λ€λ₯Έ dependencyλ₯Ό μ¬μ©ν  μ μκ³ , μ μ¬ logicμ λν μ½λ λ°λ³΅μ νΌν  μ μλ€
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
Dependencyλ μ¬λ¬ λ² μ¬μ¬μ©ν  μ μμ§λ§, μ¬κ²ν λμ§λ μλλ€<br>
FastAPIλ request λ²μ λ΄μμ dependency κ²°κ³Όλ₯Ό cacheν νλ κ²μ΄ default μ€μ μ΄κΈ° λλ¬Έμ΄λ€

λ§μ½, Service-`get_post_by_id`λ₯Ό νΈμΆνλ dependencyμ κ²½μ°, ν΄λΉ dependencyλ₯Ό νΈμΆν  λλ§λ€ DBλ₯Ό κ²μνμ§ μλλ€ <br>
μ²«λ²μ§Έ νΈμΆμμλ§ DBλ₯Ό κ²μνλ€

μ΄λ₯Ό μλ©΄, Multiple smaller functionμ λν dependencyλ₯Ό μ½κ² λΆλ¦¬ν  μ μλ€

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
Restful APIλ λ€μκ³Ό κ°μ κ²½λ‘μμ dependencyλ₯Ό μ½κ² μ¬μ¬μ©ν  μ μλ€

- `GET /courses/:course_id`
- `GET /courses/:course_id/chapters/:chapter_id/lessons`
- `GET /chapters/:chapter_id`

λ¨, κ²½λ‘μ λμΌν λ³μ μ΄λ¦μ μ¬μ©ν΄μΌ νλ€

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

- μ¬μ©μ IDμ μ‘΄μ¬ μ¬λΆλ₯Ό κ²μ¦ν  νμ μμ - μΈμ¦λ°©λ²μ ν΅ν΄ μ΄λ―Έ νμΈ
- μ¬μ©μIDκ° μμ²­μμ κ²μΈμ§ νμΈν  νμ μμ


## 7. Don't make your routes async, if you have only blocking I/O operations
Under the hood, FastAPIλ async&sync I/O μμμ λͺ¨λ ν¨κ³Όμ μΌλ‘ μ²λ¦¬ν  μ μλ€.

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
    * FastAPI μλ²κ° requestλ₯Ό μμ νκ³ , μ²λ¦¬λ₯Ό μμνλ€
    * μλ²μ event loopμ queueμ λͺ¨λ  μμμ΄ `time.sleep()`μ΄ λλ λκΉμ§ λκΈ°νλ€
        + μλ²λ `time.sleep()`μ΄ I/O μμμ΄ μλλΌ μκ°νλ―λ‘, μλ£λ  λκΉμ§ κΈ°λ€λ¦°λ€
        + μλ²λ λκΈ°νλ λμ μλ‘μ΄ requestλ₯Ό μλ½νμ§ μλλ€
    * event loopμ queueμ λͺ¨λ  μμμ΄ `service.get_pong()`μ΄ μλ£λ  λκΉμ§ λκΈ°νλ€
        + μλ²λ `service.get_pong()`μ΄ I/O μμμ΄ μλλΌ μκ°νλ―λ‘, μλ£λ  λκΉμ§ κΈ°λ€λ¦°λ€
        + μλ²λ λκΈ°νλ λμ μλ‘μ΄ requestλ₯Ό μλ½νμ§ μλλ€
    * Server returns the response
        + After a response, server starts accepting new requests
2. `GET /good-ping`
    * FastAPI server receives a request and starts handling it
    * FastAPI sends the whole route `good_ping` to the threadpool, where a worker thread will run the function
    * `good_ping`μ΄ μ€νλλ λμ event loopλ queueμμ λ€μ μμμ μ ννκ³  μμνλ€ (ex: μ μμ²­ μλ½, db νΈμΆ λ±)
        + Main threadμ κ΄κ³μμ΄ worker threadλ `time.sleep`κ° μλ£λ  λκΉμ§ κΈ°λ€λ¦¬κ³ , `service.get_pong`μ μλ£νλ€
        + Sync operation blocks only the side thread, not the main one
    * When `good_ping` finishes its work, server returns a response to the client
3. `GET /perfect-ping`
    * FastAPI server receives a request and starts handling it
    * FastAPI awaits `asyncio.sleep(10)`
    * Event loop selects next tasks from the queue and works on them (e.g. accept new request, call db)
    * When `asyncio.sleep(10)` is done, servers goes to the next lines and awaits `service.async_get_pong`
    * Event loop selects next tasks from the queue and works on them (e.g. accept new request, call db)
    * When `service.async_get_pong` is done, server returns a response to the client

:warning: Non-blocking awaitables|thread poolλ‘ μ μ‘λλ μμμ I/O intensive taskμ΄μ΄μΌ νλ€ (open file, db call, external api call ...)

- CPU-intensive task(heavy calculations, data processing, video transcoding)λ₯Ό κΈ°λ€λ¦¬λ κ²μ κ°μΉκ° μλ€. CPUκ° μμμ μλ£νκΈ° μν΄ μλνκΈ° λλ¬Έμ΄λ€. λ°λ©΄ I/O μμμ μΈλΆ μμμ΄λ―λ‘ μλ²λ ν΄λΉ μμμ΄ μλ£λ  λκΉμ§ μλ¬΄κ²λ νμ§ μμλ λλ―λ‘ λ€μ μμμΌλ‘ λμ΄κ° μ μλ€
- GILλ‘ μΈν΄ ν λ²μ νλμ threadλ§ μλν  μ μλ€
- CPU intensive taskλ₯Ό μ΅μ ννκΈ° μν΄μλ, multi-processλ‘ κ°μΌνλ€

## 8. Custom base model from day 0
μ μ΄ κ°λ₯ν global base modelμ μ¬μ©νλ©΄ appλ΄μ λͺ¨λ  modelμ μ»€μ€ν°λ§μ΄μ§ν  μ μλ€.<br>
μμλ‘ νμ€ datetime νμμ κ°κ±°λ, base model μ λͺ¨λ  νμν΄λμ€μ λν΄ super methodλ₯Ό μΆκ°ν  μ μλ€.
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
APIκ° κ³΅κ°λμ§ μμ κ²½μ°μλ Docs λν κ³΅κ°νμ§ μλλ€.
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
Pydanticμ νκ²½ λ³μλ₯Ό λΆμνκ³ , validatorsλ‘ μ²λ¦¬ν  μ μλ λκ΅¬λ₯Ό μ κ³΅νλ€.
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
λ°μ΄ν°λ² μ΄μ€ κ·μΉμ λ°λΌ μΈλ±μ€ μ΄λ¦μ μ€μ νλ κ²μ΄ SQLalchemyλ³΄λ€ λ μ’λ€
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
- Migrationμ staticνκ³  revertableνμ¬μΌ νλ€
    * λ§μ½ migrationμ΄ λμ μΌλ‘ μμ±λ λ°μ΄ν°μ μμ‘΄νλ κ²½μ°, λμ μΈ κ²μ΄ κ΅¬μ‘°κ° μλλΌ λ°μ΄ν° μμ²΄μΈμ§ νμΈ
- descriptive names&slugsλ₯Ό μ¬μ©νμ¬ migrationμ μμ±νλ€. Slugκ° νμνλ©° λ³κ²½ μ¬ν­μ μ€λͺν΄μΌ νλ€
- μλ‘μ΄ migrationμ λν΄ μ¬μ©μκ° μ½μ μ μλ νμΌ ννλ¦Ώμ μ€μ νλ€
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
DBμμ integration testsλ₯Ό μμ±νλ©΄, ν₯ν event loop errorκ° λ°μν  κ°λ₯μ±μ΄ λλ€. λ°λΌμ async test clientλ₯Ό μ¦μ μ€μ ν΄μΌνλ€
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

1. Inputμ΄ νμ©λ μ ν¨ν νλλ§ νμ©νλμ§ νμΈνκ³ , μμμλ νλκ° μ κ³΅λ κ²½μ° μ€λ₯λ₯Ό λ°μμν¨λ€
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
- μΌλ°μ μΌλ‘ λ°μ΄ν°λ² μ΄μ€λ CPython λ³΄λ€ ν¨μ¬ λΉ λ₯΄κ³  κ°λνκ² λ°μ΄ν°λ₯Ό μ²λ¦¬νλ€
- λ³΅μ‘ν joinκ³Ό κ°λ¨ν λ°μ΄ν° μ‘°μ λͺ¨λ SQLμ μ¬μ©νμ¬ μννλ κ²μ΄ μ’λ€
- μ€μ²©λ κ°μ²΄κ° μλ μλ΅μ λν΄ DBμμ jsonμ μ§κ³νλ κ²μ΄ μ’λ€

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

If an aggregated data form DB is a simple JSON, then take a look at Pydantic'sΒ Jsonfield type, which will load raw JSON first.
```python title="Example"
from pydantic import BaseModel, Json

class A(BaseModel):
    numbers: Json[list[int]]
    dicts: Json[dict[str, int]]

valid_a = A(numbers="[1, 2, 3]", dicts='{"key": 1000}')  # becomes A(numbers=[1,2,3], dicts={"key": 1000})
invalid_a = A(numbers='["a", "b", "c"]', dicts='{"key": "str instead of int"}')  # raises ValueError
```

## 20. Validate hosts, if users can send publicly available URLs
μλ₯Ό λ€μ΄ λ€μκ³Ό κ°μ νΉμ  endpointκ° μλ€:

- μ¬μ©μλ‘λΆν° λ―Έλμ΄ νμΌ μμ 
- ν΄λΉ νμΌμ λν΄ κ³ μ ν url μμ±
- μ¬μ©μμκ² url λ°ν
- `PUT /profiles/me` `POST/posts` κ°μ λ€λ₯Έ endpointμμ μ¬μ©
- μ΄λ¬ν endpointλ whitelisted hostμ νμΌλ§ νμ©
- μ΄ μ΄λ¦κ³Ό μΌμΉνλ urlμ μ¬μ©νμ¬ νμΌμ AWSμ μλ‘λ
- url νΈμ€νΈλ₯Ό whitelistμ μΆκ°νμ§ μμΌλ©΄, μλͺ»λ μ¬μ©μκ° μνν λ§ν¬λ₯Ό μλ‘λν  μ μμ

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