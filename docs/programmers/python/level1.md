# Level 1

### 약수의 합
정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수, solution을 완성해주세요.
``` python
def solution(n):
    answer = [i for i in range(1, n//2+1) if n%i==0]
    return sum(answer) + n
```

### 최대공약수와 최소공배수
두 수를 입력받아 두 수의 최대공약수와 최소공배수를 반환하는 함수, solution을 완성해 보세요. 배열의 맨 앞에 최대공약수, 그다음 최소공배수를 넣어 반환하면 됩니다. 예를 들어 두 수 3, 12의 최대공약수는 3, 최소공배수는 12이므로 solution(3, 12)는 [3, 12]를 반환해야 합니다.

=== "1"
    ``` python
    def cal_divisor(x):
        divisor = {i for i in range(1, x//2+1) if x%i==0}
        divisor.add(x)
        return divisor

    def solution(n, m):
        com_factor = cal_divisor(n) & cal_divisor(m)
        gcd = max(com_factor)
        lcm = (n*m)/gcd
        return [gcd, lcm]
    ```
=== "2 euclidean"
    ``` python
    def solution(n, m):
        a, b = min(n,m), max(n,m)
        while(a!=0):
            r = b % a
            b,a = a,r
        return [b, n*m/b]
    ```

### 약수의 개수와 덧셈
두 정수 left와 right가 매개변수로 주어집니다. left부터 right까지의 모든 수들 중에서, 약수의 개수가 짝수인 수는 더하고, 약수의 개수가 홀수인 수는 뺀 수를 return 하도록 solution 함수를 완성해주세요.

=== "My code"
    ``` python
    def solution(left, right):
        answer = 0
        for i in range(left, right+1):
            num = len([j for j in range(1,i//2+1) if i%j==0])+1
            if num%2==0:
                answer += i
            else:
                answer -= i
        return answer
    ```
=== "Others"
    ``` python
    def solution(left, right):
        answer = 0
        for i in range(left,right+1):
            if int(i**0.5)==i**0.5:
                answer -= i
            else:
                answer += i
        return answer
    ```