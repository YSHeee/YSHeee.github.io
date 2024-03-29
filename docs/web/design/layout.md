# HTML, CSS - Web Page Layout

## 박스 요소의 중앙 배치
- `margin: 0 auto;` : 상하단 마진은 0, 좌우측 마진은 auto = 박스 중앙 배치
- `text-align: right;` : 우측 정렬
- `text-align: center;` : 가운데 정렬
- `height: 100px` = `line-height: 100px` : 둘을 같은 크기로 선언하면 상하 중앙에 배치
``` html
<head>
    <meta charset="utf-8">
    <title>TITLE</title>
    <style>
        #box {
            margin: 0 auto; 
            background-color: red;
        }
        #box2 {text-align: right;}
    </style>
</head>
<body>
    <div id="box">
        안녕하세요
    </div>
</body>
```

---
## float 
: 웹 페이지의 요소를 공중에 띄워 화면의 좌측 또는 우측에 배치 가능

- `float: left;` : 요소를 공중에 띄워 좌측에 배치
- `float: right` : 요소를 공중에 띄워 우측에 배치
- `both` : 이전에 사용된 float 속성 값 left와 right의 기능 둘 다 해제
- `clear` : 한 요소에 float 속성이 적용되면, 다음 요소들도 계속해서 float의 영향을 받게 된다. 영향에서 벗어나 새로운 줄에 배치하고자 할 때 사용
- float 속성이 적용되지 않은 a,b : display 속성의 기본값인 블록 방식이 적용됨
``` html
<head>
    <meta charset="utf-8">
    <title>TITLE</title>
    <style>
        div {float:left;}
        h3 {clear:both;}
    </style>
</head>
<body>
    <div><img src=".png"></div>
    <h3>안녕하세욥</h3> <!-- 해당 단락은 이미지 박스 다음의 새로운 줄에서 시작 -->
</body>
```
---
## div 요소 레이아웃
``` html
<head>
    <meta charset="utf-8">
    <style>
        #a { width: 800px; margin: 0 auto;}
        #header { height: 100px; background-color: hsl(88, 67%, 70%);}
        #sidebar { float: left; width: 200px; height: 300px; background-color: hwb(189 42% 15%);}
        #section {float: right; width: 600px; height: 300px; background-color: hwb(46 47% 3%);}
        #footer {clear: both; height: 60px; background-color: rgba(236, 144, 144, 0.904);}

        #a,#header,#sidebar,#section,#footer {font-size: 20px; text-align: center;}
    </style>
</head>
<body>
    <div id="a">
        <div id="header">header</div>
        <div id="sidebar">sidebar</div>
        <div id="section">section</div>
        <div id="footer">footer</div>
    </div>
</body>
```
![HTML-layout](../images/html_layout.png){:style width=80%;height=70%}

---
## HTML 레이아웃 요소 :star:
- 기존 레이아웃 방식
    - 모든 레이아웃 영역에 `<div>` 태그 사용 -> 세부적인 구별이 어려움
    - `<div>` 태그의 id 속성값으로 의미를 표시하거나 class 속성값으로 의미 표현
- 시맨틱 레이아웃 방식
    - 레이아웃 영역을 시맨틱 태그를 이용하여 구분
    - `<div>` 대신 여러 시맨틱 태그로 표시
    - 표준 시맨틱 태그로 정의함으로써 문서의 의미 구조를 명확하고 간결하게 표현하도록 개선

![HTML-1](../images/html_1.PNG)

### 시맨틱 레이아웃
- `<body>`
    - `<header>` : 주로 머리말, 제목 표현
    - `<section>` : 본문 콘텐트 담당
    - `<footer>` : 하단 푸터, 회사소개/저작권/약관/제작정보 등 (연락처는 `<address>`)
- `<nav>` : 네비게이션. 콘텐츠를 담고 있는 문서를 사이트간에 서로 연결하는 링크 역할 담당 <br> 위치에 영향을 받지 않아 어디에서든 사용 가능
- `<article>` : 실질적인 내용 (ex. 뉴스에서 정치/사회 대분류는 section, 기사내용은 article)
- `<aside>` : 본문 이외의 내용을 담는 사이드바. 주로 광고나 링크
- `<div>` : HTML5에 와서는 글자나 사진등의 콘텐트들을 묶어서 CSS 스타일을 적용시킬 때 사용

![HTML-layout2](../images/html_layout2.png)
``` html
<head>
    <meta charset="utf-8">
    <title>TITLE</title>
    <style>
        a { width: 800px; margin: 0 auto;}
        header { height: 100px; background-color: hsl(88, 67%, 70%);}
        aside { float: left; width: 200px; height: 300px; background-color: hwb(189 42% 15%);}
        section {float: left; width: 600px; height: 300px; background-color: hwb(46 47% 3%);}
        footer {clear: both; height: 60px; background-color: rgba(236, 144, 144, 0.904);}
        header,aside,section,footer {font-size: 20px; text-align: center;}
    </style>
</head>
<body>
    <div id="a">
        <header>header</header>
        <aside>sidebar</aside>
        <section>section</section>
        <footer>footer</footer>
    </div>
</body>
```
---
## 요소의 위치 지정
- position : HTML 요소의 위치 지정 (float는 화면의 좌/우측에 배치)
    - `position: relative;` : 상대 위치 지정. 요소의 원래 위치에서 지정한 만큼 이동한 지점에 배치
    - `position: absolute;` : 절대 위치 지정. 브라우저의 좌측 상단 시작점(기본 마진 제외)에서 지정한 만큼 이동한 지점에 배치
    - 부모 요소(relative) + `position: absolute;` : 부모 요소의 원점을 기준으로 요소 배치
    - `position: fixed;` : 웹 페이지의 특정 위치에 고정
``` html
<head>
    <meta charset="utf-8">
    <title>TITLE</title>
    <style>
        #a { position: relative; left:60px; top: 60px; width: 800px; height: 500px; }
        #b { position: absolute; left: 70px; top: 60px; width: 800px; height: 500px; }
        #parent { position: relative; width: 800px; height: 500px; }
        #d { position: fixed; right: 70px; top: 60px; width: 800px; height: 500px; }

    </style>
</head>
<body>
    <div id="a">상대위치 A</div>
    <div id="b">절대위치 B</div>
    <div id="parent">
        <div id="b">부모가 있는 절대위치 B</div>
    </div>
    <div id="d">고정위치 D</div>
</body>
```
---
## box-sizing
: 패딩과 경계선 설정이 요소에 사용되더라도 width와 height 속성에 의해 설정된 박스의 크기는 그대로 유지
<br> 요소에 패딩과 경계선이 적용되면서 박스의 크기가 커지는 단점 보완

---
## 전체 페이지 레이아웃

1. 박스 형태로 구획 나누기 (Ex. 상단 헤더, 메인 이미지, 사이드바, 메인 섹션, 하단 푸터)
2. 소스 파일 정리
    - layout.html : 전체 페이지 레이아웃 (마진 패딩 초기화, header 높이 설정, box의 중앙 배치와 너비 설정 등)
    - header.html : 상단 헤더 (마진 패딩 초기화, box-sizing)
    - mainimage.html : 메인 이미지
    - header-mainimage.html : 헤더+메인 이미지
    - sidebar.html : 사이드바
    - main.html : 메인 섹션
    - footer.html : 하단 푸터
    - index.html : 완성된 웹 페이지

---
## 반응형 웹
: 하나의 웹 페이지로 데스크톱, 태블릿, 스마트폰 등 다양한 기기의 화면에서 콘텐츠가 제대로 보이게 하는 기술
<br> 스마트 폰 전용 모바일 사이트를 별도로 제작할 필요 없이, 하나의 웹사이트로 다양한 기기의 화면에 제대로 된 페이지 표시 가능

- 뷰포트(Viewport) : 브라우저 화면 크기 (메뉴바, 탭 영역 제외)
- Ethan Marcotte가 처음 도입
- `<meta>` 태그를 이용하여 모바일 기기의 뷰포트 설정

``` css
/* `width=device-width` : 웹페이지의 너비를 모바일 기기의 뷰포트로 설정 */
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
```

### 뷰포트의 속성

|    속성   |     설명    |
| :-------: | :---------: |
|   width   | 픽셀 단위로 뷰포트의 너비 설정 (default: device-width) |
|   height  | 픽셀 단위로 뷰포트의 높이 설정 (default: device-height)|
| initial-scale | 초기 배율 (1.0: 기본값, 0.5: 두배 축소, 2.0: 두배 확대) |
| user-scalable | yes: 사용자가 화면 확대/축소 가능, no: 불가 <br>(default: no) |
| minimum-scale | 사용자가 축소할 수 있는 최소값 (default: 0.25) |
| maximum-scale | 사용자가 확대할 수 있는 최대값 (default: 0.5) |

---
### 그리드 뷰
: 웹페이지를 제작할 때 Column을 기반으로 하는 것

#### 가변그리드 
: Fluid Grid. 열의 너비가 웹페이지를 접속하는 다양한 기기의 해상도에 맞추어 가변적으로 변화

- px 단위 대신 **%** 사용
- `calc()` : px과 % 함께 사용

``` css
header {
    width: 25%; /* 뷰포트 전체 너비(100%)의 25% 차지 */
    float: left;
}
#a {width: 300px;} /* a는 300px로 고정 */
#b {
    width: calc(100% - 300px); /* 뷰포트 전체 너비(100%)에서 300px을 뺀 결과 값 */
    height: 150px;
}
```

#### 열 그리드 시스템 :star:
: Columns Grid System. 다양한 너비의 블록 요소 생성

``` css title="12열 그리드 예제"
/* 12열 그리드에서 하나의 열의 너비는 100%를 12로 나눈 8.33% */
.col_1 {width: 8.33%;}
.col_2 {width: 16.66%;}
.col_3 {width: 25%;}
.col_4 {width: 33.33%;}
.col_5 {width: 41.66%;}
.col_6 {width: 50%;}
.col_7 {width: 58.33%;}
.col_8 {width: 66.66%;}
.col_9 {width: 75%;}
.col_10 {width: 83.33%;}
.col_11 {width: 91.66%;}
.col_12 {width: 100%;}
[class=*="col_"]{ /* col_1~col_12 */
    float: left;
    padding: 15px;
}
.main li:nth-child(1){color:skyblue;} /* main의 하위에 있는 li 요소 중 첫번째 요소 선택 */

...
<div class="row">
    <div class="col_6"></div>
</div>
```
- `선택자-[attribute*=value]` : 속성값 value를 포함한 요소 선택
- `선택자-:nth-child(n)` : 같은 부모를 가진 해당 요소 중 n번째 요소 선택

---
### 반응형 웹의 폰트
: px은 모니터 해상도를 기준으로 하기 때문에, 다양한 기기를 고려하는 em, rem 단위 사용

- em : 영문자 M의 너비를 1em으로 계산하여 이에 대한 상대적인 크기로 글자 크기 표현
    - 1em = 16px
    - em이 사용된 요소의 하위요소는 부모요소의 em을 상속 받아 글자 크기 지정
- rem : **브라우저의 기본 글자 크기**를 기준으로 한 상대적인 크기
    - 일반적인 브라우저의 기본 글자 크기는 `<html>` 태그에 기본으로 설정된 16px (1rem = 16px)
    - em의 상속 특징으로 인해 다양한 글자 크기 설정의 어려움을 해결한 단위

``` css
.title1 {font-size: 1.5em;}
#a {font-size: 1rem;}
```

---
## 반응형 웹 기술

### 미디어 쿼리 (Media Queries)
: 특정 미디어의 성능과 상황(=뷰포트의 크기)에 따라 특정한 CSS 적용

``` css
/* 미디어 타입이 스크린이고, 뷰포트의 최대 너비가 600 px인 경우, yellow 사용*/
@media only screen and (max-width: 600px){ 
    body { background-color: yellow;}
}
.row::after{
    content: "";
    clear: both;
    display: block;
}
a::after {content: "←";} /* 링크 걸린 글자 뒤에 화살표 추가 */
a::before {content: "→";} /* 링크 걸린 글자 앞에 화살표 추가 */
a::after {content: "";} /* 링크 걸린 글자 뒤에 빈 텍스트 (=Null) 삽입 */

img {max-width:100%;} /* image의 최대 너비 100% 설정 */
```
- `선택자-::after` : 선택된 요소 다음에 가상 요소(Pseudo-Element) 생성
    - 보통 content 속성과 같이 사용
    - content 속성을 통해 주로 장식용 텍스트 콘텐츠 삽입

### 플렉서블 박스
: Flexible box, 가변적인 박스를 쉽게 생성

가변 그리드, 인라인/블록, float 속성과 비교되는 장점:

- 콘텐츠를 수직방향으로 쉽게 중앙 정렬 가능
- 뷰포트의 너비에 따라 요소의 배치순서를 달리할 수 있음
- 박스 내 요소의 여백과 배치를 자동으로 조절 가능

``` css
.container {display: flex;}
...
<div class="container">
    <div class="items"></div>
    <div class="items"></div>
    <div class="items"></div>
</div>
```





---






---
!!! quote
    - HTML/CSS 입문 예제 중심 (지은이: 황재호 | 출판사: 인포앤북(주))
    - openAI
    - [W3Schools](https://www.w3schools.com/html/html_layout.asp)