# Standard Object

: Javascript 언어 자체에 정의되어 있는 객체

- Object : 최상의 객체로서 JavaScript의 모든 객체들은 이 객체를 상속
- Number : 수치값에 대한 Wrapper 객체
- String : 문자열 데이터에 대한 Wrapper 객체
- Boolean : 논리값에 대한 Wrapper 객체
- Array : 배열 정의시 생성되는 객체
- Math : : 다양한 수학 함수 기능을 제공하는 객체
- Date : 날짜와 시간 정보 추출과 설정 관련 기능을 제공하는 객체
- Error : 런타임 오류가 발생할 때마다 Error 객체의 인스턴스가 생성되어 해당 오류의 정보 저장 `throw new Error();`
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
: 숫자 값을 감싸고 있는 wrapper 객체 생성
``` javascript
var x = 100; // object type
var y = new Number(100); // number type
x==y; // true
x===y; // false : 숫자 리터럴과 Number 객체의 타입이 다르므로 false 반환
```

#### 64비트 부동 소수점 수 

JS는 정수와 실수를 따로 구분하지 않고, 모든 수를 실수 하나로만 표현한다
<br>-> 모든 숫자는 IEEE 754 국제 표준에서 정의한 **64비트 부동소수점** 수로 저장된다

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

#### NaN
: Not A Number, 숫자가 아니라는 뜻으로 정의되지 않거나 표현할 수 없는 값

``` javascript
NaN == NaN; // false
NaN === NaN; //false
Object.is(NaN, NaN) //true
isNaN(NaN) //true
```

- null : object 타입, 아직 **값**이 정해지지 않았음을 의미
- undefined : 하나의 독립적인 타입, **타입**이 정해지지 않았음을 의미
- NaN : number 타입, **숫자가 아님**을 의미
- Infinity: number 타입, **무한대** 의미

|  값  |  Boolean 문맥 |  Number 문맥  |  String 문맥  |
| :-------: | :---: | :------: | :-------: |
|    null   | false |     0    | "null" |
| undefined | false |    NaN   | "Infinity" |
|    NaN    | false |    NaN   | "NaN" |
|  Infinity |  true | Infinity | "Infinity" |


#### Number Method

- Number.parseFloat() : 문자열을 파싱하여 숫자 부분을 실수 형태로 반환
``` javascript
Number.parseFloat("12.34"); // 12.34
Number.parseFloat("12문자열"); // 12
Number.parseFloat("12 34 56"); // 12
Number.parseFloat("문자열 56"); // NaN
```
- Number.parseInt() : 문자열을 파싱하여 숫자 부분을 정수 형태로 반환
``` javascript
Number.parseFloat("12.34"); // 12
Number.parseFloat("12문자열"); // 12
Number.parseFloat("12 34 56"); // 12
Number.parseFloat("문자열 56"); // NaN
```
- Number.isNaN() : **isNaN() 함수와 달리** 오직 숫자인 값에서만 동작하며 그 값이 NaN인 경우에만 true 반환
``` javascript
isNaN(NaN); // true
isNaN("NaN"); // true
isNaN(undefined); // true
isNaN("문자열"); // true

isNaN(null); // false
Number.isNaN(null); // false

Number.isNaN(NaN); // true
Number.isNaN("NaN"); // false
Number.isNaN(undefined); // false
Number.isNaN("문자열");  // false
```
- Number.isFinite() : 유한한 수인 경우 true, 아니면 false 반환 (강제 변환하지 않음)
``` javascript
Number.isFinite(0); // true
Number.isFinite(Infinity); // false
Number.isFinite(NaN); // false

isFinite("0"); // true
isFinite(null); // true

Number.isFinite("0"); // false
Number.isFinite(null); // false
```
- Number.isInteger() : 정수이면 true, 아니면 false 반환
``` javascript
Number.isInteger(0); // true

Number.isInteger(0.1); // false
Number.isInteger(NaN); // false
Number.isInteger(true); //false
Number.isInteger(Infinity); // false
```
- Number.isSafeInteger() : 안전한 정수인지 아닌지 검사
``` javascript
Number.isSafeInteger(10); // true
Number.isSafeInteger(Math.pow(2, 53) - 1); // true
Number.isSafeInteger(Math.pow(2, 53));// false
Number.isSafeInteger(Infinity); // false
```

---
#### Number.prototype Method

- Number.prototype.toExponential() : 지수표기법으로 변환한 후 문자열 반환
``` javascript
var num = 12.3456;

num.toExponential(); // 1.23456e+1
num.toExponential(2); // 1.23e+1
num.toExponential(4); // 1.2346e+1
12.3456.toExponential(); // 1.23456e+1
```
- Number.prototype.toFixed() : 소수 부분 자릿수를 고정한 후, 문자열 반환
``` javascript
var num = 12.3456;

num.toFixed(); // 12
num.toFixed(2); // 12.34
num.toFixed(4); // 12.3456
12.3456.toExponential(4); // 12.3456
```
- Number.prototype.toPrecision() : 가수+소수의 자릿수를 고정한 후, 문자열 반환
``` javascript
var num = 3.14159265;

num.toPrecision(); // 3.14159265
num.toPrecision(2); // 3.1
num.toPrecision(4); // 3.142
3.14159265.toPrecision(4); // 3.14159
```
- Number.prototype.toString() : 해당 진법으로 변환 후 문자열 반환
``` javascript
var num = 25;

num.toString(); // 255
num.toString(2); // 11111111
(255).toString(); // 255
(100).toString(16); //64
```
- Number.prototype.valueOf() : Number 인스턴스가 가지고 있는 값 반환
``` javascript
var numObj = new Number(123)

typeof numObj; //object
var num = numObj.valueOf();
num; // 123
typeof num; // number
```

---
## Math
: 수학 함수 기능을 제공하는 JS 표준 내장 객체
<br> 생성자가 존재하지 않아 인스턴스를 생성하지 않아도 바로 method나 property 사용 가능

#### Method

|        Method     |       설명       |      Example     |
|   :------------:  |   :-----------:  |   :-----------:  | 
|Math.min(x, y, ...)| 인수 값 중 가장 작은 수 반환 |     0    |
|Math.max(x, y, ...)| 인수 값 중 가장 큰 수 반환 |    NaN   |
|   Math.random()   | 0<=난수<1 반환 |    NaN   | 
|   Math.round(x)   | x를 소수점 첫 번째 자리에서 반올림 | Infinity |
|   Math.floor(x)   | x와 같거나 작은 수 중 가장 큰 정수 반환|
|   Math.ceil(x)    | x와 같거나 큰 수 중 가장 큰 정수 반환 |
|   Math.abs(x)     | x의 절댓값 반환 |
|   Math.cbrt(x)    | x의 세제곱근 반환 |
|   Math.sqrt(x)    | x의 제곱근 반환 |
|   Math.clz32(x)   | x를 32비트 이진수로 변환한 후 0이 아닌 비트의 개수 반환|
|   Math.exp(x)	    | e^x 값 반환 (e : 오일러의 수) |
|   Math.expm1(x)   | 1 - e^x 값 반환 |
|   Math.fround(x)	| x와 가장 근접한 32비트 부동 소수점 수 반환 |
|Math.hypot(x, y, ...)| 인수 값들을 각각 제곱한 후 더한 총합의 제곱근 반환 |
|   Math.imul(x, y) | 두 값의 32비트 곱셈의 결과를 반환
|   Math.log(x)     | x의 자연로그 값 반환 (ln x) |
|   Math.log1p(x)   | ln(1 + x)의 값을 반환 |
|   Math.log10(x)	| x의 10을 밑으로 가지는 로그 값 반환 |
|   Math.log2(x)    | x의 2를 밑으로 가지는 로그 값 반환 |
|   Math.pow(x, y)	| x^y 반환 | 
|   Math.sign(x)    | x의 부호 값 반환 |
|   Math.trunc(x)   | x의 모든 소수 부분을 삭제하고 정수 부분만 반환 |
| Math.sin(x) <br>  Math.cos(x) <br>  Math.tan(x) <br> Math.asin(x) <br> Math.acos(x) <br> Math.atan(x) <br> Math.asinh(x) <br> Math.acosh(x) <br> Math.atanh(x) <br>  Math.atan2(x) | x의 해당 삼각 함수값 반환 | 


#### Property

|    Property   |       설명       |      대략값     |
|  :----------: |   :-----------:  |   :-----------:  | 
|   Math.E      | 오일러의 수라고 불리며, 자연로그의 밑 값 | 2.718  |
|   Math.LN2    | 2의 자연로그 값   | 0.693 |
|   Math.LN10   | 10의 자연로그 값  | 2.303 |
|   Math.LOG2E  | 오일러 수(e)의 밑 값이 2인 로그 값    | 1.443 |
|   Math.LOG10E | 오일러 수(e)의 밑 값이 10인 로그 값   | 0.434 |
|   Math.PI	    | 원의 원주를 지름으로 나눈 비율(원주율) 값| 3.14159 |
|   Math.SQRT1_2| 2의 제곱근의 역수 값  | 0.707 |
|   Math.SQRT2  | 2의 제곱근 값 | 1.414 |


---
## Date 

- 연도(year) : 1900년(00) ~ 1999년(99)
- **월(month)** : 1월(**0**) ~ 12월(**11**) 
- 일(day) : 1일(1) ~ 31일(31)
- 시(hours) : 0시(0) ~ 23시(23)
- 분(minutes) : 0분(0) ~ 59분(59)
- 초(seconds) : 0초(0) ~ 59초(59)

#### 날짜 양식 Date format

- ISO 날짜 양식
    - ISO 8601 : 날짜와 시간을 나타내는 국제 표준 양식
    - YYYY-MM-DDTHH:MM:SS (T는 UTC를 나타내는 문자, 시간까지 표현할 때에는 반드시 사용)
    - YYYY-MM-DD
``` javascript
new Date("1977-12-14T13:30:00");
new Date("1977-12-14");        
```
- Long 날짜 양식
    - MMM DD YYYY
    - DD MMM YYYY
``` javascript
new Date("Feb 19 1982");
new Date("19 Feb 1982");  
new Date("February 19 1982"); 
new Date("FEBRUARY, 19, 1982"); 
```
- Short 날짜 양식 
    - MM/DD/YYYY
    - YYYY/MM/DD
``` javascript
new Date("02/19/1982"); 
new Date("1982/02/19");
```
- Full 날짜 양식
``` javascript
// GMT가 현재 국가와 다른 시간은 현재 국가의 GMT로 변환되어 표현됨
new Date("Wed May 25 2016 17:00:00 GMT+0900 (Seoul Time)");
new Date("Wed May 25 2016 17:00:00 GMT-0500 (New York Time)");
```

#### getter Method

|   Method    |    설명    | 
| :--------:  | :--------: |
|  getDate()  | 날짜 중 일자를 숫자로 반환 (1~31) |
|  getDay()   | 날짜 중 요일을 숫자로 반환 (일요일:0 ~ 토요일: 6) |
| getMonth()  | 날짜 중 월을 숫자로 반환 (1월:0 ~ 12월: 11)
| getFullYear() | 날짜 중 연도를 4자리 숫자로 반환 (yyyy) |
|  getHours() | 시간 중 시를 숫자로 반환 (0~23) |
| getMinutes() | 시간 중 분을 숫자로 반환 (0~59) |  
| getMilliseconds() | 시간 중 초를 밀리초 단위 숫자로 반환 (0~999) |
|  getTime()  | 1970년 1월 1일부터 현재까지의 시간을 밀리초 단위 숫자로 반환|
| getTimezoneOffset()| UTC로부터 현재 시각까지의 시간차를 분 단위로 환산한 값을 숫자로 반환 |
| toLocaleString() | `2023. 9. 19. 오전 10:35:58` 형태로 반환 |

#### UTC getter Method

|   Method    |    설명    | 
| :--------:  | :--------: |
|  getUTCDate()  | 협정세계시(UTC)로 현재 일자에 해당하는 숫자 반환 |
|  getUTCDay()   | 협정세계시(UTC)로 현재 요일에 해당하는 숫자 반환 |
| getUTCMonth()  | 협정세계시(UTC)로 현재 월에 해당하는 숫자 반환
| getUTCFullYear() | 협정세계시(UTC)로 현재 연도를 4자리 숫자로 반환 (yyyy) |
|  getUTCHours() | 협정세계시(UTC)로 현재 시각에 해당하는 숫자 반환 |
| getUTCMinutes() | 협정세계시(UTC)로 현재 시각의 분에 해당하는 숫자 반환 |  
|  getUTCSeconds() | 협정세계시(UTC)로 현재 시각의 초에 해당하는 숫자 반환 |
| getUTCMilliseconds() | 협정세계시(UTC)로 현재 시각의 밀리초에 해당하는 숫자 반환 |

#### UTC setter Method

|   Method    |    설명    | 
| :--------:  | :--------: |
|  setDate()  | 특정 일자 설정 (1~31) |
| setMonth()  | 특정 월 설정 (1월:0 ~ 12월: 11)
| setFullYear() | 특정 연도/월/일자 설정 (yyyy, mm, dd) |
|  setHours() | 특정 시간 설정 (0~23) |
| setMinutes() | 특정 분 설정 (0~59) |  
| setMilliseconds() | 특정 밀리초 설정 (0~999) |
|  setSeconds() | 특정 초 설정 (0~59) |
| setTime() | 1970년 1월 1일 0시 0분 0초부터 밀리초 단위로 표현되는 특정 시간 설정 |

#### UTC setter Method

|   Method    |    설명    | 
| :--------:  | :--------: |
|  setUTCDate()  | 협정세계시(UTC)로 특정 일자 설정 (1~31) |
| setUTCMonth()  | 협정세계시(UTC)로 특정 월 설정 (1월:0 ~ 12월: 11) |
| setUTCFullYear() | 협정세계시(UTC)로 특정 연도/월/일자 설정 (yyyy, mm, dd) |
|  setUTCHours() | 협정세계시(UTC)로 특정 시간 설정 (0~23) |
| setUTCMinutes() | 협정세계시(UTC)로 특정 분 설정 (0~59) |  
|  setUTCSeconds() | 협정세계시(UTC)로 특정 초 설정 (0~59) |
| setUTCMilliseconds() | 협정세계시(UTC)로 특정 밀리초 설정 (0~999) |

---
## String  
: 문자열 값을 감싸는 wrapper 객체 생성

``` javascript
var strObj = new String("한글");

// 문자열 길이
strObj.length; // 2

// 긴 문자열 리터럴 나누어 표현하기
document.write("첫번째 문자열 \
두번째 문자열");
document.write("첫번째 문자열" +
"두번째 문자열");
```

#### Escape Sequence 

- 16진수 이스케이프 시퀀스 `\x`
- 유니코드 이스케이프 시퀀스 `\u`
- 유니코드 코드 포인트 이스케이프 `String.fromCodePoint(0x00A2)`

#### Method

|   Method    |    설명    | 
| :--------:  | :--------: |
|  String.fromCharCode()  | 유니코드에 해당하는 문자들의 문자열 반환 |
| String.fromCodePoint()  | 코드포인트에 해당하는 문자들의 문자열 반환 |
| String.raw() | 템플릿 문자열의 원형 반환 | 

#### String.prototype Method
: :heart_exclamation: String은 Immutable하므로 모든 String method는 새로운 문자열을 생성하여 결과를 반환한다 

|   Method    |    설명    | 
| :--------:  | :--------: | 
|  indexOf()    | 특정 문자나 문자열이 처음으로 등장하는 위치의 인덱스 반환 |
| lastIndexOf() | 특정 문자나 문자열이 마지막으로 등장하는 위치의 인덱스 반환|
| charAt()      | 해당 인덱스에 위치한 문자 반환 | 
| charCodeAt()  | 해당 인덱스에 위치한 문자의 UTF-16 코드를 반환 (0~65535) |
| charPointAt() | 해당 인덱스에 위치한 문자의 유니코드 코드 포인트 반환 |
| slice(s, e)   | start ~ end-1 까지 문자열 추출하여 새 문자열 반환 |
| substring(s, e)| start ~ end-1 까지 문자열 추출하여 새 문자열 반환 |
| substr(s, length)| 시작인덱스부터 length만큼 추출하여 새 문자열 반환 |
| split()       | 구분자를 기준으로 나눈 후, 나뉜 문자열을 하나의 배열로 반환 |
| concat()      | 전달받은 문자열을 결합한 새로운 문자열 반환 |
| toUpperCase() | 모든 문자를 대문자로 변환한 새로운 문자열 반환 |
| toLowerCase() | 모든 문자를 소문자로 변환한 새로운 문자열 반환 |
| trim()        | 양 끝의 공백과 모든 줄 바꿈 문자를 제거한 새로운 문자열 반환 |
| replace()     | 패턴에 맞는 문자열을 대체 문자열로 변환한 새 문자열 반환 | 
| includes()    | 문자/문자열이 포함되어 있는지를 불리언 값으로 반환 | 
| startsWith()  | 전달받은 문자/문자열로 시작되는지를 불리언 값으로 반환 |
| endsWith()    | 전달받은 문자/문자열로 끝나는지를 불리언 값으로 반환
| toLocaleUpperCase()| 모든 언어의 문자를 대문자로 변환한 새로운 문자열 반환 |
| toLocaleLowerCase() | 모든 언어의 문자를 소문자로 변환한 새로운 문자열 반환
| localeCompare()    | 문자열과 정렬 순서로 비교하여 그 결과를 정수 값으로 반환 |
| normalize()        | 문자열의 유니코드 표준화 양식 반환 |
| repeat() |문자열을 인수로 전달받은 횟수만큼 반복하여 결합한 새로운 문자열 반환 |
| toString()    | String 인스턴스의 값을 문자열로 반환 |
| valueOf()     | String 인스턴스의 값을 문자열로 반환 |
| | | 
| search()  | 정규 표현식에 맞는 문자나 문자열이 처음으로 등장하는 위치의 인덱스 반환 |
| match()   | 정규 표현식에 맞는 문자열을 찾아서 하나의 배열로 반환 |


substring() vs slice() 

- start > end인 경우
    - substring() : start값과 end값을 바꾸어서 처리
    - slice() : 비어있는 String `""` 리턴
- start 또는 end 값이 음수인 경우 (-2, 6)
    - substring() : 음수인 경우 0 변경해서 처리
    - slice() : 문자열의 음수 인덱스에 위치한 문자의 index로 변경해서 처리
- start 또는 end 값이 음수이고, 음수의 절댓값이 전체 string 길이보다 클때
    - slice() : 0으로 변경해서 처리

---
## Array
: 배열, 정렬된 값들의 집합

#### Method

|   Method    |    설명    | 
| :--------:  | :--------: | 
| Array.isArray()| 전달된 값이 Array 객체인지 아닌지 검사 |
| Array.from()   | 배열과 비슷한 객체/반복할 수 있는 객체를 배열처럼 변환 <br> Array 객체의 자식 클래스로 생성 |
| Array.of()     | 인수로 전달받은 값을 가지고 새로운 Array 인스턴스를 생성 |

- 배열과 비슷한 객체(array-like objects) : length 프로퍼티와 인덱스 된 요소를 가지고 있는 객체
- 반복할 수 있는 객체(iterable objects) : Map과 Set 객체 및 문자열과 같이 해당 요소를 개별적으로 선택할 수 있는 객체

#### Array.prototype Method

|   Method    |    설명    | 
| :--------:  | :--------: | 
| 원본 배열 변경 | |
| push()    | 요소를 배열의 마지막에 추가하고, 배열의 총 길이 반환 <br> Stack, Queue |
| pop()     | 배열의 가장 마지막 요소를 제거하고, 그 제거된 요소 반환 <br> Stack |
| shift()   | 배열의 가장 첫 요소를 제거하고, 그 제거된 요소 반환 <br> Queue |
| unshift() | 하나 이상의 요소를 배열의 가장 앞에 추가하고, 배열의 총 길이 반환 |
| reverse() | 배열 요소의 순서를 전부 반대로 교체 |
| sort() | 해당 배열의 배열 요소들을 알파벳 순서에 따라 정렬 <br> 숫자는 따로 별도의 함수 필요|
| splice()  | (새 요소가 삽입될 위치, 제거할 요소의 개수) <br> 배열의 내용을 변경하고, 제거된 요소를 배열의 형태로 반환, 아무 요소도 제거되지 않았으면 빈 배열 반환 |
| fill()    | start부터 end-1까지의 모든 배열 요소를 특정 값으로 교체 |
| copyWithin()| 배열에서 일련의 요소들을 복사하여, 명시된 위치의 요소들을 교체 |
| 원본 배열은 두고, 참조만 함 | |
| join(구분자)    | 배열의 모든 요소를 하나의 문자열로 반환 |
| slice()   | start ~ end-1 까지 모든 배열 요소 추출하여 새로운 배열 반환 |
| concat()  | 해당 배열의 뒤에 인수로 전달받은 배열을 합쳐서 만든 새로운 배열 반환 |
| toString()| 해당 배열의 모든 요소를 하나의 문자열로 반환 |
| toLocaleString() | 해당 배열의 모든 요소를 하나의 문자열로 반환 |
| indexOf() | 전달받은 값과 동일한 배열 요소가 처음으로 등장하는 위치의 인덱스 반환 |
|lastIndexOf()| 전달받은 값과 동일한 배열 요소가 마지막으로 등장하는 위치의 인덱스 반환 |
| 원본 배열은 두고, 반복 참조 | |
| forEach(func) | 배열의 모든 요소에 대하여 반복적으로 명시된 콜백 함수를 실행
| map(func)     | 배열의 모든 요소에 대하여 반복적으로 명시된 콜백 함수를 실행한 후, 그 실행 결과를 새로운 배열로 반환 |
| filter(func)  | 해당 배열의 모든 요소에 대하여 반복적으로 명시된 콜백 함수를 실행한 후, 그 결과가 true인 요소들만을 새로운 배열에 담아 반환 |
| every(func)   | 해당 배열의 모든 요소에 대하여 반복적으로 명시된 콜백 함수를 실행한 후, 그 결과가 모두 true일 때에만 true 반환 |
| some(func)    | 해당 배열의 모든 요소에 대하여 반복적으로 명시된 콜백 함수를 실행한 후, 그 결과가 하나라도 true이면 true를 반환 |
| reduce(func)  | 해당 배열의 모든 요소에 대한 연산, 두 개의 인수를 전달받는 콜백 함수 실행 <br> 배열의 첫번째 요소부터 시작 |
| reduceRight(func)| 해당 배열의 모든 요소에 대한 연산, 두 개의 인수를 전달받는 콜백 함수 실행 <br> 배열의 마지막 요소부터 시작 |
| entries() | 배열 요소별로 키와 값의 한 쌍으로 이루어진 새로운 배열 반복자 객체(Array Iterator Object)를 배열 형태로 반환 |
| keys()    | 배열 요소별로 key만 포함하는 새로운 배열 반복자 객체를 배열 형태로 반환 |
| values()  | 배열 요소별로 value만 포함하는 새로운 배열 반복자 객체를 배열 형태로 반환 |
| find()    | 검사를 위해 전달받은 함수를 만족하는 배열 요소의 값을 반환함. 만족하는 값이 없으면 undefined를 반환 |
| findIndex()| 검사를 위해 전달받은 함수를 만족하는 배열 요소의 인덱스를 반환함. 만족하는 값이 없으면 -1 반환 |


---
!!! quote
    - [TCP School](https://www.tcpschool.com/javascript/intro)