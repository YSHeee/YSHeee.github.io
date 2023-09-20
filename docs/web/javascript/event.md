# Event
: 웹브라우저가 알려주는 HTML 요소에 대한 사건의 발생을 의미

- 이벤트 타입(=event name) : 발생한 이벤트의 종류를 나타내는 문자열
    - click, mouseover, load, keydown, keyup, change, submit,...
- 이벤트 타겟 : 이벤트가 발생한 대상 DOM 객체
- 이벤트 핸들러 : 이벤트 처리 코드를 구현한 함수
- 이벤트 명세 
    - DOM Level 3 이벤트 명세
    - HTML5 관련 이벤트 명세
    - 모바일 장치를 위한 이벤트 명세

---
## Event Model
: 웹 페이지에서 어떠한 액션이 발생했을 때, 수행되는 코드를 작성하여 등록하는 방법

- In-line 이벤트 모델 : 대상의 **HTML 태그**에 속성으로 정의하는 모델 (지역적)
``` javascript
<태그명 onxxx = "function()">;
```
- 고전 이벤트 모델 : 대상 DOM 객체를 찾아 이벤트 핸들러 등록 (전역적)
``` javascript
let dom  = document.querySelector("#target");
dom.onxxx = function; // xxx : 이벤트 타입
dom.onxxx = null; // 이벤트 해제
```
- 표준 이벤트 모델 : 대상 DOM 객체에 다음 method 사용 (전역적) :star:
``` javascript
let dom  = document.querySelector("#target");
dom.addEventListener = (eventName, handler_func, useCapture);
dom.removeEventListener(eventName, handler_func); // 이벤트 해제
```

---
## Event Handler
: Event Listener, 이벤트가 발생했을 때 그 처리를 담당하는 함수

### 이벤트 리스너 등록

1. 이벤트의 대상이 되는 객체나 요소에 프로퍼티로 등록<br>: 이벤트 타입별로 오직 하나의 이벤트 리스너만을 등록할 수 있음
    - JS 코드에서 Property로 등록
    - HTML 태그에 속성으로 등록
    ``` javascript
    // Property로 등록
    window.onload = function() { // HTML 문서가 로드될 때 실행
    var text = document.getElementById("text"); // text id 선택
    text.innerHTML = "HTML 문서가 로드되었습니다.";}

    // HTML 태그 속성 등록 - 가독성이 안좋고, 유지보수가 힘들어짐
    <p onclick="alert('문자열을 클릭했어요!')">클릭!</p>
    ```
2. 객체나 요소의 메소드에 이벤트 리스너를 전달
    - addEventListener()
    - attachEvent()
``` javascript
/* 대상객체.addEventListener(이벤트명, 실행할이벤트리스너, 이벤트전파방식)
    - 이벤트명 : 이벤트 리스너를 등록할 이벤트 타입을 문자열로 전달 
    - 실행할 이벤트 리스너 : 지정된 이벤트가 발생했을 때 실행할 이벤트 리스너 전달
    - 이벤트 전파 방식 : true면 capturing 방식, false면 bubbling 방식
*/
var showBtn = document.getElementById("btn"); // 아이디가 "btn"인 요소
showBtn.addEventListener("click", showText);  // click 이벤트 리스너 등록
showBtn.addEventListener("mouseover", showText); // mouseover 이벤트 리스너 등록
function showText() {
    document.getElementById("text").innerHTML = "텍스트가 나타났습니다!";
}
function mouseoverBtn() {
    document.getElementById("text").innerHTML = "버튼 위에 마우스가 있네요!";
}
```

### 이벤트 리스너 삭제
- removeEventListener()
``` javascript
btn.removeEventListener("click", showText);
```

### 이벤트 리스너 호출




---
``` javascript
<script>    
	function f1(t) {
		alert(t.textContent);
	}
	const dom2 = document.querySelector('#t1');
    const dom3 = document.querySelector('#t2');
	function f2(e) {
		alert(e);
		alert(e.target.textContent); //발생된 이벤트 객체
		alert(this.textContent);
	} 
    dom2.onclick = f2;
    dom3.addEventListener("click", f2);
</script>
```