# List Comprehension
List : 목록, 값을 일렬로 늘어놓은 형태<br>
리스트 안에 식, for 반복문, if 조건문 등을 지정하여 리스트를 생성하는 것
``` python
li = [i for i in range(10)] # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

- [식 for 변수 in 리스트 if 조건식]
``` python
[i + 5 for i in range(10) if i % 2 == 0] # [5, 7, 9, 11, 13] 0부터 9까지 숫자 중 짝수+5로만 리스트 생성 
```
- [식 for 변수1 in 리스트1 if 조건식1 for 변수2 in 리스트2 if 조건식 2 …]
``` python
[i*j for j in range(2,10) for i in range(1,10)] #  2단부터 9단까지 구구단
```

### list + map
- list(map(함수, 리스트))
- tuple(map(함수, 튜플))
=== "range"
    ``` python
    a = list(map(str, range(10)))  # a = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
    ```
=== "map"
    ``` python
    a = [1.2, 2.5, 3.7, 4.6]
    a = list(map(int, a)) # a = [1, 2, 3, 4]
    ```
=== "for"
    ``` python
    a = [1.2, 2.5, 3.7, 4.6]
    for i in range(len(a)):
        a[i] = int(a[i])    # a = [1, 2, 3, 4]
    ```

### input.split + map
- map + input().split()
``` python
a = map(int, input().split())  # 10 20 (입력)
print(a) # <map object at 0x03DFB0D0>
list(a) # [10, 20]
```
- map이 반환하는 map 객체는 이터레이터이므로 변수 여러 개에 저장하는 언패킹(Unpacking) 가능
``` python
a, b = map(int, input().split()) # 10 20 (입력)
print(a) # 10
print(b) # 20
```

### 요소 추가
- append: 요소 하나 추가
- extend: 리스트를 연결하여 확장
- insert: 특정 인덱스에 요소 추가
=== "append"
    ``` python
    a = [1,2,3,4,5]
    a.append(500) # a = [1,2,3,4,5,500]
    a.append([500,600]) # a= [1,2,3,4,5,[500,600]]
    ```
=== "extend"
    ``` python
    a.extend([500,600]) # a = [1,2,3,4,5,500,600]
    ```
=== "insert"
    ``` python
    a.insert(0,500) # a = [500,1,2,3,4,5]
    a.insert(len(a), 500) # a= [1,2,3,4,5,500]
    a.insert(1, [500,600]) # a = [1,[500,600],2,3,4,5]
    ```

### 요소 삭제
- pop: 리스트의 마지막 요소를 삭제한 뒤 삭제한 요소 반환
- remove: 특정 값을 찾아서 삭제
=== "pop"
    ``` python
    a = [1,2,3,4,5]
    a.pop() # 5, a = [1,2,3,4]
    a.pop(1) # 2, a= [1,3,4,5]
    ```
=== "del"
    ``` python
    del a[1] # a = [1,3,4,5]
    ```
=== "remove"
    ``` python
    a.remove(3) # a = [1,2,4,5] 값이 여러개 일 경우에는, 처음 찾은 값 삭제
    ```

### 특정 값의 인덱스
- index : 리스트에서 특정 값의 인덱스를 구함 (여러 개일 경우, 처음 찾은 값의 인덱스 반환)
``` python
b = [10,20,30,15,20,40]
b.index(20) # 1
```

### 특정 값의 개수
- count: 리스트에서 특정 값의 개수
``` python
b = [10,20,30,15,20,40]
b.count(20) # 2
```

### 정렬 & 순서 뒤집기
- reverse: 요소의 순서를 반대로 뒤집기
- sort() / sort(reverse=False): 리스트의 값을 작은 순서대로 정렬 (오름차순)
- sort(reverse=True): 리스트의 값을 큰 순서대로 정렬 (내림차순)
- **sort: 리스트 내용을 변경  vs  sorted:  정렬된 새 리스트 생성**
``` python
a.reverse() # [5,4,3,2,1]
b.sort() # [10,15,20,20,30,40]
sorted(b) # [10,15,20,20,30,40]
```

### 리스트의 모든 요소 삭제
``` python
a.clear() # a = []
del a[:] # a= []
```

---

### 빈 리스트인지 확인하기
``` python
if not list: # 리스트가 비어 있으면 True
if list: # 리스트에 내용이 있으면 True
```

### 할당과 복사
- **할당** : c와 d는 같은 객체이므로 변경 사항 공유
``` python
c = d
c is d # True
```
- **복사** :  c와 d는 다른 객체이므로 변경 사항을 공유하지 않음
``` python
d = c.copy() # 요소 복사
c is d  # False
c == d  # True, 복사 했으므로 값은 같음.
```

### 인덱스와 요소를 함께 출력하기
- for 인덱스, 요소 in enumerate(리스트):
- while
=== "1"
    ``` python
    for index, value in enumerate(c):
        print(index, value) 
    ```
=== "2"
    ``` python
    for index, value in enumerate(c, 1): #인덱스를 1부터 시작
        print(index, value) 
    ```
=== "3"
    ``` python
    i = 0
    while i <= len(a):
        print(i, a[i])
        i+=1
    ```

### 가장 작은 수 구하기
=== "for"
    ``` python
    small = a[0]
    for i in a:
        if i < smallest: # 가장 큰 수는 부호 >으로
            smallest = i
    ```
=== "sort"
    ``` python
    a.sort()  # 가장 큰 수는 a.sort(reverse=True)
    a[0]
    ```
=== "min, max"
    ``` python
    min(a) 
    max(a) 
    ```

### 요소 합계
=== "for"
    ``` python
    x=0
    for i in a:
        x += i
    ```
=== "sum"
    ``` python
    sum()
    ```

---

### 2차원 list
``` python
a = [[10,20], [30,40], [50,60]] # a[세로][가로]
```

### 2차원 요소 출력
=== "for 1"
    ``` python
    for x,y in a:   # 10 20 
        print(x,y)  # 30 40
    ```
=== "for 2"
    ``` python
    for i in a:
        for j in i:
            print(j, end = ' ')
        print() 
    ```
=== "while"
    ``` python
    i=0
    while i < len(a):
        x,y = a[i]
        print(x,y)
        i+=1
    ```

### 2차원 list 생성
=== "List Comprehension"
    ``` python
    a = [[0]*2 for i in range(3)]  # [[0,0], [0,0], [0, 0]]
    a = [[0 for j in range(2)] for i in range(3)] # [[0,0], [0,0], [0, 0]]
    ```
=== "for 1"
    ``` python
    a=[]
    for i in range(10):
        a.append(0) # [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    ```
=== "for 2"
    ``` python
    for i in range(3):
        line = []
        for i in range(2):
            line.append(0)
        a.append(line) # [[0,0], [0,0], [0, 0]]
    ```

### 톱니형 리스트
``` python
a = [3,1,3,2,5] # 가로 크기
b = [] # 빈 리스트 생성
for i in a: # 가로 크기를 저장한 리스트 반복
	line=[] # 안쪽 리스트로 사용할 빈 리스트 생성
	for j in range(i): # 리스트 a에 저장된 가로 크기만큼 반복
		line.append(0) 
	b.append(line) # 안쪽 리스트를 b 리스트에 추가
print(b)  # [[0, 0, 0], [0], [0, 0, 0], [0, 0], [0, 0, 0, 0, 0]]
```

### 2차원 리스트 정렬 sorted
- sorted (반복가능한객체, key=정렬함수, reverse= True 또는 False)

### 2차원 리스트 할당과 복사
- **할당** : `a=b`,  `b=a.copy()`
- **복사** : `b = copy.deepcopy(a)` 2차원 이상의 다차원 리스트는 복사할 때, copy 모듈의 deepcopy 함수 사용