# HTML
: HyperText Markup Language

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
        h3 {
            color: red;
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


## 이미지
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
- loop : 무한 반복
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
``` html
<body>
    <video width="320" height="240" controls>
        <source src="https://www.youtube.com/watch?v=9bZkp7q19f0" type="video/mp4">
    </video>
</body>
```

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

## 하이퍼링크 
: 텍스트, 이미지 같은 요소에 링크를 걸어두는 것

- href : 이동할 페이지의 url 주소 설정
- `target='_black'` : 새 창에 페이지를 표시
``` html
<body>
    <p><a href="test.html">test로 가요</a></p> <!-- 텍스트+링크 -->
    <a href="test.html"><img src="image.png"></a> <!-- 이미지+링크 -->
</body>
```

---

## 폼양식
사용자가 키보드로 데이터를 입력하거나 마우스로 선택할 수 있는 서식

- value : 초기값 설정
- autofocus : 필드에 마우스 커서가 깜빡이게 함
- readonly : 필드를 읽기 모드로 설정 (입력값 수정 불가)
- disabled : 필드 비활성화
- placeholder : 값 입력의 힌트 부여

| 폼 종류 | HTML 태그와 속성 
| :-----: | :-----: | 
| 텍스트 입력 창 | `<input type="text">`
| 비밀번호 입력 창 | `input type="password"`
| 라디오 버튼 | `input type="radio"`
| 체크 박스 | `input type="checkbox"`
| 파일 | `input type="file"`
| 버튼 | `input type="submit"`<br>`input type="button"`<br>`input type="reset"`<br>`<button>`
| 선택 박스 | `<select>`, `<option>`
| 다중 입력 창 | `<textarea>`

### 텍스트 입력
``` html
<body>
    <form>
        내용 : <input type="text">
    </form>
</body>
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
        <input type="checkbox" name="fruit" checked>사과
        <input type="checkbox" name="fruit2">배
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
- `<table>` : 전체 테이블을 감싸는 태그. border는 경계선 두께 설정을 의미
- `<tr>` : 각각의 행을 나타냄
- `<th>` : 테이블의 첫번째 행에서 사용. 각 열의 제목
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
!!! quote
    - HTML/CSS 입문 예제 중심 (지은이: 황재호 | 출판사: 인포앤북(주))
    - openAI