# AJAX
: Asynchronous JavaScript and XML
<br> Reload(=refresh 재갱신)하지 않고, 웹페이지의 일부만을 갱신하여 웹서버와 데이터를 교환하는 방법. 빠르게 동적 웹페이지를 생성하는 기술이다

- 고전적 웹 통신과 AJAX 웹 통신
![1](./images/ajax-1.PNG)

- 동기/비동기
![2](./images/ajax-2.PNG)

## AJAX의 동작과정
![3](./images/ajax-3.PNG)

1. 이벤트 발생에 의해 이벤트핸들러 역할의 JavaScript 함수를 호출
2. 핸들러 함수에서 XMLHttpRequest 객체를 생성한다. 요청이 종료되었을 때 처리할 기능을 콜백함수로 만들어 등록한다.
3. XMLHttpRequest 객체를 통해 서버에 요청을 보낸다.
4. 요청을 받은 서버는 요청 결과를 적당한 데이터로 구성하여 응답한다.
5. XMLHttpRequest 객체에 의해 등록된 콜백함수를 호출하여 응답 결과를 현재 웹 페이지에 반영한다.


## XMLHttpRequest 객체
: 서버측과의 비동기 통신 제어

- new XMLHttpRequest()
=== "Example"
    ``` html
    <script>
    function requestAjax() {
        const xhr = new XMLHttpRequest(); // 객체 생성
        xhr.onload = function () { // onreadystatechange = 함수 (Event-Handler 등록)
            const result = document.getElementById("result");
            result.innerHTML += xhr.responseText + "<hr>"; //현재 페이지에 내용 붙이기		
        }
        xhr.open("GET", "/edu/first.html", true);  // GET, POST, HEAD, PUT, DELETE
        xhr.send();
    }
    </script>
    ```
=== "Example-JSON"
    ``` html
	<script>
    function requestAjax() {
        const xhr = new XMLHttpRequest();
        xhr.onload = function () {
            const result = document.getElementById("result");
            const jsonObj = JSON.parse(xhr.responseText);
            result.innerHTML += "<h2>"+jsonObj.LampScpgmtb.RESULT.MESSAGE+"</H2>";	
            const target = jsonObj.LampScpgmtb.row;				
            for(let i in target) {					
                result.innerHTML += "<h3>"+target[i].UP_NM+"</H3>";
                result.innerHTML += "<h4>"+target[i].PGM_NM+"</H4>";
            }
            result.innerHTML += "<hr>";
        }
        xhr.open("GET", "http://openapi.seoul.go.kr:8088/796143536a756e69313134667752417a/json/LampScpgmtb/1/3/", true);
        xhr.send();
    }
	</script>
    ```
=== "Example-POST"
    ``` html
        <script>
        window.addEventListener("load", function() {
            document.getElementById("loginb").onclick = handleButtonPress;
        });
        let xhr;
        let id, form;
        function handleButtonPress(e){
            e.preventDefault();
            xhr =  new XMLHttpRequest();
            form = document.querySelector("#loginf");
            id = document.querySelector("#id");
            const passwd = document.querySelector("#passwd");
            const queryString = `id=${id.value}&passwd=${passwd.value}`;
            xhr.addEventListener("load", handleResponse);
            xhr.open("POST", form.action, true);
            xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
            xhr.send(queryString);
        }
        function handleResponse() {
            const jsonObj = JSON.parse(xhr.responseText);
            const output = document.querySelector("output");
            if (jsonObj.result == "ok") {
                output.textContent="로그인 성공!!";
                output.style.color = "blue";
            } else if (jsonObj.result == "fail") {
                output.textContent="로그인 실패!!";
                output.style.color = "red";
                form.reset();
                id.focus();
            }
        }								
        </script>
    ```
=== "Example-Image"
    ``` html
        <script>
        let imgname = 1;
        function getImage() {
            imgname = imgname == 10 ? 1 : imgname+1; 
            const xhr = new XMLHttpRequest();	
            xhr.responseType = 'blob'; <!-- blob : binary file -->
            xhr.onload = function(e) {
                if (this.status == 200) {
                    const blob = e.target.response
                    const img = document.createElement('img');
                    img.width=100;
                    img.height=100;
                    img.src = URL.createObjectURL(blob); <!-- 가상 url 생성 -->
                    document.body.appendChild(img);    
                }
            };
            xhr.open('GET', `/edu/images/${imgname}.jpg`, true);
            xhr.send();
        }							
        </script>
    ```

|  분류  |  멤버  |  개요  |
| property | `onreadystatechange`| 통신 상태가 변화된 타이밍에 호출되는 이벤트 핸들러 |
| | `readyState` | HTTP 통신 상태 취득 |
| | `status` | HTTP Status 코드 취득 |
| | `responseType` | 응답받으려는 컨텐트 타입 <br> "arraybuffer", "blob", "
document", "json"/"text" |
| | `responseText` | 응답 본체를 plaintext로 취득 |
| | `responseXML` | 응답 본체를 XML(XMLDocument)로 취득 |
| | `response` | 지정된 응답 타입에 따른 응답 객체 <br> binary 형식(이미지 등)|
| | `upload` | XMLHttpRequestUpload 객체 제공 |
| method | `abort()` | 현재의 비동기 통신 중단 |
| | `getAllResponseHeaders()` | 수신한 모든 HTTP 응답 헤더 취득 |
| | `getResponseHeader(header)` | 지정한 HTTP 응답 헤더 취득 |
| | `open( ... )` | HTTP 요청 초기화 |
| | `setRequestHeader(header, value)` | 요청 시에 송신하는 헤더 추가 |
| | `send([body])` | HTTP 요청 송신(인수 body는요청본체) |
| 이벤트 관련 속성 | | |
| | `onloadstart` | |
| | `onprogress` | |
| | `onabort` | |
| | `onerror` | |
| | `onload` | |
| | `ontimeout` | |
| | `onloadend` | |
| | `onreadystatechange` | |

- readyState
    - 0 : 미초기화 (open 메서드가 호출되지 않음)
    - 1 : 로드중 (open 메서드는 호출됐지만, send 메서드는 호출되지 않음)
    - 2 : 로드 완료 (send 메서드는 호출됐지만, response status/header는 미취득)
    - 3 : 일부 응답 취득 (응답 스테이터스/헤더만 취득, 본체는 미취득)
    - 4 : 모든 응답데이터 취득 완료
- open(HTTP Method, url, [비동기 모드 통신 여부])
    - url : AJAX로 요청하려는 서버의 대상 페이지
    - 비동기 모드 통신 여부 : true(비동기), false(동기)
- send([요청 파라미터])
    - ArrayBufferView, Blob, Document, DOMString, FormData, null, Query 문자열 등

## fetch() 함수 이용
: ECMA6~

## axios 추가 라이브러리 이용

---
## XML vs JSON



---
!!! quote
    - 김정현 강사님