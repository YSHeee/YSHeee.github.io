# Cheat Sheet

## 연산자

|   연산자  |   의미   |
| :-----: | :-----: |
|`+`, `-`, `*`, `/`| 사칙연산
|`%`, `MOD`| 나머지
| `IS` | 양쪽이 모두 TRUE 또는 FALSE
| `IS NOT` | 한쪽은 TRUE, 한쪽은 FALSE
| `AND`, `&&` | 양쪽이 모두 TRUE 일 때만 TRUE
| `OR`, `||` | 한쪽이라도 TRUE이면 TRUE
| `=` | 양쪽 값이 같음
| `!=`, `<>` | 양쪽 값이 다름
| `>`, `<` | (좌측, 우측) 값이 더 큼
| `>=`, `<=` | (좌측, 우측) 값이 같거나 더 큼
| `BETWEEN {MIN} AND {MAX}` | 두 값 사이에 있음
| `NOT BETWEEN {MIN} AND {MAX}` | 두 값 사이가 아닌 곳에 있음
| `IN` | 해당 값들 중에 있음
| `NOT IN` | 해당 값들 중에 없음
| `LIKE '..%..'` | 0~N개 문자를 가진 패턴
| `LIKE '.._..'` | `_` 개수만큼의 문자를 가진 패턴

---

## 숫자 관련 함수
![NUM](../images/number.png)

## 문자 관련 함수
![CHAR](../images/char.png)

- `CHAR(ASCII번호)` : ASCII 코드 번호를 문자나 숫자로 변경


## 날짜 관련 함수
![DATE](../images/date.png)

- `DATEDIFF(날짜1, 날짜2)` : 날짜1-날짜2 값 반환 (DAY)
- `TIMESTAMPDIFF(단위, 날짜1, 날짜2)` : SECOND, MINUTE, HOUR, DAY, WEEK, MONTH, QUARTER(분기), YEAR

## 논리 관련 함수
![LOGICAL](../images/logical.png)
- `COALESCE(표현식1, 표현식2, …)` : 첫번째로 NULL이 아닌 값 반환, 모든 표현식이 NULL이라면 NULL 리턴

---
!!! quote
    - 김정현 강사님