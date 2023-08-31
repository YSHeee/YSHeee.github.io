# Function

- 매개변수 : 함수에서 받는 값  def 함수이름(매개변수1, 매개변수2):
- 인수: 함수를 호출할 때 넣는 값  함수이름(인수, 인수)
- return : 함수 바깥으로 값을 반환 (return에 값을 지정하지 않으면, None 반환)
- 순수 함수(pure function) : 함수의 실행이 외부 상태에 영향을 끼치지 않는 함수
- 비순수 함수(impure function) : 함수의 실행이 외부 상태에 영향을 끼치는 함수
- ⭐️[Built-in Functions](https://docs.python.org/3/library/functions.html)⭐️

```python
def hello():
	print('Hello world!')
hello()  # Hello world!
```

### 값을 여러 개 반환하는 함수
```python
def add(a,b):
	return a+b, a-b  
a = add(2,3) # (a+b, a-b) 튜플로 반환됨
x, y = add(2,3) # x = a+b, y = a-b 언패킹 가능
```

### 위치 인수
함수에 인수를 순서대로 넣는 방식 (=인수의 위치가 정해져 있음)

- 인수를 순서대로 넣을 때, 리스트나 튜플 사용하여 언패킹 가능
- 함수(*리스트)
- 함수(*튜플)
```python
def number(a,b):
	print(a)
	print(b)
x = [10,20]  # 10
number(*x)   # 20
```

### 가변 인수
- 인수의 개수가 정해지지 않았을 때 사용, 매개변수 앞에 * 붙임
- 함수(*리스트)
- 함수(*튜플)
```python
def number(*args): 
	for i in args:
		print(i)  # 들어온 숫자 개수만큼 출력

number(10, 20, 30, 40) # 10\n 20\n 30\n 40\n
y = [10, 20, 30, 40]
number(*y)  # 10\n 20\n 30\n 40\n
```
- 고정 인수와 가변 인수 함께 사용하기
```python
def number(a, *args):  # !!!!! 반드시 고정 인수가 가변 인수보다 앞에 오도록 하기
	print(a)
	print(args) 
```

### 키워드 인수
- 인수의 순서와 용도를 매번 기억하지 않아도 되도록 사용하는 기능
- 함수(키워드=값)
```python
def info(name, age, address):
	print(f"{name}은, {age}살, 주소는 {address}"})
info(name = '정수현', address = '경기도', age = 28) # 키워드 인수는 순서 바뀌어도 상관X
```

### 키워드 인수 + 딕셔너리 언패킹
- 함수의 매개변수와 딕셔너리의 키의 개수와 이름이 동일해야함
- 함수(**딕셔너리)
함수(*딕셔너리)로 호출할 경우, 딕셔너리의 값이 아닌 key만 호출된다.
```python
def info(name, age, address):
	print(f"{name}은, {age}살, 주소는 {address}"})

x = {'name': 정수현, 'age': 28, 'address': 경기도}
info(**x)  # 정수현은 28살, 경기도
```

### 키워드 인수를 사용하는 가변 인수 함수
- def 함수(**매개변수)
```python
def info(**kwargs):
	if 'name' in kwargs:
		print('이름: ', kwargs['name'])
	for k,v in kwrgs.items():
			print(k,v)
```

### 초깃값이 지정된 매개변수
** 초깃값이 지정된 매개변수는 뒤에 사용한다.
```python
def info(name, age, address = '비공개'):
	print(f"{name}은, {age}살, 주소는 {address}"})
```

### 위치 인수 + (키워드+가변) 인수
```python
def custom_print(*args, **kwargs):
	print(*args, **kwargs)
# 출력할 값을 위치 인수, sep, end 등을 키워드 인수로
custom_print(1,2,3, sep=':', end ='') # 1:2:3
```

### ** 리스트에 함수 넣기
```python
def hello():
	print('Hello, world!')

y = [hello, hello()]  
y[0]() # 함수를 그대로 넣으면, 변수에 할당하거나 호출 가능
y[1] # 함수() 형태로 넣으면, 반환값이 들어감
```

### 함수 독스트링
함수에 대한 설명을 넣는 부분
```python
def 함수이름(매개변수):
    """독스트링"""
    코드
print(함수이름.__doc__) # 함수의 독스트링 출력
print( help(함수이름) ) # 함수의 이름, 매개변수, 독스트링을 도움말 형태로 출력
```

### return - 함수 중간에서 빠져나오기
```python
def ten(a):  # 값이 10이면, 함수에서 바로 빠져나오기
	if a == 10:
		return  
	print("10이 아닙니다")
```

---

### 재귀 호출 (Recursive call)
함수 안에서 함수 자기 자신을 호출하는 방식

- 파이썬의 최대 재귀 깊이 : 1000 를 초과하면, RecursionError 발생  → 종료 조건 필수
- 최대 재귀 깊이를 늘리려면,  sys.setrecursionlimit 사용
```python title="팩토리얼"
def fectorial(n):
	if n == 1:  # 종료 조건
		return 1
	return n * factorial(n-1)

print(factorial(5))
```

### 함수 안에서 함수 만들기
``` python
def print_hello():
	hello = "Hello, world!"
	def print_message():
		print(hello) # 바깥 함수의 지역 변수 사용
	print_message()

print_hello()  # Hello, world!
```

- print_hello()의 지역 변수는 그 안에 속한 모든 함수에서 접근 가능
- 변경은 `nonlocal`: 현재 함수의 바깥쪽에 있는 지역 변수를 찾을 때, 가장 가까운 함수부터 찾음
```python
def A():
	x = 10
	def B():
		nonlocal x
		x =20
	B()
	print(x)

A()  # 20
```


---

### 람다 표현식 (Lambda expression)
- 변수 = lambda 매개변수들: 식
- (lambda 매개변수들: 식) (인수들)
```python 
lambda x: x+10  # <function <lambda> at 0x02C27270>
plus_ten = lambda x: x+10
plus_ten(1)  # 11
(lambda x: x+10)(1) # 11
```

### ** 람다 표현식 안에서는 변수 생성 X
- 외부 변수를 사용하거나 변수 생성이 필요한 경우, def로 함수 작성 
```python 
(lambda x: y = 10; x+y)(1) # SyntaxError: invalid syntax
y=10
(lambda x: x+y)(1) # 11
```

### 람다 표현식을  다른 함수의 인수로 사용
```python 
list(map(lambda x: x+10, [1,2,3]))
```

### 람다 표현식과 조건부 표현식   map + filter + reduce
- map
- filter(함수, 반복가능한객체)
- reduce(함수, 반복가능한객체)
=== "map"
	```python 
	# lambda 매개변수들: 식1 if 조건식 else 식2  ( ** else 반드시 사용! )
	a = [i for i in range(1,11)]
	list(map(lambda x: str(x) if x % 3 ==0 else x, a)) # [1,2,'3',4,5,'6',7,8,'9',10]
	
	# lambda 매개변수들: 식1 if 조건식1 else 식2 if 조건식2 else 식3  → 가독성이 낮아 안좋은 예제
	list(map(lambda x: str(x) if x ==1 else float(x) if x==2 else x+10, a)) # ['1', 2.0, 13, 14, 15, 16, 17, 18, 19, 20]

	# map을 이용하여 리스트 2개 처리하기 ( 리스트 개수만큼 매개변수(x,y) 지정)
	a = [1,2,3,4,5]
	b = [2,4,6,8,10]
	list(map(lambda x,y : x*y, a, b) # [2, 8, 18, 32, 50]
	```
=== "filter"
	```python 
	# 지정한 함수의 반환값이 True일 때, 반복 가능한 객체에서 특정 조건에 맞는 요소만 가져옴
	a = [8, 3, 2, 10, 15, 7, 1, 9, 0, 11]
	list(filter(lambda x: x>5 and x<10, a))
	```
=== "reduce"
	```python 
	# 반복 가능한 객체의 각 요소를 지정된 함수로 처리한 뒤, 이전 결과와 누적해서 반환하는 함수
	from functools import reduce
	a = [1,2,3,4,5]
	reduce(lambda x,y : x+y, a) # 15
	```