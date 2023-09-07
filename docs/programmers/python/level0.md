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

- 특수문자 출력하기 `print("!@#$%^&*(\\'\"<>?:;")` 
    - Others: `print(r'!@#$%^&*(\'"<>?:;')`
- 덧셈식 출력하기 `print(f"{a} + {b} = {a+b}")`
- 문자열 붙여서 출력하기 `print(f"{str1}{str2}")` 
    - Others: `input().strip().replace(' ', '')`
- 문자열 돌리기 `for i in input(): print(i)` 
    - Others: `print('\n'.join(input()))`  
- 문자 리스트를 문자열로 변환하기 `"".join(arr)`
- 문자열 곱하기 `solution = lambda my_string, k: my_string*k`
- 더 크게 합치기  
    - `solution = lambda a, b: int(f"{a}{b}") if int(f"{a}{b}")>=int(f"{b}{a}") else int(f"{b}{a}")`
    - `solution = lambda a, b: max(int(f"{a}{b}"), int(f"{b}{a}"))`

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

### 문자열 섞기
길이가 같은 두 문자열 str1과 str2가 주어집니다.
두 문자열의 각 문자가 앞에서부터 서로 번갈아가면서 한 번씩 등장하는 문자열을 만들어 return 하는 solution 함수를 완성해 주세요.

=== "My code"
    ``` python 
    def solution(str1, str2):
        return "".join([f"{value}{str2[idx]}" for idx, value in enumerate(str1)]) 
    ``` 
=== "Others"
    ``` python 
    def solution(str1, str2):
        res=''
        for s1,s2 in zip(str1,str2):
            res+=s1+s2
        return res
    ``` 

## 2023.09.07

- 두 수의 연산값 비교하기 `solution = lambda a,b: max(int(f"{a}{b}"), 2*a*b)`
- n의 배수 `solution = lambda num,n: 1 if num%n==0 else 0`
    - Others : `solution = lambda num,n: int(not(num % n))`
- flag에 따라 다른 값 반환하기 `solution = lambda a,b,flag: a+b if flag else a-b`


### 홀짝에 따라 다른 값 반환하기
양의 정수 n이 매개변수로 주어질 때, n이 홀수라면 n 이하의 홀수인 모든 양의 정수의 합을 return 하고 n이 짝수라면 n 이하의 짝수인 모든 양의 정수의 제곱의 합을 return 하는 solution 함수를 작성해 주세요.

=== "My code"
    ``` python 
    def solution(n):
        return sum([i if (n%2 & i%2) else i**2 if not(n%2 | i%2) else 0 for i in range(n,0,-1)])
    ``` 
=== "Others"
    ``` python 
    def solution(n):
        return sum(x ** (2 - x % 2) for x in range(n + 1) if n % 2 == x % 2)
    ``` 

### 코드 처리하기
=== "My code"
    ``` python
    def solution(code):
        mode = 0
        ret = []
        
        for idx,value in enumerate(code):
            if value == '1':
                mode = abs(mode-1)
        
            elif mode == idx%2:
                ret.append(value)

        return ''.join(ret) if ret else "EMPTY"
    ```
=== "Others"
    ``` python 
    def solution(n):
        return sum(x ** (2 - x % 2) for x in range(n + 1) if n % 2 == x % 2)
    ``` 

### 조건 문자열 [note](../../python/note/1.md)
두 문자열 ineq와 eq가 주어집니다. ineq는 "<"와 ">"중 하나고, eq는 "="와 "!"중 하나입니다. 그리고 두 정수 n과 m이 주어질 때, n과 m이 ineq와 eq의 조건에 맞으면 1을 아니면 0을 return하도록 solution 함수를 완성해주세요.
=== "My code"
    ``` python
    def solution(ineq, eq, n, m):
        val = ord(ineq)+ord(eq)
        if val < 100:
            return int(n<m) if val==93 else int(n>m)
        else:
            return int(n<=m) if val==121 else int(n>=m)
    ```
=== "Others"
    ``` python 
    def solution(ineq, eq, n, m):
        return int(eval(str(n)+ineq+eq.replace('!', '')+str(m)))
    ``` 