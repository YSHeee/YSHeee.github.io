# Variable

### 변수의 사용 범위
- 전역 변수 Global variable : 함수를 포함하여 스크립트 전체에서 접근할 수 있는 변수
``` python
x = 10 #전역 변수
def foo():
	print(x) # 전역 변수 출력
```
- 지역 변수 Local variable : 자신이 생성된 함수 내에서만 접근 가능한 변수
```python
def foo():
	x = 10  # foo의 지역 변수
	print(x)
```

### 함수 안에서 전역 변수 변경하기
- Global 전역변수
``` python
x = 10
def foo():
	global x # 전역변수 선언
	x = 20
	print(x)

foo() # 20
print(x) # 20
```

### 네임스페이스
- 변수는 네임스페이스(namespace, 이름공간)에 저장되어 locals() 함수를 통해 출력 가능

=== "전역 변수"
``` python
x = 10
locals()
# {'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 
# 'x': 10}
```
=== "지역 변수"
``` python
def foo():
	x = 10
	print(locals())

foo()  # {'x' : 10}
```