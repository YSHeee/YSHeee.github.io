# Level 1

## 2023.09.15

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

---
## 2023.09.16
### 달리기 경주
얀에서는 매년 달리기 경주가 열립니다. 해설진들은 선수들이 자기 바로 앞의 선수를 추월할 때 추월한 선수의 이름을 부릅니다. 예를 들어 1등부터 3등까지 "mumu", "soe", "poe" 선수들이 순서대로 달리고 있을 때, 해설진이 "soe"선수를 불렀다면 2등인 "soe" 선수가 1등인 "mumu" 선수를 추월했다는 것입니다. 즉 "soe" 선수가 1등, "mumu" 선수가 2등으로 바뀝니다.

선수들의 이름이 1등부터 현재 등수 순서대로 담긴 문자열 배열 players와 해설진이 부른 이름을 담은 문자열 배열 callings가 매개변수로 주어질 때, 경주가 끝났을 때 선수들의 이름을 1등부터 등수 순서대로 배열에 담아 return 하는 solution 함수를 완성해주세요.

=== "My code"
    ``` python
    def solution(players, callings):
        name_table = {players[i]:i for i in range(len(players))}
        index_table = {i:players[i] for i in range(len(players))}
        
        for name in callings:
            
            # {'mumu': 0, 'soe': 1, 'poe': 2, 'kai': 3, 'mine': 4} -> {'mumu': 0, 'soe': 1, 'poe': 3, 'kai': 2, 'mine': 4}
            name_table[name] -=1
            index = name_table[name]
            name_table.update({index_table[index]: name_table[name]+1})
            
            # {0: 'mumu', 1: 'soe', 2: 'poe', 3: 'kai', 4: 'mine'} -> {0: 'mumu', 1: 'soe', 2: 'kai', 3: 'poe', 4: 'mine'}
            index_table[index], index_table[index+1] =  name, index_table[index]

        return [i for i in index_table.values()]
    ```
=== "Others"
    ``` python
    def solution(players, callings):
        table = {players[i]:i for i in range(len(players))}
        
        for name in callings:
            
            index = table[name]
            table[name] -=1
            table[players[index-1]] +=1
            
            players[index-1], players[index] = players[index], players[index-1]

        return players
    ```
---
## 2023.09.17
### 완주하지 못한 선수
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

=== "My code"
    ``` python
    from collections import Counter
    def solution(participant, completion):
        
        count = Counter(participant)
        
        for name in completion:
            count[name] -= 1
        
        for key,value in count.items():
            if value != 0:
                return key
    ```
=== "Others"
    ``` python
    from collections import Counter
    def solution(participant, completion):
        result =  Counter(participant) - Counter(completion)
        return list(result)[0]
    ```
