# 예외 처리 Try-Exception
⭐️[Exception hierarchy](https://docs.python.org/3/library/exceptions.html#exception-hierarchy)⭐️

AttributeError, NameError, TypeError 등 다양한 예외가 발생했을 때, 스크립트 실행을 중단하지 않고 계속 실행하게 해주는 방법
```python
try: 
	x = int(input('나눌 숫자를 입력하세요: '))
	y = 10/x
	print(y)
except: 
	print('예외가 발생했습니다.') # 예외가 발생했을 때 실행
```

### 특정 예외만 처리하기
```python
y = [10,20,30]
try:
	index, x = map(int, input('인덱스와 나눌 숫자를 입력하세요: ').split())
	print(y[index] / x)
except ZeroDivisionError:  # 숫자를 0으로 나눠서 에러가 발생했을 때 실행
	print('숫자를 0으로 나눌 수 없습니다.')
except IndexError:  # 범위를 벗어난 인덱스에 접근하여 에러가 발생했을 때 실행
	print('잘못된 인덱스입니다.')
```

### 예외의 에러 메시지 받아오기
```python
y = [10, 20, 30]

try:
	index, x = map(int, input('인덱스와 나눌 숫자를 입력하세요: ').split())
	print(y[index]/x)
except ZeroDivisionError as e:  # as 뒤에 변수를 지정하면, 에러를 받아옴
	print('숫자를 0으로 나눌 수 없습니다.', e)  # e에 저장된 에러 메시지 출력
except IndexError as e
	print('잘못된 인덱스입니다', e)  
except Exception as e: # 위 두 에러를 제외한 모든 예외의 에러메시지 출력
	print('예외가 발생했습니다', e)
```

### try + else
```python
try:
	x = int(input('나눌 숫자를 입력하세요: '))
	y = 10/x
except ZeroDivisionError:
	print('숫자를 0으로 나눌 수 없습니다')
else:  # try의 코드에서 예외가 발생하지 않았을 때 실행
	print(y)
```

### finally : 예외와는 상관없이 항상 코드 실행하기
- try안에서 만든 변수는 try 바깥에서 사용 가능 <br>
(try는 함수가 아니므로 스택 프레임을 생성하지 않기 때문에 try 바깥에서 사용 가능함)
```python
try:
	x = int(input("나눌 숫자를 입력하세요: "))
	y = 10/x
except ZeroDivisionError:
	print("숫자를 0으로 나눌 수 없습니다.")
else:
	print(y)
finally:  # 예외 발생 여부와 상관없이 항상 실행
	print("코드 실행이 끝났습니다")
```

### 예외 발생시키기
- raise 예외(’에러메시지’)
```python
try:
	x = int(input('3의 배수를 입력하세요: '))
	if x % 3 != 0:
		raise Exception('3의 배수가 아닙니다')
	print(x)
except Exception as e:
	print('예외가 발생했습니다', e)  # e = Exception에 넣은 에러 메시지 # 예외가 발생했습니다. 3의 배수가 아닙니다.
```
-  three_multiple()안에서 예외가 발생하더라도, 현재 코드 블록에서 처리해줄 except가 없다면 except가 나올 때까지 계속 상위 코드 블록으로 올라감
``` python
def three_multiple():
    x = int(input('3의 배수를 입력하세요: '))
    if x % 3 != 0:                              
        raise Exception('3의 배수가 아닙니다.')  # 현재 함수 안에는 except가 없으므로 예외를 상위 코드 블록으로 넘김
    print(x)                
try:
    three_multiple()
except Exception as e:  # 하위 코드 블록에서 예외가 발생해도 실행됨
    print('예외가 발생했습니다.', e)  # 예외가 발생했습니다. 3의 배수가 아닙니다.
```

### try-except 에서 처리한 예외를 다시 발생시키기 
- raise
```python
def three_multiple():
	try:
		x = int(input('3의 배수를 입력하세요: '))
		if x % 3 != 0:
			raise Exception('3의 배수가 아닙니다.') 
		print(x)

	except Exception as e:
		print("three_multiple 함수에서 예외가 발생했습니다", e)
		raise  # raise로 현재 예외를 다시 발생시켜서 상위 코드 블록으로 넘김

try:
	three_multiple()
except Exception as e:
	print('스크립트 파일에서 예외가 발생했습니다', e) 
# three_multiple 함수에서 예외가 발생했습니다. 3의 배수가 아닙니다.
# 스크립트 파일에서 예외가 발생했습니다. 3의 배수가 아닙니다.
```
- raise 예외(’에러메시지’) : raise에 다른 예외를 지정하고, 에러 메시지를 넣을 수 있음
```python
...
except Exception as e:
    print("three_multiple 함수에서 예외가 발생했습니다", e)
    raise RuntimeError('three_multiple 함수에서 예외가 발생했습니다.')
```

### assert로 예외 발생시키기
- assert 조건식 
- assert 조건식, 에러메시지 
: 지정된 조건식이 거짓일 때 AssertionError 발생, 참이면 그냥 넘어감
: 디버깅 모드에서만 실행됨 (파이썬은 기본적으로 디버깅 모드)
```python
x = int(input('3의 배수를 입력하세요: '))
assert x % 3 == 0, '3의 배수가 아닙니다.' # 3의 배수가 아니면 예외 발생, 맞으면 pass
print(x)
```

### 예외 생성
=== "Shape"
    ```python
    class 예외이름(Exception):
        def __init__(self):
            super().__init__('에러메시지')
    ```
=== "Example1"
    ```python
    class NotThreeMultipleError(Exception):
        def __init__(self):
            super().__init__('3의 배수가 아닙니다.')

    def three_multiple():
        try:
            x = int(input('3의 배수를 입력하세요: '))
            if x % 3 != 0:
                raise NotThreeMultipleError  ## NotThreeMultipleError 발생
            print(x)

        except Exception as e:
            print('예외가 발생했습니다', e)

    three_multiple() # 예외가 발생했습니다 3의 배수가 아닙니다.
    ```
=== "Example2"
    ```python
    class NotThreeMultipleError(Exception):
        pass

    def three_multiple():
        try:
            x = int(input('3의 배수를 입력하세요: '))
            if x % 3 != 0:
                raise NotThreeMultipleError('3의 배수가 아닙니다')  ## NotThreeMultipleError 발생
            print(x)

        except Exception as e:
            print('예외가 발생했습니다', e)

    three_multiple() # 예외가 발생했습니다 3의 배수가 아닙니다.
    ```