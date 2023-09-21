# Note

1. eval() : 문자열로 표현된 JS 코드를 실행하는 함수
    ```javascript
    var a=1, b=2;
    eval("x+y"); //30
    ```
2. isFinite() : 값이 유한한 수인지 검사
    ```javascript
    isFinite(123); //true
    isFinite("123"); //true
    isFinite(""); //true
    isFinite(null); //true
    isFinite(undefined); //false
    isFinite(NaN); //false
    isFinite("문자열"); //false
    ```
3. isNaN() : NaN인지 판단함으로써 매개변수가 숫자인지 검사
    - 매개변수가 숫자이면 false, 숫자가 아니면 true 반환
    - null은 체크 불가
    - ECMAScript 6부터는 Number.isNaN() 메소드의 사용 권장<br>(Number.isNaN()은 문자열을 전달하면 false 반환)
    ```javascript
    if(isNaN(num) || num == '' || num == null );

    isNaN("문자열");  // true
    isNaN(undefined); // true
    isNaN(NaN);       // true

    isNaN(null); //false
    isNaN(0) ; // false
    isNaN(true) ; // false
    ```
4. encodeURI() : URI에서 주소를 표시하는 특수문자를 제외하고, 모든 문자를 이스케이프 시퀀스 처리하여 부호화
    - `encodeURI(부호화할 URI);`
5. encodeURIComponent() : encodeURI()에서 부호화하지 않은 모든 문자까지 포함하여 이스케이프 시퀀스 처리
    - `encodeURIComponent(부호화할 URI);`
6. decodeURI() : URI 해독
    - `decodeURI(해독할 URI);`
7. decodeURIComponent() : URI 컴포넌트 해독
    - `decodeURIComponent(해독할 URI);`
10. ~~escape()~~ : 전달값 중 특정 문자들을 16진법 이스케이프 시퀀스 문자로 변환
    - `escape("문자열");`
11. ~~unescape()~~ : 이스케이프 시퀀스 문자를 원래의 문자로 변환
    - `unescape(escape("문자열"));`

---
## Strict 모드
: ECMAScript5에서 소개된 모드. JS 코드에 더욱 엄격한 오류 검사 적용

``` javascript title="Example"
"use strict" // 전체 스크립트를 strict 모드로 설정함.

try {
    num = 3.14; // 선언되지 않은 변수를 사용했기 때문에 오류를 발생!
} catch (ex) {
    document.getElementById("text").innerHTML = ex.name + "<br>";
    document.getElementById("text").innerHTML += ex.message;
}
```

|  대상  |  제한 사항  |
| :-----:| :---------:|
| 변수 | 선언되지 않은 변수나 객체를 사용할 수 없음 <br> eval() 함수 내에서 선언된 변수는 외부에서 사용할 수 없음 |
| 프로퍼티 | 읽기 전용 프로퍼티에는 대입할 수 없음 <br> 한 프로퍼티를 여러 번 정의할 수 없음 |
| 함수 | 함수를 구문이나 블록 내에서 선언할 수 없음 |
| 매개변수 | 매개변수의 이름이 중복되어서는 안됨 <br> arguments 객체의 요소 값을 변경할 수 없음 |
| 문자열 | 문자열 "eval"과 "arguments"는 사용할 수 없음 | 
| 8진수 | 숫자 리터럴에 8진수 값을 대입할 수 없음 |
| this | this 포인터가 가르키는 값이 null이나 undefined인 경우 전역 객체로 변환되지 않음 |
| delete | delete 키워드를 사용할 수 없음 |
| with | with 문을 사용할 수 없음 |
| 예약어 | implements, interface, let, package, private, protected, public, static, yield 사용할 수 없음 |

--- 
## JSON + Javascript

- JSON.stringify(obj) : 자바스크립트 객체를 JSON 문자열로 변환 (UTF-16)
- JSON.parse(jsonStr) : JSON 문자열을 자바스크립트 객체로 변환
- toJSON() : JS의 Date 객체의 데이터를 JSON 형식의 문자열로 변환 <br> `YYYY-MM-DDTHH:mm:ss.sssZ`, `±YYYYYY-MM-DDTHH:mm:ss.sssZ`


---
!!! quote
    - [TCP School](https://www.tcpschool.com/javascript/intro)