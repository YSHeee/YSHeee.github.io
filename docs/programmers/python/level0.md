## 2023.08.24

- 문자열 출력하기 `print(str)`
- a와 b 출력하기 `print(f"a = {a}\nb = {b}")`
- 문자열 반복해서 출력하기 `print(a*int(b))`

### 대소문자 바꿔서 출력하기 
영어 알파벳으로 이루어진 문자열 str이 주어집니다. <br>
각 알파벳을 대문자는 소문자로 소문자는 대문자로 변환해서 출력하는 코드를 작성해 보세요.

=== "My code"
    ``` python 
    print(''.join(chr(ord(ch)+32) if ord(ch)<97 else chr(ord(ch)-32) for ch in input()))
    ``` 
=== "Others"
    ``` python 
    print(input().swapcase()) #CASE-1
    print(''.join(x.upper() if x == x.lower() else x.lower() for x in input())) #CASE-2
    ``` 

## 2023.09.06
- 특수문자 출력하기 `print("!@#$%^&*(\\'\"<>?:;")` - Others: `print(r'!@#$%^&*(\'"<>?:;')`
- 덧셈식 출력하기 `print(f"{a} + {b} = {a+b}")`
- 문자열 붙여서 출력하기 `print(f"{str1}{str2}")` - Others: `input().strip().replace(' ', '')`
- 문자열 돌리기 `for i in input(): print(i)` - Others: `print('\n'.join(input()))`  

### 홀짝 구분하기
자연수 n이 입력으로 주어졌을 때 만약 n이 짝수이면 "n is even"을, 홀수이면 "n is odd"를 출력하는 코드를 작성해 보세요.

=== "My code"
    ``` python 
    a = int(input())
    print(f"{a} is even" if a%2==0 else f"{a} is odd")
    ``` 
=== "Others"
    ``` python 
    n=int(input())
    print(f"{n} is {'eovdedn'[n&1::2]}")
    ``` 