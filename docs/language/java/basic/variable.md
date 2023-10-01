# 변수 variable
: 데이터를 저장하기 위해서 프로그램에 의해 이름을 할당받은 메모리 공간
<br>저장된 값은 변경이 가능하다


### 변수명 생성 규칙

- *Camel 스타일로 작성한다 `mathScore`
- *변수가 어떤 값을 저장하고 있는지 쉽게 알 수 있도록 의미있게 작성
- 영문자(대소문자), 숫자, 언더스코어`_`, 달러`$`로만 구성
- 숫자로 시작할 수 없음
- 공백을 포함할 수 없음
- 자바에서 미리 정의된 키워드(keyword) 사용할 수 없음

### 종류
- 기본형(Primitive) 변수 (실제 값 저장): byte, short, int, long, float, double, boolean, char
- 참조형(Reference) 변수 (객체의 주소 저장): String, Arrays, Classes

### 변수 선언
- 변수를 선언하여 메모리 공간을 할당받고, 나중에 변수 초기화
``` java
int num;                 // 변수의 선언
System.out.println(num); // 오류 발생

num = 20; // 변수의 초기화
System.out.println(num); // 20
```

- 변수의 선언과 동시에 초기화
``` java
int num1, num2;                  // 같은 타입의 변수를 동시에 선언함.
double num3 = 3.14;              // 선언과 동시에 초기화함.
double num4 = 1.23, num5 = 4.56; // 같은 타입의 변수를 동시에 선언하면서 초기화함.
```

### 변수 타입
- 지역 변수 (Local Variables) : 메서드 블럭안에서 선언된 변수
- 인스턴스 변수 (Instance Variables) : Non-static, 
- 클래스 변수 (Static Variables) : 

### 변수 사용 범위
: if, for, while 등 중괄호 `{}`블록 내에서 선언된 변수는 블록 밖에서는 사용할 수 없다

---

## 상수 Constant
: 메모리에 저장된 데이터를 변경할 수 없는, 데이터를 저장할 수 있는 메모리 공간

- `final int AGES = 30;` 
    - final 키워드 사용 
    - 일반적으로 모두 대문자를 사용하여 선언
    - 여러 단어로 이루어질 시  언더바`_`를 사용하여 구분

---

## 리터럴 Literal
: 변수/상수처럼 데이터가 저장된 메모리 공간이 아닌 값 그 자체를 의미

``` java
int var = 30;         // 30이 바로 리터럴임.
final int AGES = 100; // 100이 바로 리터럴임.
```

### 타입에 따른 리터럴
- 정수형 리터럴(Integer literals) : `123`, `-456` 같이 아라비아 숫자와 부호로 직접 표현
- 실수형 리터럴(floating-point literals) : `3.14`와 같이 소수 부분을 가지는 아라비아 숫자로 표현
- 논리형 리터럴(boolean literals) : `true`나 `false`로 표현
- 문자형 리터럴(character literals) : `'a'`, `'Z'`와 같이 작은따옴표(')로 감싸진 문자로 표현
- 문자열 리터럴(string literals) : `"Java"`와 같이 큰따옴표(")로 감싸진 문자열로 표현
- null 리터럴(null literals) : 아무런 값도 가지고 있지 않은 빈 값. `null`로 표현

### 리터럴 타입 접미사 (literal type suffix)
: 리터럴 뒤에 추가되어 해당 리터럴의 타입을 명시해주는 접미사

``` java
float var1 = 0.1234567890123456789f; // f로 명시해주지 않는다면, double로 인식
long var2 = 20L;
double var3 = 2e-3;
```

| 타입 접미사 | 리터럴 타입	 | 예제 |
| :--------: | :---------: | :--: |
| `L`, `l` | long형 | `123456789L`
| `F`, `f` | float형 | `1.234567F`, `8.9f`
| `D`, `d` (생략 가능) | double형 | `1.2345D`, `6.789d`

---

!!! quote
    - [Java의 정석](https://github.com/castello/javajungsuk_basic/tree/master)
    - [점프 투 자바](https://wikidocs.net/book/31)
    - [TCP school](http://www.tcpschool.com/java/intro)
    - 이것이 자바다 (저자: 신용권, 임경균 | 출판사: 한빛미디어)