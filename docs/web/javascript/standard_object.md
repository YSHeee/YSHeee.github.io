# Standard Object (Built-in Object)

: Javascript 언어 자체에 정의되어 있는 객체

- Object : 최상의 객체로서 JavaScript의 모든 객체들은 이 객체를 상속
- Number : 수치값에 대한 Wrapper 객체
- String : 문자열 데이터에 대한 Wrapper 객체
- Boolean : 논리값에 대한 Wrapper 객체
- Array : 배열 정의시 생성되는 객체
- Math : : 다양한 수학 함수 기능을 제공하는 객체
- Date : 날짜와 시간 정보 추출과 설정 관련 기능을 제공하는 객체
- Error : 
- Function : 함수 정의시 사용되는 객체
- RegExp: 정규표현식(패턴)을 이용하여 데이터를 처리하려는 경우 사용되는 객체

---
## global 전역 객체와 wrapper 래퍼 객체

- 전역 객체 : JS에 미리 정의된 객체로 전역 property나 전역 함수를 담는 공간의 역할
    - 전역 범위에서 this 연산자를 통해 접근
- 래퍼 객체: primitive type의 property에 접근할 때 생성되는 임시 객체
``` javascript
/* 문자열 리터럴 str은 객체가 아니지만, 
JS는 new String(str)을 호출한 것처럼 문자열 리터럴을 객체로 자동 변환한다
이때 생성된 임시 객체는 String 객체의 메서드를 상속받아 property를 참조하는 데 사용되고
이후 참조가 끝나면 자동으로 삭제된다 */
var str = "문자열";
var len = str.length; // 문자열 property인 length 사용
```

---
## Number

JS는 정수와 실수를 따로 구분하지 않고, 모든 수를 실수 하나로만 표현한다
<br>-> 모든 숫자는 IEEE 754 국제 표준에서 정의한 **64비트 부동소수점** 수로 저장된다

#### 64비트 부동 소수점 수 

|  0 ~ 51비트  |  52 ~ 62비트  |  63비트  |
| :---------: | :------------: | :------:|
| 총 52비트의 가수 부분 | 총 11비트의 지수 부분 | 총 1비트의 부호 부분

- 정밀도는 정수부 15자리, 소수부는 17자리까지만 유효
- 아래와 같은 오차를 없애기 위해 '정수로 변환 + 계산 수행 + 실수로 재변환' 과정을 거치기도 함
``` javascript
var z = 0.1 + 0.2 // 0.30000000000000004
```

#### 진법 표현
- JS는 산술 연산 시 모든 수가 10진수로 자동 변환되어 계산
- toString()을 통해 해당 숫자를 여러 진법의 형태로 변환하여 문자열로 반환
``` javascript
var x =  0xAB; // 16진법으로 표현된 10진수 171
var y = 29;   // 10진법으로 표현된 10진수 29
x + y; // 200 : 두 수 모두 10진법으로 자동 변환되어 계산됨

var num = 256;
num.toString(2);  // 100000000 : 2진법으로 변환
num.toString(8);  //  400 : 8진법으로 변환
num.toString(10); // 256 : 10진법으로 변환
num.toString(16); // 100 : 16진법으로 변환
(num.toString(2) / 2); // 50000000 : 문자열은 자동으로 10진수로 변환되어 산술 연산
```

#### Infinity
: 사용자가 임의로 수정할 수 없는 읽기 전용 값이자 JS내에서 어떤 수보다도 큰 수

- Infinity : 양의 무한대
- -Infinity : 음의 무한대

``` javascript
var x = 10 / 0; // Infinity 반환
var y = Infinity * 1000 // Infinity 반환
var z = 1 / Infinity // 0 : infinity의 역수는 0 반환
```

---
!!! quote
    - [TCP School](https://www.tcpschool.com/javascript/intro)