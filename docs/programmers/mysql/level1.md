# Level 1

## 2023.09.09

### 모든 레코드 조회하기
``` mysql
SELECT *
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

### 역순 정렬하기
``` mysql
SELECT NAME, DATETIME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC;
```

### 아픈 동물 찾기
``` mysql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION = 'Sick'
ORDER BY ANIMAL_ID;
```

### 어린 동물 찾기
``` mysql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS 
WHERE INTAKE_CONDITION != 'Aged'
ORDER BY ANIMAL_ID;
```

### 이름이 없는 동물의 아이디
``` mysql
SELECT ANIMAL_ID
FROM ANIMAL_INS 
WHERE NAME IS NULL
ORDER BY ANIMAL_ID;
```

### 동물의 아이디와 이름
``` mysql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID;
```

### 여러 기준으로 정렬하기
``` mysql
SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS 
ORDER BY NAME, DATETIME DESC;
```

### 상위 n개 레코드
``` mysql
SELECT NAME 
FROM ANIMAL_INS 
ORDER BY DATETIME LIMIT 1;
```

### 이름이 있는 동물의 아이디
``` mysql
SELECT ANIMAL_ID
FROM ANIMAL_INS 
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID;
```

### 최댓값 구하기
``` mysql
SELECT MAX(DATETIME) AS 시간
FROM ANIMAL_INS
```

### 강원도에 위치한 생산공장 목록 출력하기
``` mysql
SELECT FACTORY_ID, FACTORY_NAME, ADDRESS
FROM FOOD_FACTORY 
WHERE ADDRESS LIKE '%강원도%'
ORDER BY FACTORY_ID;
```

### 경기도에 위치한 식품창고 목록 출력하기
``` mysql
SELECT WAREHOUSE_ID, WAREHOUSE_NAME, ADDRESS, IFNULL(FREEZER_YN, 'N')
FROM FOOD_WAREHOUSE  
WHERE ADDRESS LIKE '%경기도%'
ORDER BY WAREHOUSE_ID;
```

### 나이 정보가 없는 회원 수 구하기
``` mysql
SELECT COUNT(*) AS USERS
FROM USER_INFO
WHERE AGE IS NULL
```

### 조건에 맞는 회원수 구하기
``` mysql
SELECT COUNT(*) AS USERS
FROM USER_INFO 
WHERE YEAR(JOINED) = 2021 AND AGE BETWEEN 20 AND 29
```

### 가장 비싼 상품 구하기
``` mysql
SELECT MAX(PRICE) AS MAX_PRICE
FROM PRODUCT 
```

### 12세 이하인 여자 환자 목록 출력하기
``` mysql
SELECT PT_NAME, PT_NO, GEND_CD, AGE, IFNULL(TLNO,'NONE') AS TLNO
FROM PATIENT
WHERE AGE <= 12 and GEND_CD = 'W'
ORDER BY AGE DESC, PT_NAME;
```

### 흉부외과 또는 일반외과 의사 목록 출력하기
``` mysql
SELECT DR_NAME, DR_ID, MCDP_CD, DATE_FORMAT(HIRE_YMD, '%Y-%m-%d') AS HIRE_YMD
FROM DOCTOR
WHERE MCDP_CD IN ('CS', 'GS')
ORDER BY HIRE_YMD DESC, DR_NAME;
```

### 인기있는 아이스크림
``` mysql
SELECT FLAVOR
FROM FIRST_HALF
ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID;
```

### 과일로 만든 아이스크림 고르기
=== "sub query"
    ``` mysql
    SELECT FLAVOR
    FROM FIRST_HALF
    WHERE TOTAL_ORDER > 3000 AND FLAVOR IN (
        SELECT FLAVOR
        FROM ICECREAM_INFO
        WHERE INGREDIENT_TYPE = 'fruit_based')
    ORDER BY TOTAL_ORDER DESC;
    ```
=== "join"
    ``` mysql
    SELECT F.FLAVOR
    FROM FIRST_HALF AS F
        JOIN ICECREAM_INFO AS I
        ON F.FLAVOR = I.FLAVOR
    WHERE F.TOTAL_ORDER > 3000 and I.INGREDIENT_TYPE = 'fruit_based'
    ORDER BY F.TOTAL_ORDER DESC;
    ```

### 조건에 맞는 도서 리스트 출력하기
``` mysql
SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
FROM BOOK 
WHERE CATEGORY = '인문' and YEAR(PUBLISHED_DATE) = 2021
ORDER BY PUBLISHED_DATE;
```

### 평균 일일 대여 요금 구하기
CAR_RENTAL_COMPANY_CAR 테이블에서 자동차 종류가 'SUV'인 자동차들의 평균 일일 대여 요금을 출력하는 SQL문을 작성해주세요. 이때 평균 일일 대여 요금은 소수 첫 번째 자리에서 반올림하고, 컬럼명은 AVERAGE_FEE 로 지정해주세요.
``` mysql
SELECT ROUND(AVG(DAILY_FEE)) AS AVERAGE_FEE
FROM CAR_RENTAL_COMPANY_CAR 
WHERE CAR_TYPE = 'SUV' 
```

## 2023.09.09

### 자동차 대여 기록에서 장기/단기 대여 구분하기
CAR_RENTAL_COMPANY_RENTAL_HISTORY 테이블에서 대여 시작일이 2022년 9월에 속하는 대여 기록에 대해서 대여 기간이 30일 이상이면 '장기 대여' 그렇지 않으면 '단기 대여' 로 표시하는 컬럼(컬럼명: RENT_TYPE)을 추가하여 대여기록을 출력하는 SQL문을 작성해주세요. 결과는 대여 기록 ID를 기준으로 내림차순 정렬해주세요.
``` mysql
SELECT HISTORY_ID, CAR_ID, 
        DATE_FORMAT(START_DATE, "%Y-%m-%d") AS "START_DATE", 
        DATE_FORMAT(END_DATE, "%Y-%m-%d") AS "END_DATE", 
        IF(DATEDIFF(END_DATE, START_DATE)+1 >= 30, "장기 대여", "단기 대여") AS "RENT_TYPE"
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE YEAR(START_DATE)=2022 and MONTH(START_DATE)=9
ORDER BY HISTORY_ID DESC;
```

### 특정 옵션이 포함된 자동차 리스트 구하기
CAR_RENTAL_COMPANY_CAR 테이블에서 '네비게이션' 옵션이 포함된 자동차 리스트를 출력하는 SQL문을 작성해주세요. 결과는 자동차 ID를 기준으로 내림차순 정렬해주세요.
``` mysql
SELECT CAR_ID, CAR_TYPE, DAILY_FEE, OPTIONS
FROM CAR_RENTAL_COMPANY_CAR 
WHERE OPTIONS LIKE "%네비게이션%"
ORDER BY CAR_ID DESC;
```

### 조건에 부합하는 중고거래 댓글 조회하기
USED_GOODS_BOARD와 USED_GOODS_REPLY 테이블에서 2022년 10월에 작성된 게시글 제목, 게시글 ID, 댓글 ID, 댓글 작성자 ID, 댓글 내용, 댓글 작성일을 조회하는 SQL문을 작성해주세요. 결과는 댓글 작성일을 기준으로 오름차순 정렬해주시고, 댓글 작성일이 같다면 게시글 제목을 기준으로 오름차순 정렬해주세요.
``` mysql
SELECT TITLE, B.BOARD_ID, REPLY_ID, R.WRITER_ID, R.CONTENTS, DATE_FORMAT(R.CREATED_DATE, "%Y-%m-%d") AS "CREATED_DATE"
FROM USED_GOODS_BOARD B
    JOIN USED_GOODS_REPLY R
    ON B.BOARD_ID = R.BOARD_ID
WHERE YEAR(B.CREATED_DATE) = 2022 AND MONTH(B.CREATED_DATE) = 10 # 또는 B.CREATED_DATE LIKE "2022-10%"
ORDER BY R.CREATED_DATE, TITLE;
```