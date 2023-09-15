# HTML5
: HyperText Markup Language
<br> 1991년 처음 HTML 이라는 용어로 사용되었고, 1995년 W3C에서 정식으로 HTML2.0 표준안 발표
<br> 2014년 HTML5의 최종 권고안이 확정되어 최신 표준으로 지정되었다

:material-book-plus: HTML5는 '(문서의 내용과 구조 = HTML 태그(시멘틱 태그)) + (스타일 표현 = CSS) + (동작 구현 = JavaScript)'으로 처리하게 하여 웹 표준에 기반한 웹사이트를 개발하도록 지원하며 브라우저/디바이스에 무관한 웹사이트 개발을 가능케 함

- W3C의 HTML WG을 통해 만들어지고 있는 차세대 마크업 언어 표준
- 문서 작성 중심으로 구성된 기존 표준 + 그림, 동영상, 음악 등을 실행하는 기능 + 다양한 기능의 클라이언트 애플리케이션 구현 API
- 플랫폼 중립적이며 특정 디바이스에 종속되지 않음
- Active-X를 설치하지 않아도 동일한 기능 구현 가능

``` html
<!-- 
    주석입니다!
-->
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>TITLE</title>
    <style>
        body{
            background-color: white;
        }
        p{
            background-color: blue;
        }
    </style>
</head>

<body>
    <h1>HTML</h1>
</body>

</html>
```

- `<!DOCTYPE html>` : 현재 HTML 문서의 버전이 HTML5임을 나타내는 행
- `<html>`, `</html>` : HTML 문서의 시작과 끝
- `<body>`, `</body>` : 브라우저 메인 창에 들어가는 내용
- `<head>` : 한글 문자셋이나 웹 브라우저의 제목 등을 설정하는 데 사용
- `<meta>` : 데이터를 표현하는 메타데이터를 설정할 때 사용<br>HTML 문서가 UTF-8로 설정되면 HTML 문서 파일을 텍스트 에디터로 저장할 때 반드시 UTF-8 방식으로 저장해야 함
- `<style>` : HTML 문서를 꾸미는 CSS 코드가 삽입되는 곳. `<head>` 태그 내에 삽입되어야 함
- `<title>` : 웹 페이지의 제목 설정. `<head>` 태그 내에 삽입되어야 함
- `<!--`, `-->` : 주석


---
## 텍스트

### 글 제목 `<h1> ~ <h6>`
``` html
<body>
    <h1>HTML</h1> <!-- 가장 큰 크기-->
    <h2 style="font-size:30px">HTML</h2> <!-- 글자 크기 변경-->
    <h3 style="color:blue">HTML</h3> <!-- 글자 색상 변경-->
    <h4>HTML</h4>
    <h5>HTML</h5>
    <h6>HTML</h6>
</body>
```

### 단락 `<p>`
``` html
<body>
    <p>paragraph</p> <!-- 각 단락 사이에는 빈 줄이 자동으로 생성되어 있음-->
    <p>paragraph2</p>
</body>
```

### 줄바꿈 `<br>`
``` html
<body>
    <p>paragraph<br>
    paragraph2</p>
</body>
```

### 구분선 `<hr>`
### _강조 텍스트_ `em`
### **강조 텍스트** `strong`

### HTML 특수 문자
공백, `<`, `>`, `"`, `'` 등

| HTML 표기 | 기호 | 설명 |
| :-----: | :-----: | :-----:|
| `&nbsp;`| | 공백
| `&lt;`| < | '~보다 작다', less than
| `&gt;`| > | '~보다 크다', greater than
| `&amp;`| & | Ampersand
| `&quot;`| " | 쌍따옴표
| `&#039;`| ' | 단따옴표
| `&copy;`| | 저작권 기호

---
## 이미지
- `<figure>`, `</figure>` : 그림이나 비디오 같은 멀티미디어 요소
- `<figcaption>`, `</figcaption>` : Figure 요소에 대한 제목 (개략적 설명)
``` html
<body>
    <!-- title: 마우스 커서를 올렸을 때, 나타나는 이미지 제목-->
    <img src="googlelogo.png" alt="구글 로고" title="구글"> <!-- 원본 이미지의 가로 세로 비율과 동일하게 자동 계산된 크기대로 표시-->
    <img src="lactofit.png" alt="락토핏" width="200" height="200"> <!-- 너비, 높이 200픽셀 -->
</body>
```

### 웹의 이미지 파일 포맷

| 이미지 포맷 | 확장자 | 설명 |
| :-----: | :-----: | :-----:|
| JPG | .jpg | 24비트 트루 컬러, 손실 압축, 고화질을 유지하면서 고압축 가능, 비교적 파일 크게를 작게할 수 있음
| PNG | .png | 24비트 트루 컬러, 무손실 압축, jpg에 비해 압축 효율은 떨어지나 휴대폰 등에서 이미지 확대 시 고화질 유지 가능
| GIF | .gif | 8비트(256컬러)지원, 무손실 압축, 파일 크기가 작음
| SVG | .svg | 벡터 그래픽 포맷, 확대 시 화질 손상 없음


## 오디오
- controls : 화면에 플레이어 표시
- autoplay : 자동재생 (크롬은 허용x)
- loop : 반복 재생 횟수 지정
``` html
<!-- 화면에 나타난 오디오 플레이어의 재생 버튼을 클릭하면, 오디오 파일 재생 -->
<body>
    <audio src="song-1.mp3" controls autoplay loop></audio>
    <audio controls autoplay loop>
        <source src="song-1.mp3" type="audio/mpeg">
    </audio>
</body>
```


## 비디오
- controls : 화면에 플레이어 표시
- autoplay : 자동재생 (크롬은 허용x)
- loop : 반복 재생 횟수 지정
- poster : 동영상이 화면에 나타나지 않을 때 대신 표시할 그림 지정
- preload : 동영상이 백그라운드에서 다운로드되어 재생 단추를 눌렀을 때 재생
- width : 동영상 화면 너비 지정
- height : 동영상 화면 높이 지정
- **iframe** : youtube 영상을 끌어오는 태그 
``` html
<body>
    <video width="320" height="240" controls>
        <source src="https://www.youtube.com/watch?v=9bZkp7q19f0" type="video/mp4">
    <iframe width="677" height="400" src="https://www.youtube.com/video" title="YouTube video player"></iframe>
    </video>
</body>
```

---
## 목록

### 순서없는 목록 Unordered List `<ul>`, `<li>`
- `<ul>` : 목록의 시작과 끝
- `<li>` : 목록의 각 항목
``` html
<body>
    <ul>
        <li>1</li>
        <li>2</li>
    </ul>
</body>
```
### 순서있는 목록 Ordered List `<ol>`, `<li>`
1. `<ol>`
2. `<li>`
``` html
<body>
    <ol>
        <li>1</li>
        <li>2</li>
    </ol>
</body>
```

---
## 하이퍼링크 
: 텍스트, 이미지 같은 요소에 링크를 걸어두는 것

- href : 이동할 페이지의 url 주소 설정
- title : 마우스 커서를 올렸을 때, 나타나는 제목
- `target='_black'` : 새 창에 페이지를 표시
``` html
<body>
    <p><a href="test.html" title="하이퍼링크에요">test로 가요</a></p> <!-- 텍스트+링크 -->
    <a href="test.html"><img src="image.png"></a> <!-- 이미지+링크 -->
</body>
```

---
## 폼양식
사용자가 키보드로 데이터를 입력하거나 마우스로 선택할 수 있는 서식

- `form ation="URL" method="get|post"` : 폼 데이터를 서버로 보낼 때 해당 데이터가 도착할 URL 
- value : 초기값 설정
- readonly : 필드를 읽기 모드로 설정 (입력값 수정 불가)
- disabled : 필드 비활성화
- checked : 선택된 채로 시작 (라디오 버튼, 체크 박스)
- autocomplete : 자동완성제어기능(default: on)
- autofocus : 웹페이지 로딩 완료시 자동으로 포커스 이동 (필드에 마우스 커서가 깜빡이게 함)
- min, max, step : 입력 값 제한 (date, month, week, time, number, range일 경우)
- placeholder : 필드 안에 힌트 내용 표시. 값을 입력하면 핀트표시는 자동으로 사라짐
- required : 값이 입력되었는지 브라우저에서 체크
- multiple : 다중 파일 업로드를 처리하려는 경우 사용 (file 타입일 경우)

| 폼 종류 | HTML 태그와 속성  | 특징 |
| :-----: | :-----: | :-----: |
| 텍스트 입력 창 | `<input type="text">` | maxlength
| 비밀번호 입력 창 | `input type="password"` |
| 라디오 버튼 | `input type="radio"` |
| 체크 박스 | `input type="checkbox name="" value="""` | value 필수
| 파일 | `input type="file" name="files" multiple` |
| 버튼 | `input type="submit"`<br>`input type="button"`<br>`input type="reset"`<br>`<button>` | input 대신 button도 가능
| 선택 박스 | `<select>`, `<option>` |
| 다중 입력 창 | `<textarea>` |
| 이메일 입력 | `<input type="email">` | 서버로 전송시 이메일 형식 자동 체크 
| 웹사이트 주소 입력 | `<input type="url">` | url 문자열에 부합되는지 확인 <br> **유효성 검증은 안함**
| 스핀 박스로 숫자 입력 | `<input type="number">`| min, max, step:간격, value:초기값<br>숫자만 입력 가능
| 슬라이드 막대로 숫자 입력 | `<input type="range">` | min, max, step, value 
| 검색 상자 | `<input type="search">` | 검색어를 입력하면 오른쪽에 x가 표시됨 
| 날짜 선택 | `<input type="date">` <br> `<input type="datetime-local">` <br>`<input type="month">` <br> `<input type="week">` <br> `<input type="time">` | 달력에서 날짜 선택하거나 스핀 박스에서 시간 선택 
| 색상 선택 | `<input type="color">` | 색상 선택 상자 표시
| 전화번호 입력 | `<input type="tel">` | 정규표현식으로 패턴 설정 가능<br>(pattern="[0-9]{2,3}-[0-9]{3,4}-[0-9]{4}")

 
### 텍스트 입력
==="Example1"
    ``` html
    <body>
        <form action="URL">
            내용 : <input type="text">
        </form>
    </body>
    ```
==="Example2-List"
    ```html
    <!-- 자주 선택되는 항목을 제시해줄 뿐, 리스트 외 데이터도 입력 가능 -->
    <li>
        <label for=favorite_star>좋아하는 연예인</label>
        <input id=favorite_star name=favorite_star type=text list=favorite_star_list>
        <datalist id=favorite_star_list>
            <option value=아이유>
            <option value=뉴진스>
            <option value=NCT>
            <option value=태연>			
        </datalist>
    </li>
    ```

### 비밀번호 입력
``` html
<body>
    <form>
        비밀번호 : <input type="password"> <!-- 입력되는 데이터가 감추어짐 -->
    </form>
</body>
```

### 라디오 버튼 : 하나 선택
- checked : 선택된 채로 시작
``` html
<body>
    <form>
        내용 : <input type="radio" name="value" checked> 예 <!-- 항목들 중 하나 선택 -->
        <input type="radio" name="value"> 아니오 <!-- 하나의 라디오 버튼 그룹은 같은 name 속성값 설정 -->
    </form>
</body>
```

### 체크 박스 : 중복 선택
- checked : 선택된 채로 시작
``` html
<body>
    <form>
        <input type="checkbox" name="fruit" value="f1"checked>사과
        <input type="checkbox" name="fruit" value="f2">배
    </form>
</body>
```

### 파일
: 첨부파일 업로드
``` html
<body>
    <form>
        <input type="file" name="file" id="file">
    </form>
</body>
```

### 버튼
- value : 버튼에 표시되는 글자
``` html
<body>
    <form>
        <input type="submit" value="Submit!"> <!-- 버튼 클릭 시 action 속성에 명시된 insert.php 페이지로 이동함으로써 DB에 저장 -->
        <input type="button" value="버튼" onclick="alert('버튼을 눌렀습니다.')"> 
        <input type="reset" value="Reset!"> <!-- 버튼 클릭 시 입력한 내용이 모두 삭제되어 초기화됨 -->
        <button type="submit|button|reset" ...> <!-- input 대신 button도 가능 -->
    </form>
</body>
```

### 선택 박스 `<select>` `<option>`
: 마우스를 이용하여 선택 박스의 목록 중 하나 선택
``` html
<body>
    <form>
        이메일 : <input type="text" name="email" value="이메일을 입력하세요.">@
        <select>
            <option>naver.com</option>
            <option>gmail.com</option>
            <option>daum.net</option>
        </select>
    </form>
</body>
```

### 다중 입력 창 `textarea`
: 사각형 박스 형태의 폼으로써 여러 줄의 데이터 입력 가능

- cols : 한 줄에 입력 가능한 글자 수. 창의 너비 설정
- rows : 입력 가능한 줄의 수. 창의 높이 설정
``` html
<body>
    <form>
        <textarea name="description" cols="80" rows="50" placeholder="description"></textarea>
    </form>
</body>
```

---
## 테이블 

### 테이블 생성
- `<table>` : 전체 테이블을 감싸는 태그. 
    - border는 경계선 두께 설정을 의미 (`border=1`은 있어야 경계선 생김)
- `<tr>` : 각각의 행을 나타냄
- `<th>` : 테이블의 첫번째 행에서 사용. 각 열의 제목 (가운데 정렬, bold체)
- `<td>` : 각각의 셀 표현
``` html
<body>
    <table border="2">
        <tr>
            <th>이름</th>
            <th>나이</th>
            <th>성별</th>
        </tr>
        <tr>
            <td>홍길동</td>
            <td>20</td>
            <td>남</td>
        </tr>
    </table>
</body>
```

### 열/행의 병합
- colspan : 테이블 열 병합
- rowspan : 테이블 행 병합
``` html
<body>
    <table border="2">
        <tr>
            <th>이름</th>
            <th>년도</th>
            <th colspan="2">사용여부(깃허브/깃랩)</th> <!-- 두 개의 열을 하나로 합침 -->
        </tr>
        <tr>
            <td rowspan="2">yshee</td>
            <td>2023</td>
            <td>O</td>
            <td>X</td>
        </tr>
        <tr>
            <td>2022</td> <td>O</td> <td>X</td>
        </tr>
    </table>
</body>
```

---
## 폼 꾸미기
``` html
    <style>
        li {list-style: none;}/* 목록의 글머리 기호 삭제 */
        h3, #title {text-align: center;}
        #title {color: red;}
        .cols li {display: inline-block;} /* 클래스 cols 하위의 li 요소를 인라인-블록으로 설정 */
        .hello {vertical-align:top} /* 수직방향 정렬 */
        #buttons button {
            width: 100px;
            height: 50px;
            background-color: #eee;
            border: 1px solid #aaa;
            border-radius: 10px;}
    </style>
```

---
## 그 외

### 박스 
- `<fieldset>`, `</fieldset>`
- `<legend>`, `</legend>`
``` html
<fieldset>
	<legend>필수 항목</legend>
</fieldset>
```

### `<label>`
- 사용자 인터페이스 요소의 라벨을 정의할 때 사용
- `<button>`, `<input>`, `<meter>`, `<output>`, `<progress>`, `<select>`, `<textarea>`에 사용
```html
<label for=size>내용</label>
```

### 링크 걸린 글자 꾸미기
: `<a>` 태그로 링크가 걸린 글자 색상과 글자 스타일 등을 설정
``` html
<style>
    a:link, a:visited, a:hover, a:active {
        color: black;
        text-decoration: none;
    }
</style>
```


---
## NOTE



---
!!! quote
    - HTML/CSS 입문 예제 중심 (지은이: 황재호 | 출판사: 인포앤북(주))
    - openAI