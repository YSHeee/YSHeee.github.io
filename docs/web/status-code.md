## 1xx Information 
요청을 받았으며 프로세스를 계속 진행합니다

|    응답코드      |      의미     |       
| :-----------:  | :-----------: |
100 Continue | 진행중임을 의미하는 응답 코드. <br>지금까지의 상태는 괜찮으며 클라이언트가 계속해서 요청을 하거나 이미 요청을 완료한 경우에는 무시해도 됨을 알려준다
101 Switching Protocol | 클라이언트가 보낸 Upgrade 요청 헤더에 대한 응답으로 보내지며 서버에서 프로토콜을 변경할 것임을 알려준다
102 Processing  | 서버가 요청을 수신해 처리하고 있지만, 아직 제대로 된 응답을 반환할 수 없음을 알려준다
103 Early Hints | 주로 Link 헤더와 함께 사용되어 서버가 응답을 준비하는 동안 사용자 에이전트가 preloding을 시작할 수 있도록 한다


## 2xx Successful
사용자 요청을 서버가 성공적으로 수신•승인 및 처리했습니다

|    응답코드      |      의미     |       
| :-----------:  | :-----------: |
200 OK | 요청이 성공적으로 이루어졌습니다<br>• GET : 리소스를 불러와 메시지 바디에 전송됨<br>• HEAD : 개체 헤더가 메시지 바디에 존재함<br>• PUT 또는 POST : 수행 결과에 대한 리소스가 메시지 바디에 전송됨<br>• TRACE : 메시지 바디는 서버에서 수신한 요청 메시지를 포함하고 있음
201 Created | 클라이언트 요청이 성공적이었으며 그 결과로 새로운 리소스가 생성되었습니다<br>(일반적으로 POST 또는 일부 PUT 요청 이후에 따라오는 코드)
202 Accepted | 요청은 수신됐으나 아직 처리되지 않았습니다<br>다른 프로세스에서 처리하고 있거나 또는 서버가 요청을 다루고 있거나 배치 프로세스를 하고 있는 경우를 위해 만들어진 코드<br>(PUT, DELETE, PATCH)
203 Non-Authoritative Information | 돌려받은 메타 정보가 origin 서버와 일치하지 않지만, 로컬 또는 서드파티 복사본에서 모아졌음을 의미한다
204 No Content | 사용자 요청을 성공적으로 완료했으나 상태 메시지 반환은 없음을 의미한다
205 Reset Content | 요청을 완수한 이후, 사용자 에이전트에게 이 요청을 보낸 문서 뷰를 리셋하라고 알려주는 응답 코드
206 Partial Content | 클라이언트에서 복수의 스트림을 분할 다운로드 하고자 범위 헤더를 전송했기 때문에 사용되는 응답 코드.<br>클라이언트가 이어받기를 시도하면, 이에 대한 206 응답 코드와 함께 Range 헤더에 명시된 데이터의 부분(byte)부터 전송을 시작한다
207 Multi-status (WebDAV) | 여러 리소스가 여러 상태 코드인 상황이 적절한 경우, 해당되는 정보를 전달한다
208 Already Reported (WebDAV) | propstat 응답 속성으로 동일 컬렉으로 바인드된 내부 멤버를 반복적으로 열거하지 않기 위해 사용한다
226 IM Used (HTTP Delta encoding) | 서버가 GET 요청에 대한 리소스의 의무를 다 했고, 하나 또는 그 이상의 인스턴스 조작이 현재 인스턴스에 적용이 되었음을 알려준다


## 3xx Redirection
요청을 완료하기 위해 사용자가 추가 작업을 수행해야 합니다

|    응답코드      |      의미     |       
| :-----------:  | :-----------: |
300 Multiple choices | 사용자 요청에 대해 둘 이상의 응답이 있음을 의미한다<br>사용자 에이전트 또는 사용자는 그 중 하나를 반드시 선택해야 한다
301 Moved Permanently | 요청한 리소스가 지정된 URI로 이동되었습니다
302 Found | 요청한 리소스의 URI가 일시적으로 변경되었습니다
303 See Other | 클라이언트가 요청한 리소스를 다른 URI에서 GET 요청을 통해 얻어야 할 때, 서버가 클라이언트로 직접 보내는 응답 코드
304 Not modified | 클라이언트에게 응답이 수정되지 않았음을 알려주는 코드<br>(요청한 내용이 cache 되어 있는 경우)클라이언트는 계속해서 응답의 cache 버전을 사용할 수 있다
307 Temporary Redirect | 클라이언트가 요청한 리소스가 다른 URI에 있고, 이전 요청과 동일한 메소드를 사용해 요청해야 할 때 보내는 응답 코드.<br> 302 Found 응답 코드와 동일한 의미를 가지고 있으며, 사용자 에이전트가 반드시 사용했던 HTTP 메소드를 변경하지 말아야 한다는 점에서 차이가 있다
308 Permanent Redirect | 리소스가 HTTP 응답 헤더의 Location:에 지정된 다른 URI에 영구적으로 위치하고 있음을 의미한다<br>301 Moved Permanently 응답 코드와 동일한 의미를 가지며, 사용자 에이전트가 반드시 사용했던 HTTP 메소드를 변경하지 말아야 한다는 점에서 차이가 있다


## 4xx Client Error
잘못된 형식의 요청 또는 기타 클라이언트 문제로 인해 사용자 요청이 수행되지 않았습니다

|    응답코드      |      의미     |       
| :-----------:  | :-----------: |
400 Bad Request | 클라이언트 오류로 인해 요청을 처리할 수 없습니다<br>(잘못된 형식의 요청 등)
401 Unauthorized | 클라이언트 요청에 인증이 필요하거나 리소스에 대한 액세스가 허용되지 않았음을 의미
403 Forbidden | 클라이언트 요청은 유효하나 콘텐츠에 접근할 권리를 가지고 있지 않습니다<br>401 응답 코드와 비슷하나 클라이언트가 누군지 서버가 알고 있다는 점에서 다르다
404 Not Found | 요청한 리소스를 찾을 수 없습니다
405 Method Not Allowd | 서버가 요청 메소드를 알고 있지만, 대상 리소스가 해당 메소드를 지원하지 않음을 가리킨다
406 Not Acceptable | 서버가 server-driven content negoriation을 수행한 이후, 사용자 에이전트에서 정해진 규격에 따른 콘텐츠를 찾지 못했을 때 웹서버가 보내는 코드
407 Proxy Authentication Required | 프록시에 의해 완료된 인증이 필요합니다
408 Request Timeout | 요청을 한 지 오래된 연결이거나 클라이언트로부터 어떠한 요청이 없을 때 보내지는 응답 코드.<br>서버가 사용하지 않는 연결을 끊고 싶음을 의미한다
409 Conflict | 요청이 현재 서버의 상태와 충돌할 때 보내는 응답 코드
410 Gone | 요청한 리소스를 더 이상 사용할 수 없습니다<br>서버에서 영구적으로 삭제되었으며, 전달해 줄 수 있는 주소 역시 없을 때 사용
411 Length Required | 서버에서 필요로 하는 Content-Length 헤더 필드가 정의되지 않은 요청이 들어왔을 때, 사용하는 요청 거절 코드
412 Precondition Failed | If-Unmodified-Since또는 If-None-Match 헤더에 정의된 조건이 충족되지 않는 경우 반환하는 응답 코드
413 Payload Too Large | 요청된 엔티티가 서버에서 정의한 한계보다 큽니다
414 URI Too Long | 클라이언트가 요청한 URI가 서버가 해석 가능한 URI보다 더 깁니다
415 Unsupported Media Type | 요청한 미디어 포맷은 서버에서 지원하지 않습니다
416 Requested Range Not Satisfiable | 서버가 요청받은 범위에 대해서 서비스 할 수 없음을 나타내는 응답 코드
417 Expectation Failed | 요청의 Expect 헤더에 제공된 기대치를 서버가 충족할 수 없음을 나타내는 응답 코드
418 I'm a teapot | 서버는 커피를 찻 주전자에 끓이는 것을 거절합니다
421 Misdirected Request | 요청이 잘못된 서버에 연결되었습니다
422 Unprocessable Entity (WebDAV) | 서버가 요청된 엔티티의 콘텐츠 유형을 이해하고, 구문도 정확하지만 명령을 처리할 수 없음을 의미
423 Locked (WebDAV) | 해당 리소스는 접근이 잠겨있습니다
424 Failed Dependency (WebDAV) | 이전 요청의 실패로 인해 지금의 요청이 실패하였습니다
426 Upgrade Required | 현재 요청의 프로토콜은 거부하며, 클라이언트가 다른 프로토콜로 업그레이드 한 후에는 요청을 수행할 의향이 있습니다
428 Precondition Required | 보통 If-Match 같은 precondition header가 누락되었음을 의미한다
429 Too many Requests | 클라이언트가 일정 시간 동안 너무 많은 요청을 보냈을 때 사용
431 Request header Fields Too Large | 헤더 필드가 너무 커서 서버가 요청을 처리할 수 없습니다
451 Unavailable For Legal Reasons | 사용자가 요청한 것은 불법적인 리소스입니다 


## 5xx Server Error
클라이언트 요청은 유효하나 서버 문제로 수행되지 않았습니다

|    응답코드      |      의미     |       
| :-----------:  | :-----------: |
500 Internal Server Error | 서버가 요청을 수행할 수 없도록 하는 예상치 못한 상황이 발생했습니다.
501 Not Implemented | 서버가 클라이언트 요청에 필요한 기능을 지원하지 않습니다
502 Bad Gateway | 서버가 게이트웨이나 프록시 서버 역할을 하면서 업스트림 서버로부터 유효하지 않은 응답을 받았음을 의미
503 Service Unavailable | 서버가 요청을 처리할 준비가 되지 않았습니다. <br> 보통 서버가 많은 사용량으로 인해 중단되었거나 과부하되어 현재 요청을 처리할 수 없음을 의미
504 Gateway Timeout | 서버가 게이트웨이 또는 프록시 역할을 하는 동안 업스트림 서버로부터 제때 응답을 받지 못했음을 나타낸다
505 HTTP Version Not Supported | 요청에 사용된 HTTP 버전은 지원되지 않습니다
506 Variant Also Negotiates | context of Transparent Content Negotiation에서 제공
507 Insufficient Storage (WebDAV) | 서버가 요청을 수행하는 데 필요한 representation을 저장할 수 없습니다
508 Loop Detected (WebDAV) | 서버가 요청을 처리하는 동안 무한 루프를 감지했습니다
510 Not Extended | 서버가 요청을 수행하기 위해서는 요청에 대한 추가 확장이 필요합니다
511 Network Authentication Required | 클라이언트가 네트워크 액세스를 얻기 위해 인증을 받아야 할 필요가 있음을 의미

-----

!!!quote
    - [1](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
    - [2](https://www.whatap.io/ko/blog/40/)


