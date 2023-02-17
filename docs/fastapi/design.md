# RestAPI Design Best Practices
![1](images/client-server.png){ style="height:90%;width:90%"} <div>
클라이언트와 서버는 서로 직접적으로 호출하지 않고, Application Programming Interface(API)라 불리는 중간자 역할의 인터페이스를 사용합니다

여기서 API는 클라이언트와 서버 간 통신을 원활하게 하는 중요한 역할을 하므로 모범 사례를 따라 잘 설계해야 합니다

잘 디자인 된 webAPI는 다음과 같은 특성을 가집니다 :

- Platform Independence<div>
ㅤ: 모든 클라이언트는 내부에서 API가 구현되는 방식에 관계 없이 API를 호출할 수 있다<div>
ㅤ: 이를 위해 Standard protocol을 사용해야 하고, 클라이언트 및 웹 서비스가 교환할 데이터 형식에 상호 동의할 수 있는 매커니즘이 있어야 한다
- Service Evolution<div>
ㅤ: Web API는 클라이언트 애플리케이션과 독립적으로 기능을 진화시키고 추가할 수 있어야 한다

## What is a REST API?
Representational State Transfer의 약자로
2000년 Roy Fielding이 제안한 웹서비스를 디자인하는 소프트웨어 아키텍처 접근 방식입니다<div>
RestAPI는 두 컴퓨터가 HTTP 통신시 같은 형식에 맞춰 통신하도록 함으로써 일관성을 부여합니다<div>
그렇기에 API는 Resetful이라는 REST 디자인 원칙을 잘 따라야 합니다

- REST<div>
ㅤ: Hypermidia 기반의 분산 시스템을 구축하기 위한 Architectural style<div>
ㅤ: 따라서 어떤 기본 프로토콜과도 독립적이며 HTTP에 연결될 필요가 없지만, 대부분의 일반적인 REST API 구현은 HTTP를 애플리케이션 프로토콜로 사용합니다

## 1. Use Json as the Format for Sending and Receiving Data

- Client-side에서 Json데이터를 올바르게 해석할 수 있도록 요청하는 동안 Response header에서 `Content-type`을 `application/json`으로 지정해야한다
- 반대로 다수의 Server-side 프레임워크에서는 `Content-type`을 자동으로 할당한다

## 2. Use Nouns instead of Verbs in Endpoints
- RestAPI를 설계할 때, Endpoint-path에 동사 사용 X. 명사를 사용함으로써 endpoint가 무슨 일을 하는지 명시해야 한다
- 이는 이미 HTTP Method를 CRUD 작업을 수행하기 위한 동사 형태로 나타내기 때문


!!! quote
    - [IBM](https://www.ibm.com/topics/rest-apis)
    - Image<div>
    • [1: madooei](https://madooei.github.io/cs421_sp20_homepage/client-server-app/)

