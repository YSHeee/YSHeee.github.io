# WEB

## WWW이란?
: World Wide Web
<br> 인터넷에 연결된 컴퓨터를 통해 전세계 사람들이 정보를 공유할 수 있는 사이버 공간
<br> 1989년 3월 영국의 유럽 입자 물리 연구소의 공학자 팀 버너스리의 제안에 의해 연구/개발 시작

- 인터넷 : 1960년대 미국 국방부의 ARPA에서 시작된, TCP/IP 통신 규약을 통해 데이터를 주고 받는 컴퓨터 네트워크
- Web : 전자 메일과 같이 인터넷 상에서 동작하는 하나의 서비스 <br> 인터넷에서 HTTP 프로토콜, 하이퍼텍스트, HTML 형식 등을 사용하여 그림과 문자를 교환하는 전송방식
- 웹브라우저 : 웹사이트에 구축된 웹페이지. HTML 문서를 볼 수 있는 응용 프로그램 (크롬, 파이어폭스 등)
- 웹 서버 : 인터넷을 통해 사용자에게 웹서비스를 제공하는 컴퓨터의 HW/SW
- 클라이언트 : 웹서비스를 이용하는 사용자
- 웹 호스팅 : 전문 업체에서 자신의 웹 서버와 네트워크를 이용하여 개인/기관에게 홈페이지를 구축할 수 있도록 디스크 공간을 임대해주는 서비스
- 웹 페이지 : 웹 브라우저 화면에서 보이는 각각의 화면. HTML, CSS, JS 등의 프로그램 소스파일과 데이터 파일로 구성
- 웹 사이트 : 도메인 네임에 구축된 웹 페이지 묶음

## 웹표준
: W3C 조직에서 정한 표준기술만을 사용하여, 웹 페이지 작성시 문서의 구조와 표현 방법 그리고 상호 동작을 구분하여 구현하는 것

```mermaid
graph TB

    subgraph HTML5
        H(HTML5 문서\n웹페이지 내용 담당) -- + --> C(CSS3 디자인\n웹페이지 디자인 담당)
        C -- + --> J(JavaScript 동적인 상호작용\n웹페이지 동작 담당)
    end
```

---
### [MDN](https://developer.mozilla.org/ko/docs/Web)
### [W3School](https://www.w3schools.com/)
### [ECMA-262](https://262.ecma-international.org/14.0/#sec-islooselyequal)
### [HTML5-Test](https://html5test.com/)
### [Can I use](https://caniuse.com/)
### [W3C](https://www.w3.org/)
### [trio.co.kr](http://trio.co.kr/)


---
!!! quote
    - HTML/CSS 입문 예제 중심 (지은이: 황재호 | 출판사: 인포앤북(주))
    - 김정현 (unicodaum@hanmail.net)