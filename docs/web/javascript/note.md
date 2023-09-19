# Note


- NaN: Not a Number
    - `NaN == NaN;` : false
    - `NaN === NaN;` : false
    - `Object.is(NaN, NaN)` : true
    - `isNaN(NaN)` : true

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
!!! quote
    - [TCP School](https://www.tcpschool.com/javascript/intro)