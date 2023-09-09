# Dictionary
키,값 쌍으로 구성
``` python
x = {'a':10, 'b':20, 'c':30, 'd':40}
y = {1: 'one', 2:'two'}
```

### Dictionary Comprehension
- {키: 값 for 키, 값 in 딕셔너리}
- dict( { 키: 값 for 키, 값 in 딕셔너리 } )
``` python
keys = ['a', 'b', 'c', 'd']
x = {key:value for key, value in dict.fromkeys(keys).items()}  # {'a':None, 'b':None, 'c':None, 'd':None}
```
- 키-값 자리 바꾸기
``` python
{value:key for key, value in {'a':10, 'b':20, 'c':30}.items()}  # {10:'a', 20:'b', 30:'c'}
```
- {키:값 for 키, 값 in 딕셔너리 if 조건식}
``` python
x = {key:value for key, value in x.items() if value != 20}  # x = {'a':10, 'c':30}
```

### Dictionary 병합
``` python
x = {'a':1, 'b':2}
y = {'c':3, 'd':4}
```
- 딕셔너리.update()
``` python
x.update(y)  # x = {'a':1, 'b':2, 'c':3, 'd':4}
```
- {**dict, **dict}  딕셔너리 언패킹
``` python
{**x, **y} # {'a':1, 'b':2, 'c':3, 'd':4}
```

### key-value 쌍 추가
- setdefault(키, 기본값) : 키-값 쌍 추가 (키의 값 수정은 X)
- update(키=값) : 키의 값 수정, 키가 없으면 키-값 쌍 추가
=== "setdefault"
    ``` python
    x.setdefault('f')  # x = {'a':10, 'b':20, 'c':30, 'd':40, 'f':None}
    x.setdefault('f', 100)  # x = {'a':10, 'b':20, 'c':30, 'd':40, 'f':100}
    ```
=== "update"
    ``` python
    # key가 문자일 때,
    x.update(e=90)  # x = {'a':10, 'b':20, 'c':30, 'd':40, 'e'=90}
    x.update(c=20, e=90)  # x = {'a':10, 'b':20, 'c':20, 'd':40, 'e'=90}

    # key가 숫자일 때,
    y.update({1: 'ONE', 3:'THREE'})  # y = {1:'ONE', 2:'two', 3:'THREE'}
    ```
- update(리스트) / update(튜플) 
``` python
y.update( [[2, 'TWO'], [4, 'FOUR']] )  # y = {1:'one', 2:'TWO', 4:'FOUR'}
y.update( zip([1,2], ['ONE','two']) )  # y = {1:'ONE', 2:'two'}
```

### key-value 쌍 삭제
- pop()  : 특정 키-값 쌍을 삭제한 뒤 삭제한 값 반환, 해당 키가 없을 때는 기본값을 반환
- popitem()  : 마지막(python 3.6) 키-값 쌍을 삭제한 뒤 삭제한 키-값 쌍을 튜플로 반환
- clear()  : 딕셔너리의 모든 키-값 쌍 삭제
- del
=== "pop"
    ``` python
    x = {'a':10, 'b':20, 'c':30, 'd':40}
    x.pop('a')  # 10, x = {'b':20, 'c':30, 'd':40}
    x.pop('z', 0)  # 0 (기본값 반환)
    ```
=== "popitem"
    ``` python
    x.popitem()  # ('d':40) , x = {'a':10, 'b':20, 'c':30}
    ```
=== "clear"
    ``` python
    x.clear()  # x = {}
    ```
=== "del"
    ``` python
    del x['key']
    ```

### key-value 가져오기
- get()  : 특정 키의 값을 가져옴, 해당 키가 없을 때는 기본값 반환
``` python
x.get('a')  # 10
x.get('z', 0)  # 0 (기본값 반환)
```
- items()  : 키-값 쌍을 모두 가져옴 
- keys()  : 키를 모두 가져옴
- values()  : 값을 모두 가져옴
``` python
x.items()  # dict_items([ ('a',10), ('b',20), ('c',30), ('d',40) ])
x.keys()  # dict_keys(['a', 'b', 'c', 'd'])
x.values()  # dict_values([10, 20, 30, 40])
```

### 리스트와 튜플로 딕셔너리 생성
- dict.fromkeys(키 리스트)  : 키 리스트로 딕셔너리를 생성, 값은 모두 None (값 지정 가능)
``` python
keys = ['a', 'b', 'c', 'd']

x = dict.fromkeys(keys)  # x = {'a':None, 'b':None, 'c':None, 'd':None}
x = dict.fromkeys(keys,100)  # x = {'a':100, 'b':100, 'c':100, 'd':100}
```

### 할당과 복사
- **할당** : `x=y`
- **복사** : `y = x.copy()`
``` python
x = {'a':10, 'b':20}
y = x  # x is y -> True
y = x.copy()  # x is y -> False
```
- 중첩 딕셔너리 (**할당**: `x.copy()`, **복사**: `deepcopy`) <br>
``` python
x = {'a':{'python': 3.7}, 'b':{'python':3.6}} # 딕셔너리 = {키1: {키A: 값A}, 키2: {키B: 값B}}
y = x.copy()  # x is y -> True
import copy  
y = copy.deepcopy(x)  # x is y -> False
```

---

### key-value 출력
``` python
x = {'a':10, 'b':20, 'c':30}
```
=== "key-value 출력"
    ``` python
    for key, value in x.items():  # a 10 \n b 20 \n c 30
        print(key, value)      
    ```
=== "key 출력"
    ``` python
    for i in x:
        print(i, end = ' ')  # a b c
    ```
=== "key 출력"
    ``` python
    for key in x.keys():
        print(key, end=' ')  # a b c 
    ```
=== "value 출력"
    ``` python
    for value in x.values():
        print(value, end = ' ')  # 10 20 30 
    ```
