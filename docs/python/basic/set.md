# Set
집합. 중복x 순서x Set(Set())x <br>
순서가 없으므로 출력시 그 순서가 매번 다름. (숫자로만 이루어지면 순서대로 출력)
``` python
# 세트 = {값1, 값2, 값3}
fruits = {'strawberry', 'grape', 'orange', 'cherry'}
```

### 특정 값의 유무 확인
- 값 in 세트  : 특정 값이 있으면 True
``` python
'orange' in fruits  # True
'peach' in fruits  # False
```
- 값 not in 세트  : 특정 값이 없으면 True
``` python
'orange' not in fruits  # False
'peach' not in fruits  # True
```

### set 생성
- set(반복가능한객체)
- frozenset : 변경할 수 없는 set
``` python
a = set('apple')  # a = {'e', 'a', 'l', 'p'}
b = set(range(5))  # b = {0,1,2,3,4}
c = set()  # c = set() 빈 세트
```

### 요소 추가
- add(요소)
``` python
fruits.add('melon')  # fruits = {'strawberry', 'grape', 'orange', 'cherry', 'melon'}
```

### 요소 삭제
- remove(요소) : 세트에서 특정 요소를 삭제, 해당 요소가 없으면 에러 
- discard(요소) : 세트에서 특정 요소를 삭제, 해당 요소가 없으면 Pass
- pop() : 세트에서 임의의 요소를 삭제하고, 해당 요소를 반환 - 없으면 에러 
- clear()  : 모든 요소 삭제
=== "remove"
    ``` python
    fruits.remove('strawberry')  # fruits = {'grape', 'orange', 'cherry'}
    ```
=== "discard"
    ``` python
    fruits.discard('strawberry') # fruits = {'grape', 'orange', 'cherry'}
    friots.discard('watermelon') # fruits = {'strawberry', 'grape', 'orange', 'cherry'}
    ```
=== "pop"
    ``` python
    fruits.pop() # orange,  fruits = {'strawberry', 'grape', 'cherry'}
    ```
=== "clear"
    ``` python
    fruits.clear()  # fruits = set()
    ```

### 요소 개수 구하기
``` python
len(fruits)  # 4
```

### set이 같은지 다른지 확인
- ==  : 순서 상관없이 각 요소만 같으면 참
- !=  : 세트가 다른지 확인
``` python
a = {1,2,3,4}
a == {1,2,3,4}  # True
a != {1,2,3}  # True
```

### set이 겹치는지 확인
- Set.isdisjoint(Other set)  : 겹치는 요소가 있으면 False, 없으면 True 
``` python
a.isdisjoint({5,6,7,8}) # True (겹치는 요소 없음)
a.isdisjoint({3,4,5,6}) # False (a와 3,4 겹침)
```

### Set Comprehension
- {식 for 변수 in 반복가능한 객체 if 조건식}
- set( 식 for 변수 in 반복가능한 객체 if 조건식)
``` python
a = {i for i in 'pineapple' if i not in 'apl'}  # a = {'i', 'n', 'e'}
```
-----

### 집합연산
``` python
a = {1,2,3,4}
b = {3,4,5,6}
```

### 합집합
- 세트1 | 세트 2
- set.union(세트1, 세트2)
``` python
a | b  # {1,2,3,4,5,6}
set.union(a,b)  # {1,2,3,4,5,6}
```

### 교집합
- 세트1 & 세트2
- set.intersection(세트1, 세트2)
``` python
a & b  # {3,4}
set.intersection(a,b)  # {3,4}
```

### 차집합
- 세트1 - 세트2
- set.difference(세트1, 세트2)
``` python
a - b  # {1,2}
set.difference(a, b)  # {1,2}
```

### 대칭차집합 (symmetric difference)
- 세트1 ^ 세트2
- set.symmetric_difference(세트1, 세트2)
``` python
a ^ b  # {1,2,5,6}
set.symmetric_difference(a,b)  # {1,2,5,6}
```

---

### 집합 연산 후 할당 연산자 사용하기
set 자료형에  | & - ^ 연산자와 할당 연산자(=) 을 함께 사용하면, 집합 연산의 결과를 변수에 다시 저장함
``` python
a = {1,2,3,4}
```

### 합집합 
- 세트1 |= 세트2
- 세트1.update(세트2)
``` python
a |= {5}  # a = {1,2,3,4,5}
a.update({5}) # a = {1,2,3,4,5}
```

### 교집합
- 세트1 &= 세트2
- 세트1.intersection_update(세트2)
``` python
a &= {2,3,4}  # a = {2,3,4}
a.intersection_update({2,3,4})  # a = {2,3,4}
```

### 차집합
- 세트1 -= 세트2
- 세트1.difference_update(세트2)
``` python
a ^= {3}  # a = {1,2,4}
a.difference_update({3})  # a = {1,2,4}
```

### 대칭차집합 (symmetric difference)
- 세트1 ^= 세트2
- 세트1.symmetric_difference_update(세트2)
``` python
a ^= {3,4,5,6}  # a = {1,2,5,6}
a.symmetric_difference_update({3,4,5,6})  # a = {1,2,5,6}
```

---

### 부분 집합과 상위 집합 확인하기
set은 부분집합, 진부분집합, 상위집합, 진상위집합과 같이 속하는 관계를 표현할 수 있음.
``` python
a = {1,2,3,4}
```

### 부분집합 
- 현재set <= 다른set
- 현재set.issubset(다른set)
``` python
a <= {1,2,3,4}  # True  
a.issubset({1,2,3,4})  # True  (세트 a가 {1,2,3,4}의 부분집합)
```

### 진부분집합
- 현재set < 다른set
``` python
a < {1,2,3,4,5}  # True (a가 {1,2,3,4,5}의 진부분집합, a={1,2,3,4})
```

### 상위집합
- 현재set >= 다른set
- 현재set.issuperset(다른set)
``` python
a >= {1,2,3,4}  # True (a={1,2,3,4})
a.issuperset({1,2,3,4})  # True
```

### 진상위집합 (proper superset)
- 현재set > 다른set
``` python
a > {1,2,3}  # True (a={1,2,3,4})
```