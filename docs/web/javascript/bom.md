# BOM (Browser Object Model)
: 브라우저에서 실행되는 자바스크립트를 위해 브라우저가 제공하는 객체
<br>웹페이지의 내용을 제외한 브라우저의 각종 요소들을 객체화 시킨 것

## window
: 최상위 객체이자 전역 객체. 브라우저 자신으로서 창(window)을 나타냄

- 각 탭별, iframe 별로 하나씩 존재
- 전역 객체로서 멤버 사용시 객체명을 생략할 수 있음
- 전역 코드에서의 this는 window 객체를 참조한다
- JS의 모든 객체, 전역 함수, 전역 변수, DOM의 요소들은 window 객체의 property이다

- - window.onload() : 로드가 끝난 후 수행

#### 대화상자 Dialog box :star:
: 사용자에게 보여줄 수 있는 간단한 대화 상자 생성

- alert() : 메시지를 보여주고, 그에 대한 사용자의 <확인> 대기
- confirm() : 메시지를 보여주고, 사용자가 <확인/취소>를 누르면 그 결과를 bool 값으로 반환
- prompt() : 메시지를 보여주고, 사용자가 입력한 문자열 반환 (취소하면 null 반환)
- showModelDialog()

#### 브라우저 창 크기 조절
- 브라우저 창: Viewport (툴바, 스크롤바는 포함되지 않음)
- innerHeight
- innerWidth
``` javascript
window.innerHeight; // innerHeight만 써도 정상 동작
window.innerWidth;
screenX // 해당 브라우저의 왼쪽 모서리와 사용자 스크린 왼쪽 모서리 사이의 거리 반환
screenY // 해당 브라우저의 위쪽 모서리와 사용자 스크린 위쪽 모서리 사이의 거리 반환
```

#### 브라우저 새 창 열기 open() & 닫기 close()
- open() : 새로운 브라우저 창을 열면서 세부적인 옵션 설정 가능
- close() : 현재 브라우저 또는 특정 브라우저 닫기
``` javascript
/* 메뉴바, 주소창, 크기조절 손잡이, 스크롤 바, 상태 바를 가지는 새로운 브라우저 창 open 예제 */

var newWindowObj;
// 변수 strWindowFeatures를 통해 브라우저 창의 옵션들을 일일이 설정할 수 있음.
var strWindowFeatures = "menubar = yes,location = yes,resizable = yes,scrollbars = yes,status = yes";
function openWindow() {
    newWindowObj = window.open("/html/intro", "HTML 개요", strWindowFeatures);}

// Close
function closeWindow() { 
    newWindowObj.close();}
```

#### 브라우저 창 이동 move & resize
- moveTo
- resizeTo
- moveBy
- resizeBy
``` javascript
var child = window.open('', '', 'width=300, height=200');
const width = screen.width;
const height = screen.height;
child.moveTo(0, 0);
child.resizeTo(width, height);

window.setInterval(function() {
    child.resizeBy(-20, -20);
    child.moveBy(10, 10);
    child.document.write(new Date());}, 1000);
```

---
## [Document](./dom.md)
: 브라우저의 도큐먼트 영역과 관련된 기능을 제공하는 객체

- write()
- writeln()
- getElementsByTagName(태그명)
- getElementById(id속성값)
- getElementByClassName(class속성값)
- querySelector(css선택자)
- querySelectorAll(css선택자)

---
## Location
: 현재 웹 페이지에 대한 URL 정보를 보관하는 객체
<br> 현재 브라우저에 표시된 HTML 문서의 주소를 얻거나 브라우저에 새 문서를 불러올 때 사용 가능

- location.port
- location.hash

#### 현재 문서의 URL 주소 href
``` javascript
location.href // 현재 문서의 주소
```

#### 현재 문서의 호스트 이름 hostname
```javascript
location.hostname // 현재 문서의 인터넷 호스트 이름
```

#### 현재 문서의 파일 경로명 pathname
- URL : Hostname + Pathname, 웹 서버로 컨텐츠를 요청할 때 해당 컨텐츠의 위치를 알려주기 위한 규약
``` javascript
location.pathname
```

#### 현재 창에 문서 불러오기
- assign() : 브라우저 창에 지정된 URL 주소에 존재하는 문서를 불러옴
- replace() : 현재 문서를 브라우저의 히스토리에서 제거하고, 새 문서를 불러옴
- reload() : 브라우저 창에 현재 문서를 다시 불러옴
- href
``` javascript
location.assign("first.html");
location.replace("first.html"); // 뒤로가기 버튼을 눌러도 이전 페이지로 돌아갈 수 없음
location.href="first.html";
location.reload(); // 페이지 새로고침
```

---
## History
: 현재의 브라우저가 접근했던 URL의 정보를 보관하는 객체

#### history 목록 접근
- length : 히스토리 목록의 개수 반환
- back() : 브라우저 뒤로 가기
- forward() : 브라우저 앞으로 가기
- go() : 인수로 전달받는 정수만큼 히스토리 목록 사이 이동
``` javascript
history.length // 히스토리 목록 개수

window.history.back(); // 이전 페이지로 가기
window.history.go(-1); // 이전 페이지로 가기
window.history.forward(); // 다음 페이지로 가기
```

---
## Screen 
: 화면 크기나 해상도 등 디스플레이 화면에 대한 정보를 얻을 수 있는 객체

#### 사용자 화면 크기 pixel
- width
- height
``` javascript
screen.width // 사용자의 디스플레이 화면 너비
screen.height // 사용자의 디스플레이 화면 높이

window.outerWidth // 브라우저 창의 너비
window.outerHeight // 브라우저 창의 높이
```

#### 실제 사용할 수 있는 화면 크기 pixel
: 운영체제의 작업 표시줄과 같은 공간을 제외한 크기 반환

- availWidth
- availHeight
``` javascript
screen.availWidth // 실제 사용할 수 있는 화면 너비
screen.availHeight // 실제 사용할 수 있는 화면 높이
```

#### 사용할 수 있는 비트 수
- colorDepth : 사용자 화면에서 한 색상당 사용할 수 있는 비트 수
- pixelDepth : 사용자 화면에서 한 픽셀당 표시할 수 있는 비트 수
``` javascript
screen.colorDepth;
screen.pixelDepth;
```
     
---
## Navigator
: 브라우저(이름, 버전등) 정보를 보관하는 객체
<br>Netscape의 초기 웹 브라우저였던 Navigator에서 유래

- 브라우저 스니핑 Browser sniffing
: 방문자의 웹 브라우저의 종류를 미리 파악하여 조치함으로써 브라우저 간의 호환성을 유지하는 방법

#### 현재 브라우저의 이름
: 브라우저 간의 호환성을 위해 스니핑 코드로 대부분의 브라우저가 이름을 "Netscape", 코드명을 "Mozilla"로 사용한다
- 익스플로러 11, 크롬, 파이어폭스, 사파리 : Browser name - Netscape
- 익스플로러 10 이하, 크롬, 파이어폭스, 사파리, 오페라 : Browser code name - Mozilla
- ~~appName~~
- ~~appCodeName~~

#### 현재 브라우저의 버전
- ~~appVersion~~
- ~~userAgent : appVersion 정보 + 상세 정보~~

#### 현재 브라우저의 기본 언어 설정
- language : 현재 사용 중인 브라우저의 기본 언어 설정 반환
``` javascript
navigator.language;
```

#### 자바 애플릿 실행 여부
- javaEnabled() : 현재 사용 중인 브라우저가 자바 애플릿을 실행할 수 있는지 검사하는 비표준 method
``` javascript
navigator.javaEnabled()
```

#### Cookie 사용 여부
- cookieEnabled : 현재 사용 중인 브라우저가 쿠키를 사용할 수 있는지 검사하는 비표준 property
``` javascript
navigator.cookieEnabled
```

---
## 타이머
: 일정 시간이 지난 뒤에 함수 호출
- setTimeout() : 명시된 시간이 지난 뒤에 지정된 함수 호출
    - 밀리초 단위 설정
    - 성공적으로 호출하면, timeoutId 반환
- setInterval() : 지정된 시간 간격마다 지정된 함수를 반복적으로 호출
    - 밀리초 단위 설정
    - 성공적으로 호출하면, timeoutId 반환
- clearTimeout() : setTimeout() 메소드의 반환값을 clearTimeout() 메소드의 인수로 전달하여 계획된 함수의 호출 취소
- clearInterval() : 메소드의 반환값을 clearInterval() 메소드의 인수로 전달하여 반복되는 함수의 호출 취소
=== "set"
    ``` javascript
    window.setTimeout(호출할함수, 지연시간);
    window.setInterval(호출할함수, 지연시간);

    function startTimeout() {
        setTimeout(printCurrentDate, 2000);
    }
    function startInterval() {
        setInterval(printCurrentDate, 2000);
    }
    function printCurrentDate() {
        document.getElementById("date").innerHTML = new Date();
    }
    ```
=== "clear"
``` javascript
var timeoutId;

function startTimeout() {
    timeoutId = setTimeout(printCurrentDate,2000);
}
function startInterval() {
    timeoutId = setInterval(printCurrentDate, 2000);
}
function cancelTimeout() {
    clearTimeout(timeoutId);
}
function cancelInterval() {
    clearInterval(timeoutId);
}
function printCurrentDate() {
    document.getElementById("date").innerHTML += new Date() + "<br>";
}
```

---

- location : 현재 웹 페이지에 대한 URL 정보를 보관하는 객체
    - href
    - reload()
``` javascript
function getLocation() {
    if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(showPosition,showError);
    }
    else{x.innerHTML=" 이 브라우저는 geolocation을 지원하지 않습니다.";}
}
function showPosition(position) {
    window.alert("위도: " + position.coords.latitude + "\n경도: " + position.coords.longitude);       
}
function showError(error) {
    switch(error.code) {
    case error.PERMISSION_DENIED:
        x.innerHTML="사용자가 위치 기능 사용을 거부했습니다."
        break;
    case error.POSITION_UNAVAILABLE:
        x.innerHTML="위치를 구할 수 없습니다.";
        break;
    case error.TIMEOUT:
        x.innerHTML="사용자가 위치 기능 사용을 거부했습니다.";
        break;
    case error.UNKNOWN_ERROR:
        x.innerHTML="기타 에러";
    }
}
```

---

=== "Select"
    ``` javascript
    <form name="fm">
        <select id="choice" onchange="go();"> // onchange로 go 함수 호출 
            <option value="">---관심있는 기술을 선택해 주세요---</option>
            <option value="https://www.w3schools.com/js/default.asp">Learn JavaScript</option>
            <option value="https://www.w3schools.com/js/js_htmldom.asp">Learn HTML DOM</option>
        </select>
    </form>
    <script>
    function go(){	
        location.href = document.getElementById("choice").value;
        //location.href = document.querySelector("#choice").value;
    }
    </script>
    ```
=== "Font"
    ``` javascript
    <head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
    <style>
        @font-face {
        font-family: 'RixMomsBlanketR';
        src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2302@1.0/RixMomsBlanketR.woff2') format('woff2');
        font-weight: normal;
        font-style: normal;
        }
        * {
            font-family: 'RixMomsBlanketR';
        }
        a {		
            text-decoration : none;
            font-size : 2em;
            margin : 10px;
        }
    </style>
    </head>
    ```
=== "open, setInterval, resize, move"
    ``` javascript
    <head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
    <script>
        //변수를 선언합니다.
        const child = window.open('../../first.html', '', 'width=300, height=200'); //자식 window 생성
        const width = screen.width;
        const height = screen.height;
        child.moveTo(0, 0);
        child.resizeTo(width, height);   
        window.setInterval(function () {
            child.resizeBy(-20, -20);
            child.moveBy(10, 10);
        }, 2000);  
    </script>
    </head>
    ```


---
!!! quote
    - [TCP School](https://www.tcpschool.com/javascript/intro)