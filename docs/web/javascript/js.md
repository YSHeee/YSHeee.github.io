# Javascript
: 넷스케이프 커뮤니케이션즈 코퍼레이션의 Brendan Eich가 Mocha라는 이름으로, 나중에는 LiveScript, 최종적으로 Javascrip라는 이름으로 개발중인 언어

- 객체 기반의 스크립트 프로그래밍 언어
- 동적이며, 타입을 명시할 필요 없는 인터프리터 언어<br> (컴파일 작업을 거치지 않고, 소스 코드를 바로 실행할 수 있는 언어)
- 객체 지향형 프로그래밍과 함수형 프로그래밍 모두 표현 가능
- 웹브라우저 내에서 주로 사용되며 웹의 동작 구현
- 유니코드 문자셋 사용


## ECMAScript
: ECMA 인터내셔널의 ECMA-262 기술 규격에 정의된 스크립트 프로그래밍 언어의 표준화된 스펙 
<br>현재 ECMA 국제 표준화 단체에서 Javascript 업데이트 중

---
## Syntax
- 실행문은 세미콜론`;`으로 구분
- 대소문자를 구분하므로 변수나 함수 이름, 예약어 작성 시 주의
- 리터럴(Literal) : 표현되는 값 그 자체 (여기서는 10)
``` javascript
var x = 10;
```

### 식별자 Identifier
: 변수나 함수의 이름을 작성할 때 사용하는 이름

- 영문자(대소문자), 숫자, 언더스코어 `_`, 달러 `$`만 사용 가능
- 숫자로 시작할 수 없음
- 키워드와 같은 이름으로 사용할 수 없음
- **Camel Case** 사용 :star:

### 주석 Comment
- 한 줄 주석 : `//`
- 여러 줄 주석 : `/* */`

### 변수 variable
: 데이터를 저장할 수 있는 메모리 공간
<br> 선언되지 않은 변수에 접근하고자 하면 오류가 발생하지만,
<br> 선언되지 않은 변수를 초기화할 경우에는 자동으로 선언을 먼저 한 후, 초기화 진행

- var: 같은 변수에 다른 타입의 값을 다시 대입할 수 있음
- let : block 단위 스코프 지원, 두 번 이상 선언할 수 없음
- const : 상수
``` javascript
var month; 
date= 25; // 묵시적 선언
var date = 25; // 변수의 선언과 동시에 초기화

// 여러 변수를 한 번에 선언
var a, b;
var a=1, b=2;
a=1, b=2;
```

---
### 출력 :star:
- window.alert() : 브라우저와는 별도의 대화 상자를 띄워 사용자에게 데이터 전달
- console.log() : 개발자 도구의 콘솔을 통해 데이터 출력
- document.write() 
    - 웹페이지가 로딩될 때 실행되면, 웹페이지에 가장 먼저 데이터를 출력 
    - 주로 테스트나 디버깅을 위해 사용
    - 모든 내용이 로딩된 후 실행되면, 모든 데이터를 지우고 자신의 데이터를 출력하므로 테스트 이외 용도에서는 주의
- HTML DOM 요소를 이용한 innerHTML 프로퍼티 
    - 가장 많이 사용되는 방법
    - document 객체의 `getElementByID()`나 `getElementsByTagName`() 등의 메소드를 사용하여 HTML 요소 선택
    - innerHTML 프로퍼티를 이용하여 선택된 HTML 요소의 내용이나 속성값 등을 변경

### 내/외부 적용
- 내부 자바스크립트 코드로 적용 
    - `<script>` 태그를 이용하여 HTML 문서 안에 삽입
    - `<head>` 태그나 `<body>` 태그, 또는 양쪽 모두에 위치 가능
- 외부 자바스크립트 파일 적용
    - 외부 파일로 생성하여 HTML 문서에 삽입
    - 웹 브라우저가 js 파일을 미리 읽어 올 수 있어 웹페이지의 로딩 속도 상향
``` javascript
<script src="/examples/media/example.js"></script>
```
---
## Javascript와 HTML
Javascript는 ...
- HTML의 내용을 변경할 수 있다
- HTML의 속성을 변경할 수 있다
- HTML의 스타일을 변경할 수 있다

JS 코드는 HTML 내의 어느 부분에 삽입해도 가능하나 주로 `<head>`나 `body`에 삽입한다
<br>헤더에 위치한 JS 코드는 Content(`<body>`)의 렌더링 이전에 브라우저에 의해 먼저 해석되어 렌더링을 지연시킬 수 있다
<br>따라서, 이벤트 핸들러 기능의 JS 코드는 가급적 **`</body>` 태그의 바로 위에 삽입한다**
``` javascript
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>자바스크립트학습</title>
</head>
<body>
	<h1>자바스크립트의 수행 결과 출력</h1>
	<hr>
	<h2>자바스크립트를 재미있게 학습합시다...</h2>
	<h3></h3>
	<script> // script 코드가 구동되는 동안, html parser는 대기중.. (단일스레드이므로)
		window.alert("(1) 어디에 출력될까?");
		console.log("(2) 어디에 출력될까?");
		document.write("(3) 어디에 출력될까?"); 
		// DOM 기술을 활용하여 출력
		document.getElementsByTagName("h3")[0].textContent = "(4) 어디에 출력될까?";
	</script>
</body>
</html>
```

---
## JS error
```javascript
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>Insert title here</title>
</head>
<body>
	<h1>JavaScript의 변수 선언과 활용(1)</h1>
	<script>
		document.writeln(123);
		document.writeln(v1+"<br>"); // 오류 발생, 출력 불가
		document.writeln(456); //위 코드의 오류 발생으로 인해 출력 불가
	</script>
	<hr>
	<script> //해당 영역은 출력 가능
        // var는 여러 번 선언 가능. 디버깅 ...
        // writeln이 개행문자를 넣어주지만, HTML에서 개행문자는 공백` `이므로 br을 붙여줌
		var v1; //let, const
		document.writeln(v1+"<br>"); //undefined
		v1 = 100;
		document.writeln(v1+"<br>"); //100
		v1 = '가나다';
		document.writeln(v1+"<br>"); //가나다
		var v1 = true;
		document.writeln(v1+"<br>"); //true	
		v1 = 123;
		document.writeln(v1+45+"<br>"); //168	
		v1 = '123';
		document.writeln(v1+45+"<br>");	//12345
	</script>
	<hr>
	<script>
		document.writeln(v1+"<br>"); //123
	</script>
</body>
</html>
```


---
!!! quote
    - 위키백과
    - [TCP School](https://www.tcpschool.com/javascript/intro)