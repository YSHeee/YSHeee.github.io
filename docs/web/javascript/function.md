# Function
: 하나의 특별한 목적의 작업을 수행하도록 설계된 독립적인 블록

- JS에서는 Function도 하나의 타입으로 취급한다
    - 따라서 함수를 변수에 대입하거나 함수에 프로퍼티를 지정할 수 있다
- return문이 없을 때, 함수는 undifined를 반환한다
- 선언적(명시적) 함수 정의 : 위치 상관 없음
    ``` javascript
    function 함수이름(매개변수, 매개변수,...){
        실행문;
    }

    //Example
    var sum = sumNum(1,2); // 함수 sumNum에 인수 1,2를 전달하여 반환값을 sum에 대입
    document.write(sumNum(1,2)+"<br>");

    function sumNum(x,y){
        return x+y;
    };
    ```
- 표현식(익명) 함수 정의 방법 : 호출 전에 미리 선언되어있어야 함
    ``` javascript
    var myFunction = function(매개변수, ...){};

    //Example : return문이 없으므로 undifined 반환
    var msg = function(p,g){
        var text = p + "," + g;
        alert(text); // window.alert
    };
    msg("자바스크립트", "안녕!");
    ```

## 매개변수

- JS는 **인수의 개수와 매개변수의 개수가 일치하는 지 체크하지 않는다**
    - 매개변수에 인수를 전달하지 않으면, 매개변수의 값은 undefined가 된다
    - 전달된 인수를 모두 추출하려면 `arguments`를 사용한다
    ``` javascript
    function add(){
        var sum = 0; //전달받은 각각의 인수를 sum에 더함
        for (var i=0; i<arguments.length; i++){ 
            sum += arguments[i];
        }
        return sum;
    }
    ```
- 디폴트 매개변수 Default parameter : 함수 호출 시 명시된 인수를 전달하지 않았을 경우에 사용하게 될 기본값
    - JS의 디폴트 매개변수값은 undefined
    - 사파리, 오페라, 익스플로러에서 지원하지 않음
    ``` javascript
    function add(a, b=1){ // b의 default 값을 1로 변경
        return a+b
    }
    ```
- 나머지 매개변수 Rest Parameter : 생략 접두사 `...`를 사용하여 특정 위치의 인수부터 마지막 인수까지 한 번에 지정
``` javascript
function add(a, ...b){ // 첫번째 인수를 a에 저장하고, 나머지 인수들은 배열 b에 저장
    for(var i=0; i<b.length; i++){
        a -= b[i];
    }
    return a
}
```

## 변수의 유효 범위 Variable scope

### 지역 변수 Local Variable
: 함수내에서 선언된 변수

- 변수가 선언된 하무 내에서만 유효
- 함수가 종료되면 메모리에서 사라짐
- 함수의 매개변수도 지역 변수처럼 동작
- 지역 변수 선언에는 **반드시 var 키워드 사용** 
    - 키워드를 사용하지 않고 변수를 선언하면 전역 변수로 선언된다

### 전역 변수 Global Variable
: 함수의 외부에서 선언된 변수

- 프로그램의 어느 영역에서나 접근 가능
- 웹 페이지가 닫혀야만 메모리에서 사라짐
- 함수 내부에서도 접근하여 변경 가능

### 블록 변수
: 블록 안에서만 사용되는 변수

- let

## 함수의 유효 범위 Function scope
: JS는 함수를 블록({Block}) 대신 사용한다
<br> 함수는 자신이 정의된 범위 안에서 정의된 모든 변수 및 함수에 접근할 수 있다

- 블록 단위의 유효 범위 : 블록을 기준으로 하는 유효 범위
- '전역 함수' : 모든 전역 변수와 전역 함수에 접근 가능
- '내부 함수' : 다른 함수내에 정의된 함수. 부모 함수에서 정의된 모든 변수 및 부모 함수가 접근할 수 있는 모든 다른 변수까지 접근 가능
``` javascript
var x=10, y=20;
function sub(){
    return x-y; //전역 변수인 x, y 접근
}

function parentFunc(){
    var x=1, y=2; // 지역 변수 선언
    function add(){
        return x+y; // 전역 변수 x,y가 아닌 지역 변수 x,y에 접근
    }
    return add();
}
```

## 함수 호이스팅 Hoisting
: 함수의 유효 범위가 변수가 선언되기 전에도 똑같이 적용되는 것
<br>JS 함수 안에 있는 모든 변수의 선언은 함수의 맨 처음으로 이동된 것처럼 동작한다

- 다음과 같은 코드에서, 첫 write의 num이 전역 변수일 거라 생각하지만,
``` javascript
val num=10;
function printNum(){
    document.write(num);
    val num=20;
    document.write(num);
}
```
- 함수 호이스팅에 의해 다음과 같이 처리된다
``` javascript
//지역 변수 globalNum 선언 전의 globalNum의 값은 undefined입니다.
//지역 변수 globalNum 선언 후의 globalNum의 값은 20입니다.

val num=10;
function printNum(){
    val num;
    document.write(num); // undefined
    val num=20;
    document.write(num); // 20
}
```