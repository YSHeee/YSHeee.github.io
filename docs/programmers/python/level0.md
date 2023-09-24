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

### 조건 문자열 [note](../../language/python/note/1.md)
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

## 2023.09.08

### 등차수열의 특정한 항만 더하기
두 정수 a, d와 길이가 n인 boolean 배열 included가 주어집니다. 첫째항이 a, 공차가 d인 등차수열에서 included[i]가 i + 1항을 의미할 때, 이 등차수열의 1항부터 n항까지 included가 true인 항들만 더한 값을 return 하는 solution 함수를 작성해 주세요.

=== "My code"
    ``` python
    def solution(a, d, included):
        return sum(a+d*idx for idx,value in enumerate(included) if value)
    ```
=== "Others"
    ``` python 
    def solution(a, d, included):
        return sum((a+d*idx)*int(included[idx]) for idx in range(len(included)))
    ``` 

### 원소들의 곱과 합
정수가 담긴 리스트 num_list가 주어질 때, 모든 원소들의 곱이 모든 원소들의 합의 제곱보다 작으면 1을 크면 0을 return하도록 solution 함수를 완성해주세요.

``` python
from functools import reduce
def solution(num_list):
    return int(sum(num_list)**2 > reduce(lambda x,y: x*y, num_list))
```

## 2023.09.12

### 수 조작하기 1
정수 n과 문자열 control이 주어집니다. control은 "w", "a", "s", "d"의 4개의 문자로 이루어져 있으며, control의 앞에서부터 순서대로 문자에 따라 n의 값을 바꿉니다. 규칙에 따라 n을 바꿨을 때 가장 마지막에 나오는 n의 값을 return 하는 solution 함수를 완성해 주세요.

=== "My code"
    ``` python
    def solution(n, control):
        for i in control:
            if i == 'w': n+=1
            elif i == 's': n-=1
            elif i == 'd': n+=10
            else: n-=10
        return n
    ```
=== "Others"
    ``` python 
    def solution(n, control):
        key = dict(zip(['w','s','d','a'], [1,-1,10,-10]))
        return n + sum([key[c] for c in control])
    ``` 
=== "Others2"
    ``` python 
    def solution(n, control):
        return n + 10*(control.count('d')-control.count('a')) + (control.count('w')-control.count('s'))
    ``` 

### 수 조작하기 2
정수 배열 numLog가 주어집니다. 처음에 numLog[0]에서 부터 시작해 "w", "a", "s", "d"로 이루어진 문자열을 입력으로 받아 순서대로 조작을 했다고 합시다.
그리고 매번 조작을 할 때마다 결괏값을 기록한 정수 배열이 numLog입니다. 즉, numLog[i]는 numLog[0]로부터 총 i번의 조작을 가한 결과가 저장되어 있습니다.
주어진 정수 배열 numLog에 대해 조작을 위해 입력받은 문자열을 return 하는 solution 함수를 완성해 주세요.
``` python
def solution(numLog):
    table = dict(zip([1,-1,10,-10],['w','s','d','a']))
    return ''.join(table[numLog[i]-numLog[i-1]] for i in range(1, len(numLog)))
```

### 수열과 구간 쿼리 3
정수 배열 arr와 2차원 정수 배열 queries이 주어집니다. queries의 원소는 각각 하나의 query를 나타내며, [i, j] 꼴입니다.
각 query마다 순서대로 arr[i]의 값과 arr[j]의 값을 서로 바꿉니다.
위 규칙에 따라 queries를 처리한 이후의 arr를 return 하는 solution 함수를 완성해 주세요.

=== "My code"
    ``` python
    def solution(arr, queries):
        temp = 0
        for val in queries:
            temp = arr[val[0]]
            arr[val[0]] = arr[val[1]]
            arr[val[1]] = temp
        return arr
    ```
=== "Others"
    ``` python 
    def solution(arr, queries):
        temp = 0
        for val in queries:
            arr[val[0]], arr[val[1]] = arr[val[1]], arr[val[0]]
        return arr
    ``` 

### 수열과 구간 쿼리 2
정수 배열 arr와 2차원 정수 배열 queries이 주어집니다. queries의 원소는 각각 하나의 query를 나타내며, [s, e, k] 꼴입니다.
각 query마다 순서대로 s ≤ i ≤ e인 모든 i에 대해 k보다 크면서 가장 작은 arr[i]를 찾습니다.
각 쿼리의 순서에 맞게 답을 저장한 배열을 반환하는 solution 함수를 완성해 주세요.
단, 특정 쿼리의 답이 존재하지 않으면 -1을 저장합니다.
``` python
def solution(arr, queries):
    answer = []
    for query in queries:
        value_list = list(filter(lambda x: query[2]<x, arr[query[0]:query[1]+1]))
        answer.append((min(value_list) if value_list else -1))
    return answer
```

## 2023.09.15

### 약수 구하기
정수 n이 매개변수로 주어질 때, n의 약수를 오름차순으로 담은 배열을 return하도록 solution 함수를 완성해주세요.
``` python
def solution(n):
    answer = [i for i in range(1, n//2+1) if n%i==0]
    answer.append(n)
    return answer
```

## 2023.09.22

### 배열 만들기 2
정수 l과 r이 주어졌을 때, l 이상 r이하의 정수 중에서 숫자 "0"과 "5"로만 이루어진 모든 정수를 오름차순으로 저장한 배열을 return 하는 solution 함수를 완성해 주세요.

만약 그러한 정수가 없다면, -1이 담긴 배열을 return 합니다.

``` python
def solution(l, r):
    result = []
    
    for i in range(1, 64): # 2진수 1~111111
        num = 5 * int(bin(i)[2:])
        if num > r:
            break
        if num >= l and num <= r:
            result.append(num)
    return result if result else [-1]
```