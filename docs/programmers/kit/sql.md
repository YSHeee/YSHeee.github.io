# SQL 고득점 Kit

## 2024.03.01

### 3월에 태어난 여성 회원 목록 출력하기
MEMBER_PROFILE 테이블에서 생일이 3월인 여성 회원의 ID, 이름, 성별, 생년월일을 조회하는 SQL문을 작성해주세요. 이때 전화번호가 NULL인 경우는 출력대상에서 제외시켜 주시고, 결과는 회원ID를 기준으로 오름차순 정렬해주세요.

``` sql
SELECT MEMBER_ID, MEMBER_NAME, GENDER, DATE_FORMAT(DATE_OF_BIRTH, "%Y-%m-%d") AS DATE_OF_BIRTH
FROM MEMBER_PROFILE
WHERE TLNO IS NOT NULL AND GENDER = "W" AND MONTH(DATE_OF_BIRTH) = 03
ORDER BY MEMBER_ID
```


### 서울에 위치한 식당 목록 출력하기
REST_INFO와 REST_REVIEW 테이블에서 서울에 위치한 식당들의 식당 ID, 식당 이름, 음식 종류, 즐겨찾기수, 주소, 리뷰 평균 점수를 조회하는 SQL문을 작성해주세요. 이때 리뷰 평균점수는 소수점 세 번째 자리에서 반올림 해주시고 결과는 평균점수를 기준으로 내림차순 정렬해주시고, 평균점수가 같다면 즐겨찾기수를 기준으로 내림차순 정렬해주세요.

=== "MY CODE"
    ``` sql
    SELECT INFO.REST_ID, REST_NAME, FOOD_TYPE, FAVORITES, ADDRESS, ROUND(AVG(REVIEW.REVIEW_SCORE), 2) AS SCORE
    FROM REST_INFO INFO
        JOIN REST_REVIEW REVIEW
        ON INFO.REST_ID = REVIEW.REST_ID
    WHERE ADDRESS LIKE '서울%'
    GROUP BY INFO.REST_ID
    ORDER BY SCORE DESC, FAVORITES DESC;
    ```
=== "OTHERS 1"
    ``` sql
    SELECT REST_ID, REST_NAME, FOOD_TYPE, FAVORITES, ADDRESS, ROUND(AVG(REVIEW_SCORE),2) SCORE
    FROM REST_INFO JOIN REST_REVIEW USING(REST_ID)
    GROUP BY REST_NAME
    HAVING ADDRESS LIKE "서울%"
    ORDER BY SCORE DESC, FAVORITES DESC
    ```
=== "OTHERS 2"
    ``` sql
    SELECT REST_ID, REST_NAME, FOOD_TYPE, FAVORITES, ADDRESS, ROUND(AVG(REVIEW_SCORE), 2) SCORE
    FROM REST_INFO JOIN REST_REVIEW USING(REST_ID)
    WHERE ADDRESS LIKE '서울%'
    GROUP BY REST_ID
    ORDER BY SCORE DESC, FAVORITES DESC
    ```
=== "OTHERS 3"
    ``` sql
    SELECT i.REST_ID, REST_NAME, FOOD_TYPE, FAVORITES, ADDRESS, ROUND(AVG(REVIEW_SCORE),2) as SCORE
    FROM REST_INFO as i, REST_REVIEW as r
    WHERE i.REST_ID = r.REST_ID
    AND ADDRESS like "서울%"
    GROUP BY 1
    ORDER BY 6 desc, 4 desc
    ```

### Python 개발자 찾기
DEVELOPER_INFOS 테이블에서 Python 스킬을 가진 개발자의 정보를 조회하려 합니다. Python 스킬을 가진 개발자의 ID, 이메일, 이름, 성을 조회하는 SQL 문을 작성해 주세요. 결과는 ID를 기준으로 오름차순 정렬해 주세요.

``` sql
SELECT ID, EMAIL, FIRST_NAME, LAST_NAME
FROM DEVELOPER_INFOS
WHERE 'Python' IN (SKILL_1, SKILL_2, SKILL_3)
ORDER BY ID
```