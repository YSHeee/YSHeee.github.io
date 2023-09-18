# Basic

## Data Types
### Primitive type
- 숫자 number `var num = 10;`
- 문자열 string `"string";`, `'string';`
- 논리값 boolean
- undefined : 초기화되지 않은 변수나 존재하지 않는 값에 접근할 때 반환
    - null : null은 object 타입이자 아직 **'값'**이 정해지지 않은 것
    - undefined : **'타입'**이 정해지지 않은 것
    - `null==undefined;` : true, `null===undefined;` : false
- 심볼 symbol (ECMAscript6~)
``` javascript
var sym = Symbol("javascript");  // symbol 타입
var symObj = Object(sym);        // object 타입
```

### Object type
- `var`

``` javascript
<script>
    var v1;
    document.write("<li>"+ typeof v1 +"</li>"); //undefined
	document.write("<li>"+ (v1+10) +"</li>"); //NaN (Not a Number)

    v1 = true;
	document.write("<li>"+ typeof v1 +"</li>"); //boolean
	document.write("<li>"+ (v1+10) +"</li>"); //11

    document.write("<h2>"+ typeof 100 +"</h2>"); //number
    document.write("<h2>"+ typeof 3.14 +"</h2>"); //number
    document.write("<h2>"+ typeof '가' +"</h2>"); //string
    document.write("<h2>"+ typeof "abc" +"</h2>"); //string
    document.write("<h2>"+ typeof '100' +"</h2>"); //string
    document.write("<h2>"+ typeof true +"</h2>"); //boolean
    document.write("<h2>"+ typeof undefined +"</h2>"); //undefined
    document.write("<h2>"+ typeof null +"</h2>"); //object
    document.write("<h2>"+ typeof function() {} +"</h2>"); //function
    document.write("<h2>"+ typeof {} +"</h2>"); //object
    document.write("<h2>"+ typeof [] +"</h2>"); //object

    console.log("자바스크립트"*10); // Nan 
    console.log(true == 1); // true
</script>
```

## Type conversion 타입 변환
: JS의 변수는 타입이 정해져 있지 않으며, 같은 변수에 다른 타입의 값을 다시 대입할 수도 있다

### 묵시적 타입 변환 Implicit type conversion
: 특정 타입의 값을 기대하는 곳에 다른 타입의 값이 오면, 자동으로 타입 변환
``` javascript
10 + "문자열"; // 문자열 연결을 위해 숫자 10이 문자열로 변환됨.
"3" * "5";     // 곱셈 연산을 위해 두 문자열이 모두 숫자로 변환됨.
1 - "문자열";  // NaN (해당 문자열은 숫자로 변경할 수 없는 문자열이므로)
```

### 명시적 타입 변환 Explicit type conversion

- Number()
- String()
- Boolean()
- Object()
- parseInt()
- parseFloat()
- ...

#### 숫자 -> 문자열
- String()
- toString() : null과 undefined를 제외한 모든 타입이 갖고 있는 메소드
- 숫자 객체가 제공하는 숫자->문자열 메소드
    - toExponential() : 정수는 1자리, 소수는 입력받은 수만큼 e표기법을 사용하여 숫자를 문자열로 변환
    - toFixed() : 소수 부분을 입력받은 수만큼 사용하여 변환
    - toPrecision() : 입력받은 수만큼 유효 자릿수를 사용하여 변환

#### 문자열 -> 숫자
- Number()
    - `Number("123")` : 123
    - `Number("3.14")` : 3.14
- parseInt() : 문자열을 파싱하여 특정 진법의 정수 반환 :star:
    - `parseInt("123")` : 123
    - `parseInt("3.14")` : 3
    - `parseInt("100원")` : 100
- parseFloat() : 문자열을 파싱하여 부동 소수점 수 반환

#### 날짜 -> 문자열, 숫자
|   메소드    |    설명    |
| :--------:  | :--------: |
|  getDate()  | 날짜 중 일자를 숫자로 반환 (1~31) |
|  getDay()   | 날짜 중 요일을 숫자로 반환 (일요일:0 ~ 토요일: 6) |
| getFullYear() | 날짜 중 연도를 4자리 숫자로 반환 (yyyy년) |
| getMonth()  | 날짜 중 월을 숫자로 반환 (1월:0 ~ 12월: 11)
|  getTime()  | 1970년 1월 1일부터 현재까지의 시간을 밀리초 단위 숫자로 반환|
|  getHours() | 시간 중 시를 숫자로 반환 (0~23) |
| getMinutes() | 시간 중 분을 숫자로 반환 (0~59) |  
| getMilliseconds() | 시간 중 초를 밀리초 단위 숫자로 반환 (0~999) |

#### Boolean -> 문자열
- `String(true);` : 문자열 "true"로 변환
- `false.toString();` : 문자열 "false"로 변환

#### Boolean -> 숫자
- `Number(true);` : 숫자 1
- `Number(false);` : 숫자 0

---
## 연산자 

#### [연산자 우선순위](https://www.tcpschool.com/javascript/js_operator_arithmetic)

#### 수치연산자
- 덧셈 `+` : 하나라도 문자열이면 문자열 결합 연산 
- 뺄셈 `-` : 숫자 아닌 경우 숫자로 변경해서 연산. 불가시에는 Nan
- 곱셈 `*` : 숫자 아닌 경우 숫자로 변경해서 연산. 불가시에는 Nan
- 나눗셈 `/` : 숫자 아닌 경우 숫자로 변경해서 연산. 불가시에는 Nan
- 나머지 `%` : 숫자 아닌 경우 숫자로 변경해서 연산. 불가시에는 Nan
- 증감 연산자 `++`, `--`
- 단항 연산자 `-`

#### 문자열 연산
: 문자열을 합하여 하나의 문자열 생성
``` javascript
str = "ABCD" + "1234"; // ABCD1234
```

#### 비교 연산자
- `<`, `>`, `<=`, `>=`
- 동등연산자 `==` : 값이 같을 때
- `!=`
- 일치연산자 `===` : 타입도 같고, 값도 같을 때
- `!==`
``` javascript
"123" == 123 //true
1 == true // true

"123" === 123 // false, ===은 타입 먼저 체크
1 === true // false
```

#### 논리 연산자
- AND 연산자 `&&`
    - 조건식&&일반식 : 조건식이 참이면, 일반식 실행
    - Ex: `num % 2 == 0 && document.writeln(num+"는 짝수");`
- OR 연산자 `||`
- NOT 연산자 `!`
- `?` 연산자

|  A  |  B  | A && B | A ㅣㅣ B | !A |
|:---:|:---:|:------:|:------:|:--:|
| true | true | true | true | false |
| true | false | false | true | false |
| false | true | false | true | true |
| false | true | false | true | true |

#### 대입 연산자
- `=`, `+=`, `-=`, `*=`, `/=`, `%=`

#### 비트 연산자
: 비트 단위의 논리 연산

- AND `&` : 대응되는 비트가 모두 1이면 1반환
- OR `|` : 대응되는 비트가 하나라도 1이면 1반환
- XOR `^` : 대응되는 비트가 서로 다르면 1 반환
- NOT `~` : 비트를 1이면 0, 0이면 1로 반전 
- 비트 좌우 이동 `<<`, `>>` : left shift, right shift
- `>>>` : 지정한 수만큼 비트를 모두 오른쪽으로 이동시키며, 새로운 비트는 전부 0

#### 타입 점검 & 삭제 연산자
- **typeof** : 피연산자의 타입 반환
- instanceof : 객체가 특정 객체의 인스턴스인지 아닌지 반환
- **delete** 
    - 객체, 객체의 property, 배열의 요소 등을 삭제
    - 성공적으로 삭제되었을 경우 true 반환, 못했을 경우 false 반환

#### 삼항 연산자 Ternary operator
``` javascript
표현식 ? 반환값1 : 반환값2
```

#### 쉼표 연산자
: 쉼표 연산자를 for문에서 사용하면 루프마다 여러 변수를 동시에 갱신할 수 있음
``` javascript
// 루프마다 i의 값은 1씩 증가하고, 동시에 j의 값은 1씩 감소함.
for (var i = 0, j = 9; i <= j; i++, j--) {
    document.write("i의 값은 " + i + "이고, j의 값은 " + j + "입니다.<br>");}
```

---
## Control flow statements 제어문

### 조건문 Conditional Statements
- if
- if-else
- if-else if-else
- switch

### 반복문 Iteration Statements
- while
- do-while
- for
- for-in
- for-of
- break/continue


### label
: 프로그램 내의 특정 영역을 식별할 수 있도록 해주는 식별자
<br> continue/break문의 동작이 프로그램의 흐름을 특정 영역으로 이동시킬 수 있다

```javascript
label:
    식별하고자 하는 특정 영역

// Example
arrIndex:
for (var i in arr) {
    console.log(i);}
```

---
!!! quote
    - [TCP School](https://www.tcpschool.com/javascript/intro)