# etc

## Thymeleaf
: View Template Engine, 컨트롤러에서 전달받은 데이터를 추출해 동적인 페이지를 생성한다

- html 파일 내에서 태그의 속성으로 Thymeleaf 명령어 사용
- 기존 템플릿 기술들은 서버를 구동시켜야 하지만, Thymeleaf의 경우 static 파일을 사용하듯 해당 내용을 브라우저에서 바로 확인할 수 있다
    - Thymeleaf가 HTML 태그의 속성으로 작성되어 기존의 HTML구조를 건드리지 않기 때문
- Natural Template (내추럴 템플릿) : 서버를 구동하지 않으면 순수 HTML로 구성되는 정적인 페이지를, 서버를 구동하면 동적으로 페이지 생성
- default prefix : `src/main/resources/templates`
- suffix : `.html`


``` html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org"> <!-- Thymeleaf -->
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
    <!-- 서버를 기동시키지 않으면 "Hi Thymeleaf", 컨트롤러를 거치면 say가 생기므로 "안녕? 타임리프" 출력 -->
    <p><span th:text="${say}">Hi</span>Thymeleaf</p> 
    <p>[[${say}]] Thymeleaf</p>

    <!-- user.name이 있으면 value로 사용, 없으면 unico를 value로 사용 -->
    <input type="text" name="userName" value="unico" th:value="${user.name}">

    <h2>전달된 데이터 : [[${ param.pageno }]]</h2>
</body>
</html>
```

---
## Lombok
: 반복해서 구현하게 되는 메소드를 Annotation을 사용해서 자동으로 작성해주는 Java의 확장 라이브러리

주요 어노테이션

#### @NonNull 
: null을 허용하지 않는 매개변수 정의

#### @Getter, @Setter
: getter, setter 생성

#### @ToString
: ToString 메서드 생성

#### @EqualsAndHashCode
: hashCode, equals 구현

#### @NoArgsConstructor
: 매개변수가 없는 생성자 구현

#### @RequiredArgsConstructor
: final, @NonNull이 있는 필드에 값을 초기화 하는 생성자 구현

#### @AllArgsConstructor
: 모든 필드에 값을 초기화 하는 생성자 구현

#### @Data
: 다음에 제시된 모든 Annotation 을 정의한 것과 동일

- @ToString, 
- @EqualsAndHashCode
-  @Getter on all fields,
-  @Setter on all non-final fields,
-  @RequiredArgsConstructor

---
!!! quote
    - 김정현 강사님