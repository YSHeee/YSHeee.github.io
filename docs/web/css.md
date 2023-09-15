# CSS
: Cascading Style Sheets
<br>웹페이지에서 HTML을 보조하여 글꼴, 색상 등 웹페이지를 꾸미는 데 사용
<br>모든 디자인적 요소에 사용

- :material-numeric-1-circle: `<style>`, `</style>` 태그 이용
- :material-numeric-2-circle: `<style>` 속성 이용 
: W3C의 방침인 HTML/CSS 코드 분리에 위배되므로 자주 사용하지는 않음
- :material-numeric-3-circle: 외부 CSS 파일 이용
- 주석 `/*`, `*/`
``` html hl_lines="4 6 11 14"
<head>
    <title>Test</title>
    <meta charset="utf-8">
    <link rel="stylesheet" href=".../css/bootstrap.css">
    <!-- 선택자(여기서는 h2)는 CSS로 꾸밀 영역을 선택하는 역할 -->
    <style>  
        h2 {
            color: red; /* h2 태그 영역의 글자 색상과 폰트 변경 */
            font-family: "arial";
        }
    </style>
</head>     
<body>
    <p style="color:aqua">CSS가 적용되는 단락</p>
</body>
```

### 역사
- CSS1 : 1996년 12월 출시
- CSS2 : 1998년 5월 권고안 출시
- CSS3 : 2005년 12월 5일 이후 개발 중

---
## 색상

### 배경 색상 `background-color`
``` html
<style>
    /* body : 전체 페이지 영역 */
    body{
        background-color: white;
    }
    /* p : 해당 단락의 영역 */
    p{
        background-color: blue;
    }
</style>
```

### 글자 색상 `color`
- span : 웹페이지에서 CSS를 적용하고자 하는 글자들을 선택하기 위해 사용되는 HTML 태그
``` html
<body>
    <p>
        <span style="color: red;">Hello</span>
        <span style="color: #ffffff;">World</span>
    </p>
</body>
```

---
## 글자 스타일

|  속성  |  속성값  |  의미  |
| :-----: | :-----: | :-----: |
| text-align | left, center, right | 글자 정렬
| line-height | 150%, 180% 등 | 줄 간격
| text-decoration | underline, none | 글자 장식<br>underline: 밑줄<br>none: 글자 장식 삭제
| font-family | "돋움", "맑은고딕" 등 | 글자 폰트
| font-size | 16px, 20px, 1.5em(=1.5배) 등 | 글자 크기
| font-weight | bold, normal | 글자 두께
| text-shadow | 3px 3px 5px #44444 | 글자 그림자

``` html
<style>
    p {
        color: #000000;
        line-height: 150%;
        text-align: center;
        text-decoration: underline;
        font-family: "맑은고딕";
        font-size: 20px;
        font-style: italic; font-weight: bold; /* 이탤릭체로 변경, 글자 두께  설정*/
        /* 그림자 설정 (오른쪽 그림자 길이, 아래쪽 그림자 길이, 흐린 정도, 그림자 색상) */
        text-shadow: 3px 3px 5px #223422;
    }
</style>
```

### 링크 글자 꾸미기
- link : 링크가 걸린 글자의 기본 상태
- visited : 한 번 이상 방문한 링크 글자의 상태
- hover : 마우스 포인터를 글자위에 올린(마우스 오버) 상태
- active : 마우스로 글자를 클릭한 순간의 상태
- `text-decoration:none` : 글자의 밑줄 삭제
- `<a href="#">` : 임시 링크. 실제 페이지는 이동되지 않고 마우스 포인터만 손 모양으로 변경
``` html
<style>
    a:link {color: #000000; text-decoration: none;}
    a:visited {color: #111111; text-decoration: none;}
    a:hover {color: #222222; text-decoration: none;}
    a:active {color: #333333; text-decoration: none;}
</style>
```

### 온라인 폰트 사용
- [구글 폰트](https://fonts.google.com) 에서 링크 복사
- 복사한 코드를 `<head>` 태그 내에 삽입
- Example `font-family: 'Noto Sans KR', sans-serif;`
: 사용된 폰트는 Noto Sans KR, 인터넷 문제 등으로 웹 폰트를 사용하지 못할 때에는 기본 폰트인 sans-sarif 폰트가 사용된다는 의미

---
## 박스 모델 
- margin : 경계선과 외부의 간격
- padding : 경계선과 HTML 요소 사이의 간격
- border(경계선) : HTML 요소를 둘러싼 경계선
- HTML 요소 : 텍스트, 이미지 등 웹 페이지를 구성하고 있는 요소
``` html
<style>
    p {
        margin : 10px;
        padding : 20px;
        border: solid 1px #000000; /* 실선, 두께는 1px, 색상은 black */
    }
</style>
```

### 경계선 `border`
- solid : 실선 / top : 상단
- dotted : 점선 / bottom : 하단
- dashed : 파선 / left : 좌측
- double : 이중선 / right : 우측
``` html
    <style>
        p {width: 100px;} /* HTML 요소의 너비 설정 */
    </style>
</head>     
<body>
    <!-- 3D : groove, ridge, inset, outset  -->
    <p style="border:solid 1px blue;">경계선은 실선</p>
    <p style="border-top:solid 1px blue;">상단 경계선은 실선</p>
    <p style="border-bottom:dotted 1px blue;">하단 경계선은 점선</p>
    <p style="border-left:dashed 1px blue;">좌측 경계선은 파선</p>
    <p style="border-right:double 1px blue;">우측 경계선은 이중선</p>
</body>
```

### margin 마진과 padding 패딩
**padding** 속성도 사용법이 같음 (margin을 padding으로 변경)

|  속성  |  속성값의 예 |  의미  |
| :-----: | :-----: | :-----: |
| margin | 20px | 상하좌우 마진을 모두 20px로 설정
| margin | 10px 20px | 상하단 마진을 40px, 좌우측 마진을 20px로 설정
| margin | 10px 20px 30px | 상하단 10px, 좌측 20px, 우측 30px
| margin | 10px 20px 30px 40px | 상단, 우측, 하단, 좌측 마진을 각각 10, 20, 30, 40px로 설정
| margin-top | 30px | 상단 마진을 30px로 설정
| margin-bottom | 30px | 하단 마진을 30px로 설정
| margin-left | 30px | 좌측 마진을 30px로 설정
| margin-right | 30px | 우측 마진을 30px로 설정

- 마진의 적용 순서는 상단 -> 우측 -> 하단 -> 좌측
- 마진이 중복될 때에는 큰 값을 가진 마진 하나만 적용
- 마진 초기화 `* {margin: 0; padding: 0;}`
: 요소의 편리한 배치를 위해 HTML 요소들은 기본 마진이 부여되어 있다
<br>그러나 정확한 요소 배치에는 오히려 기본 마진이 방해되므로 전체 요소의 마진을 0으로 설정한다
``` html
<style>
    * {margin: 0; padding: 0;} /* 모든 HTML 요소의 여백과 여백을 없앰 */
    p {
        margin: 10px 20px; /* 요소의 상하단 여백을 10px, 좌우 여백을 20px로 설정 */
    }
    h1 {
        /* 요소의 상하단 여백을 20px로 설정 */
        margin-top: 20px; 
        margin-bottom: 20px;
    }
</style>
```

### 박스 관련 속성
- `border-radius` : 박스 모서리를 둥글게 함
- `box-shadow` : 박스 그림자
- `<div>`, `</div>` : division. HTML 요소를 담는 박스 생성
``` html
<style>
    div {border:1px solid black;
        border-radius: 10px; /* 둥근 모서리 */
        box-shadow: 5px 5px 5px gray; /* 그림자 */
        padding: 30px;
        margin: 30px;
        width: 100px;}
</style>
```

---
## 선택자 Selector
: CSS로 꾸미고자 하는 HTML의 영역 선택
<br>`선택자 {css명령, css명령}`

|  선택자  |  사용 예 |  의미  |
| :-----: | :-----: | :-----: |
| 전체 선택자 | * | HTML 요소 전체 선택
| 태그 선택자 | p | `<p>` 태그의 영역 선택
| 그룹 선택자 | p, h3 | `<p>`,`<h3>` 태그의 영역 선택
| 아이디 선택자 | #title | 아이디 title로 지정된 영역 선택
| 클래스 선택자 | .red_bold | 클래스 red_bold로 지정된 영역 선택
| 하위 선택자 | div p | `<div>` 태그 하위의 모든 `<p>` 태그의 영역 선택


### 전체 선택자
``` html
<style>
    * {
        color: blue;
        margin:0; 
        padding:0;}
</style>
```

### 태그 선택자
``` html
<style>
    p {border:1px solid black; width:100px; height:100px;}
    h1 {border:1px solid black; width:100px; height:100px;}
    span {border:1px solid black; width:100px; height:100px;}
</style>
```

### 그룹 선택자
: 여러 선택자를 그룹으로 묶음. 콤마`,`로 구분
``` html
<style>
    h1, h2, h3, h4, h5, h6 {font-family: "Playfair Display", sans-serif}
    p, ul {font-family: "Roboto", sans-serif}
</style>
```

### 아이디 선택자
: 웹페이지에서 특정 영역 하나를 선택하여 꾸미고자 할 때 사용

- id 속성 : HTML의 특정 요소 지정에 사용
- HTML 문서 내에서 유일값이어야 함
- 아이디 선택자 `#` : 아이디 이름 앞에 샾 기호를 붙여 사용
``` html
<head>
    <meta charset="utf-8">
    <style>
        #intro {border:1px solid black; 
            width:100px; 
            height:100px;}
        #box2 {border:1px solid black;}
    </style>
</head>     
<body>
    <p id="intro">인트로입니다</p>
</body>
```
### 클래스 선택자
: 웹페이지에서 **두 군데 이상의 특정 영역**을 선택할 때 사용

- `.`
- 중복 정의 가능 
``` html
<head>
    <meta charset="utf-8">
    <style>
        .box {border:1px solid black;
            width:100px;
            height:100px;}
        .green_box {background-color:green;}
    </style>
</head>     
<body>
    <p>안녕하세요? <span class="green_box">전 초록색 박스에요</span>
        <span class="box">전 박스입니다</span>
    </p >
</body>
```
### 하위 선택자 Descendant Selector
: 특정 요소의 하위에 있는 요소들 선택
<br>선택자의 개수를 줄일 수 있어 코드가 간결해지고 가독성 향상
``` html
        <style>
            #intro {border:1px solid black; 
                width:100px; 
                height:100px;}
            #box2 {border:1px solid black;}
        </style>
    </head>     
    <body>
        <div id="intro">
            <h1>Intro</h1>
            <p>Intro입니다</p>
        </div>
    </body>
```

---
## CSS 활용

### 배경 이미지
- `background-repeat`
    - no-repeat : 배경 이미지가 반복되지 안흠
    - repeat-x : 배경이미지가 수평 방향으로 반복
    - repeat-y : 배경이미지가 수직 방향으로 반복
- `background-position`
    - left top : 배경 이미지를 좌측 상단에 배치
    - center top : 중앙 상단
    - right top : 우측 상단
    - left center : 좌측 중앙
    - center center : 한 가운데 배치
    - right center : 우측 중앙
    - left bottom : 좌측 하단
    - center bottom : 중앙 하단
    - right bottom : 우측 하단

```html
<style>
body{
    background-image: url("./image.jpg");
    /*배경 이미지가 삽입되는 영역보다 작을 경우, 수평과 수직 방향으로 반복해서 삽입*/
    background-image: url("./image.jpg");
    background-repeat: no-repeat;
    background-position: right top;
}
</style>
```

### 이미지
- opacity : 투명도
- width : n% (크기)
- transition : width 2s; (크기가 점점 커짐)

### 테이블 꾸미기

|  속성(속성값)  |  의미  |
| :-----: | :-----: | 
| `border-collapse : collapse` | 테이블의 단일 경계선 그리기 |
| border(border-top, border-bottom, border-left, border-right) | 테이블의 경계선 그리기 |
| padding(padding-top, padding-bottom, padding-left, padding-right) | 셀의 패딩 설정 | 
| width, height | 테이블의 너비와 높이 설정 | 
| text-align | 셀 내 글자 정렬 | 

``` html
<style>
    table{border-collapse:collapse; /* seperate로 설정하면 이중 경계선 */
        border-top: solid 1px black; 
        border-left: solid 1px black}
    td{border:1px solid black; text-align:center}
</style>
```

### 디스플레이
- inline 
    - HTMl 요소를 수평 방향으로 표시 (줄바꿈 x) (span 태그의 기본 속성)
    - 박스의 크기를 설정하는 width와 height 속성이 적용되지 않음
    - 상하단 마진인 margin-top과 margin-bottom 속성 적용되지 않음
- block 
    - 블록 방식으로 표시함으로써 전체 행을 차지하여 앞뒤로 자동 줄바꿈이 일어남 (수직방향 요소 배치)
    - 박스 크기 설정 가능, 모든 마진 설정 가능
- inline-block 
    - inline처럼 수평방향으로 배치하고, 줄바꿈 일어나지 않음
    - 박스 크기 설정 가능, 마진 설정 가능
- none : 해당 내용이 화면에 표시되지 않음
``` html
    <head>
        <meta charset="utf-8">
        <style>
            #one {display: inline;}
            #two {display: block;}
            #three {display: inline-block;}
            #four {display: none;} 
        </style>
    </head>     
    <body>
        <p>글자1<span id="one">첫번째입니다</span></p>
    </body>
```

| 인라인(inline) |  블록(block)  |
| :-----: | :-----: | 
| `<span>`, `<a>`, `<img>`, `<input>`, `<textarea>`, `<br>`, `<button>`, `<select>`, `<option>`, `<script>` 등 | `<div>`, `<p>`, `<h1>`~`<h6>`, `<form>`, `<table>`, `<ul>`, `<ol>`, `<li>`, `<video>`, `<header>`, `<footer>`, `<selection>` 등


---
### nth-of-type
- `nth-child(n)` : 형제 요소 중 순서에 따라 n번째를 선택하여 스타일 적용
- `nth-of-type(n)` : 같은 타입의 형제 요소 중 순서에 따라 n번째를 선택하여 스타일 적용
    - n=`odd` : 형제 요소중 홀수번째 요소 선택
    - n=`even` : 형제 요소중 짝수번째 요소 선택
    - n=`An+B` : Axn+B 계산값 대입
``` html
    <!-- 지금은 body를 부모로 두고, body 기준으로 3, 5, 8번째 행에 적용 -->
    <style>
        h2:nth-child(3) {color : green;}
        h2:nth-child(5) {color : red;}
        h2:nth-child(8) {color : blue;background-color : yellow;}
    </style>
```