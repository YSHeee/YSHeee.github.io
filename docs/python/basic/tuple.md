# Tuple
내용을 변경할 수 없는 Immutable한 데이터
``` python
a = (38,21,53,62,19,53)
```

- index() : 특정 값 인덱스
- count() : 특정 값 개수
- min() : 가장 작은 수
- max() : 가장 큰 수
- sum() : 합계

### Tuple Comprehension
- tuple(식 for 변수 in 리스트 if 조건식)
``` python
a = tuple(i for i in range(10) if i % 2 == 0)  # a = (0, 2, 4, 6, 8)
```
!!  tuple을 쓰지 않으면, 튜플이 아니라 제너레이터 표현식이 됨
``` python
(i for i in range(10) if i % 2 ==0)  # <generator object <genexpr> at 0x050FE420>
```