---
date: 2023-11-02
title: MSA 교육 2차 프로젝트
authors:
  - ysheee
categories:
  - MSA 교육 프로젝트
comments: true
---

한국소프트웨어산업협회 주관 [회원사 채용연계형 MSA기반 Full Stack 개발 전문가 양성과정 3차] 

2차 프로젝트 (11/14~11/23)

---
<!-- more -->

## NONOGrammers

- 팀명 : 도트리키재기 
- 팀원 : 유승희(팀장), 전승현, 송기영, 이성수

[-> 1차 프로젝트 글 보러가기](./msa-edu-1.md)

---
### **2차 프로젝트 목표**

1. Migration: MyBatis ➡️ Spring Data JPA 
2. Migration: Html+CSS+Vanila JS ➡️ Vue.js
3. REST API 구현 
4. 코드의 재사용성 및 유지보수성 향상
5. Monitoring (Log & Visualization)


<br>
**Technical Skills**

Backend 

<a href="https://spring.io/" target="_blank" rel="noreferrer">
    <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/spring/spring-original.svg" alt="spring" width="40" height="40"/>
</a>
<a href="https://spring.io/projects/spring-boot" target="_blank" rel="noreferrer">
    <img src="https://noticon-static.tammolo.com/dgggcrkxq/image/upload/v1583139980/noticon/vtzecmjzn39cifnjtonx.png" alt="springboot" width="40" height="40"/>
</a>
<img src="https://noticon-static.tammolo.com/dgggcrkxq/image/upload/v1687307488/noticon/o9lxyva5z8zbwyeaxers.png" alt="jpa" width="40" height="40"/>
<a href="https://www.mysql.com/" target="_blank" rel="noreferrer">
    <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original.svg" alt="mysql" width="40" height="40"/>
</a>
:material-plus:
<img src="https://raw.githubusercontent.com/get-icon/geticon/master/icons/aws.svg" alt="aws" width="40" height="40"/>
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original.svg" alt="docker" width="40" height="40"/>
(DB는 AWS LightSail에 배포하여 사용)

Frontend 

<a href="https://developer.mozilla.org/en-US/docs/Web/CSS" target="_blank" rel="noreferrer">
    <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original.svg" alt="css3" width="40" height="40"/>
</a>
<a href="https://developer.mozilla.org/en-US/docs/Glossary/HTML5" target="_blank" rel="noreferrer">
    <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original.svg" alt="html5" width="40" height="40"/>
</a>
<a href="https://vuejs.org/" target="_blank" rel="noreferrer">
    <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/vuejs/vuejs-original.svg" alt="vuejs" width="40" height="40"/>
</a>
<a href="https://tailwindcss.com/" target="_blank" rel="noreferrer">
    <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/tailwindcss/tailwindcss-plain.svg" alt="tailwindcss" width="40" height="40"/>
</a>


<br>
**역할 분담**
: Vue.js + JPA 전환과 이전에 구현하지 못했던 기능을 구현하는 것에 우선순위를 두고, 
<br>새로 개발할 기능 중 구현하고 싶은 작업들을 각각 선택하는 것으로 역할을 분담했습니다.

- 공통 작업 : JPA, Vue.js 전환
- 개인 작업 : 구현하고 싶은 기능, 이전에 구현하지 못했던 기능
- 새로운 기능 추가 : 관리자, 친구 시스템, 채팅, 대결 시스템, 알림 등

![task](./images/edu-proj-2-task.png)

---
### **2차 프로젝트 종료 (11/23)**

**새로운 변화**
: `git Hooks with husky`를 통한 Commit Convention 실수 방지

약속된 Commit Convention을 지키지 않거나, Commit message에 Jira의 Task 번호를 작성하는 것을 잊지 않도록 강제하는 환경을 가졌습니다

**개발 일정**
: 짧은 개발 일정, 그리고 migration의 어려움을 겪게되면서 
<br> 새로운 기능 추가는 미루고, migration에 집중했습니다

![time](./images/edu-proj-2-time.png)

**Repository 구조**
: \- vue.js를 사용하게 되면서 Front 레포지토리를 따로 생성하였습니다
<br>- service 레이어를 구축하여 코드 로직을 분리하였습니다

=== "nonogrammers-back"
    ``` css
    project-root/
    │
    ├── src/
    │   ├── main/
    │   │   ├── java/com/dottree/nonogrammers/
    │   │   │   ├── config/
    │   │   │   │   ├── jwt/
    │   │   │   │   │    ├── JwtAuthenticationFilter.java
    │   │   │   │   │    ├── JwtAuthorizationFilter.java
    │   │   │   │   │    └── JwtProperties.java
    │   │   │   │   ├── CorsConfig.java
    │   │   │   │   ├── MyConfig.java
    │   │   │   │   ├── RedisUtil.java
    │   │   │   │   └── SpringSecurityConfig.java
    │   │   │   ├── controller/
    │   │   │   │   ├── MainController.java
    │   │   │   │   ├── MyPageController.java
    │   │   │   │   ├── PostController.java
    │   │   │   │   └── UserController.java
    │   │   │   ├── dao/
    │   │   │   │   ├── CommentMapper.java
    │   │   │   │   ├── MainMapper.java
    │   │   │   │   ├── PostMapper.java
    │   │   │   │   └── UserMapper.java
    │   │   │   ├── repository/
    │   │   │   │   ├── PostRepository.java
    │   │   │   │   ├── ...
    │   │   │   │   └── UserRepository.java
    │   │   │   ├── entity/
    │   │   │   │   ├── Board.java
    │   │   │   │   ├── ...
    │   │   │   │   └── User.java
    │   │   │   ├── domain/
    │   │   │   │   ├── UserDTO.java
    │   │   │   │   ├── ...
    │   │   │   │   └── PostDTO.java
    │   │   │   ├── service/
    │   │   │   │   ├── UserService.java
    │   │   │   │   ├── ...
    │   │   │   │   └── PostDTO.java
    │   │   │   └── NonogrammersApplication.java
    │   │   ├── resources/
    │   │   │   ├── static/
    │   │   │   │   └── images/
    │   │       └── banner.txt
    │   └── test/java/com/dottree/nonogrammers/NonogrammersApplicationTests.java  
    ├── gradle/wrapper/
    ├── README.md
    ├── ...
    └── .gitignore
    ```
=== "nonogrammers-front"
    ``` css
        project-root/
        │
        ├── src/
        │   ├── assets/
        │   │   ├── css/
        │   │   ├── fonts/
        │   │   ├── images/
        │   │   └── ...
        │   ├── components/
        │   │   ├── user/
        │   │   ├── nono/
        │   │   ├── ...
        │   │   └── Header.vue
        │   ├── js/
        │   │   ├── axiosHandler.js
        │   │   ├── ...
        │   │   └── nonodot.js
        │   ├── pages/
        │   │   ├── Login.vue
        │   │   ├── Join.vue
        │   │   ├── ...
        │   │   └── MyPage.vue
        │   ├── router/
        │   │   └── index.js
        │   ├── stores/
        │   │   ├── auth.store.js
        │   │   └── mypage.js
        │   ├── main.js
        │   └── App.vue
        ├── .env
        ├── package.json
        ├── index.html
        ├── tailwind.config.js
        ├── postcss.config.js    
        ├── ...
        └── .gitignore
    ```

---
### **구현 기능**

#### MyBatis + JPA


#### JPA

#### Spring Security 적용 (Session)
(11/3 ~ 11/9) 

thymeleaf

#### JWT 인증 

!!! note
    **[jjwt](https://github.com/jwtk/jjwt)  VS  [java-jwt](https://github.com/auth0/java-jwt)**



#### 이메일 인증 및 검증



#### Vue.js 컴포넌트


#### axios interceptor


#### vue-router beforeEach


---
### **아쉬운 점**

- Swagger 또는 Postman API 명세서를 작성할 계획이었는데, 시간상 하지 못한 점
- 구현하지 못한 계획이 많음


--- 
!!! quote
    **Document**

    - [Pinia](https://pinia.vuejs.kr/introduction)
    - [Axios](https://axios-http.com/kr/)
    - [Vue.js](https://ko.vuejs.org/guide/introduction.html)
    - [jjwt](https://github.com/jwtk/jjwt)

    **Post**

    - [JASON - pinia+jwt](https://jasonwatmore.com/post/2022/05/26/vue-3-pinia-jwt-authentication-tutorial-example)
    - [Goorm - JWT](https://ws-pace.tistory.com/254)

    **Book**

    - 스프링 부트 3 백엔드 개발자 되기 (지은이: 신선영 | 출판사: 골든래빗)