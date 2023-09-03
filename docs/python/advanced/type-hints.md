# 타입 힌트 Type Hinting

파이썬 코드 작성 시 타입에 대한 메타 정보를 제공하는 것

- 실질적인 제약 사항을 강요하지 않음 (타입 어노테이션이 부정확하다고 해서 오류가 발생하지는 않음)
- 코드를 이해하는 데에 있어서 수월하게 해주고, 개발 도구가 활용할 수 있게끔 도와주는 역할
- 원활한 개발 및 유지보수를 위해 사용<br>동적(dynamic) 프로그래밍 언어인 파이썬에서는 인터프리터가 코드를 실행하면서 타입을 추론하여 체크하는데, 변수의 타입이 고정되어 있지 않아 개발자가 원하면 자유롭게 바꿀 수 있음으로써 생기는 문제 예방

### 변수 타입 어노테이션
``` python
age: int = 25
name: str = "ysh"
```

### 함수 타입 어노테이션
``` python
def get_items(item_a: str, item_b: int, item_c: float, item_d: bool, item_e: bytes) -> str:
    return item_a
```

### 클래스 타입 어노테이션
``` python
class Person:
    def __init__(self, name: str):
        self.name = name

def get_person_name(one_person: Person):
    return one_person.name
```

### typing 모듈
``` python
from typing import List, Set, Dict, Tuple

nums: List[int] = [1]

unique_nums: Set[int] = {6, 7}

vision: Dict[str, float] = {'left': 1.0, 'right': 0.9}

john: Tuple[int, str, List[float]] = (25, "John Doe", [1.0, 0.9])

```

### 타입 어노테이션 검사
- `__annotations__`
``` python
__annotations__ # {'age': int, 'name': str}
```

### a variable can be any of several types
- |
- Union
=== "Python 3.10+"
    ```python
    def process_item(item: int | str): # int이거나 str이거나
        print(item)
    ```
=== "Python 3.6+"
    ```python
    from typing import Union

    def process_item(item: Union[int, str]): 
        print(item) 
    ```

### It could be None
- |
- Union
- Optional
=== "Python 3.10+"
    ```python
    def say_hi(name: str | None = None): # str이거나 None이거나
        if name is not None:
            print(f"Hey {name}!")
        else:
            print("Hello World")
    ```
=== "Python 3.6+, Union"
    ```python
    from typing import Union
    def say_hi(name: Union[str, None] = None):
        if name is not None:
            print(f"Hey {name}!")
        else:
            print("Hello World")
    ```
=== "Python 3.6+, Optional"
    ```python
    from typing import Optional
    def say_hi(name: Optional[str] = None):
        if name is not None:
            print(f"Hey {name}!")
        else:
            print("Hello World")
    ```

---

!!! quote
    - [Dalseo POST](https://www.daleseo.com/python-type-annotations/)
    - [FastAPI Docs](https://fastapi.tiangolo.com/ko/python-types/#python-types-intro)