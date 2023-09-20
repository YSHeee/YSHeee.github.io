# BOM (Browser Object Model)
: 브라우저에서 실행되는 자바스크립트를 위해 브라우저가 제공하는 객체
<br>웹페이지의 내용을 제외한 브라우저의 각종 요소들을 객체화 시킨 것

## window
: 최상위 객체이자 전역 객체. 브라우저 자신을 의미함
<br> 각 탭별, iframe 별로 하나씩 존재
<br> 아래 객체들은 window 객체의 속성으로 정의
<br> 전역 객체로서 멤버 사용시 객체명을 생략할 수 있음
<br> 전역 코드에서의 this는 window 객체를 참조한다

- navigator : 브라우저(이름, 버전등) 정보를 보관하는 객체
- document : 브라우저의 도큐먼트 영역과 관련된 기능을 제공하는 객체
    - write()
    - writeln()
    - getElementsByTagName(태그명)
    - getElementById(id속성값)
    - getElementByClassName(class속성값)
    - querySelector(css선택자)
    - querySelectorAll(css선택자)
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
- history : 현재의 브라우저가 접근했던 URL의 정보를 보관하는 객체
- screen : 클라이언트 머신의 화면 크기나 해상도 등의 정보를 얻을 수 있는 객체

---
- alert()
- prompt()
- confirm()
- setInterval() - clearInterval()
- setTimeout() - clearTimeout()
- open()
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