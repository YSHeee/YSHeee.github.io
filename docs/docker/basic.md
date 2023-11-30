# Docker <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original.svg" alt="docker" width="40" height="40"/>
: 2013년 3월에 발표된 컨테이너 기반의 오픈소스 가상화 플랫폼
<br> 데이터 또는 프로그램을 각각 독립된 환경에 격리시키는 기능을 제공하는 소프트웨어

## VM vs Docker







!!! note
    **컨테이너 기반 기술 Isolation**

    - 리눅스 커널에서 제공하는 기능
    - 하나의 시스템에서 프로세스를 격리시킬 수 있는 가상화 기술

    **컨테이너 런타임**
    : 컨테이너를 사용할 때 필요한 도구, 대표적으로 도커










---
### yaml/yml
: Yaml Ain't Markup Language, 2001년 Clark Evans에 의해 제안된 새로운 포매팅 방식

옛날 Windows에서 파일 확장자가 세 글자로 제한되는 특성으로 인해 `.yml`으로도 사용되었으나 요즘은 그러한 OS 시스템 수준의 규격이 없으니 `.yaml`을 사용한다

JSON은 중괄호를 이용해 데이터 간의 구분을 표현하지만, yaml은 들여쓰기로 데이터를 구분한다

- 따옴표 : 작은 따옴표, 큰 따옴표, 따옴표 없음 전부 인식 가능하지만 콜론기호(:)가 들어간 문자열이 값으로 사용되는 경우엔 따옴표를 사용해야 한다
``` yaml
name: 둘리
address1: 서울시 
address2: "도봉구 쌍문동" 
address3: '마이콜 옆집' 
ratio1: "1:2"
ratio2: '1:2'
```
- 작은 따옴표와 큰 따옴표의 차이점 : 이스케이프 문자를 구분할 때, 둘을 구분해서 사용한다
``` yaml
string1: "\t tab \n NL" # 큰 따옴표 : escape sequence 처리, 개행 문자 인식
string2: '\t tab \n NL' # 작은 따옴표 : 일반 문자로 \n 인식
```
- 배열 & 리스트
``` yaml
members: [둘리, 또치, 도우너]

또는 

members:
    - 둘리
    - 또치
    - 도우너
```
- 객체 배열 : 복잡한 구조체의 리스트 표현
``` yaml
students:
    - name: 둘리
    major: 국어
    age: 10
    - name: 또치 
    major: 
    영어 age: 11
```
- 단순 원소 배열과 객체 원소 배열
``` yaml
# 단순 원소 배열
members:
    - 둘리
    - 또치
    - 도우너

# 객체 원소 배열
members:
    - class1: 둘리
    - class2: 또치
    - class3: 도우너
```
- Boolean : yes, no, true, false (대소문자 구분 X)
- 텍스트 Multi Line : 개행 문자열 표현
    - `>` Folded block scalar : 개행 문자를 한 개의 공백 문자로 치환, 빈 줄 하나가 단독으로 있는 경우에만 개행문자로 치환한다
    ``` yaml
    # 맨 마지막은 자동으로 개행 처리 (paragraph1: "abc def ghi\naab\n")
    paragraph1: > 
        abc
        def 
        ghi

        aab

    # 맨 끝에 개행 문자를 포함시키지 않음 (paragraph1: "abc def ghi\naab\n")
    paragraph1: >- 
        abc
        def 
        ghi

        aab
    ```
    - `|` Literal block scalar : 개행 문자가 인식될 때마다 개행문자로 처리
    ``` yaml
    # 맨 마지막은 자동으로 개행 처리 (paragraph3: "abc\ndef\nghi\n\naab\nccc\n")
    paragraph1: |
        abc
        def 
        ghi

        aab

    # 맨 끝에 개행 문자를 포함시키지 않음 (paragraph3: "abc\ndef\nghi\n\naab\nccc")
    paragraph1: |- 
        abc
        def 
        ghi

        aab
    ```
- Multiple Documents : 두 가지 파일의 데이터를 하나의 파일로 포함시켜 표현해주는 기능
``` yaml
spring: 
    profiles: dev
    ...
---
spring:
    profiles: prod
    ...
```
 

---
!!! quote
    - 김정현 강사님
    - 그림과 실습으로 배우는 도커&쿠버네티스 (지은이: 심효섭 | 출판사: 위키북스)
    - [POST: 쿠버네티스 알아보기 1편: 쿠버네티스와 컨테이너, 도커에 대한 기본 개념](https://www.samsungsds.com/kr/insights/220222_kubernetes1.html)

!!! info
    - Docker document :material-arrow-right-bold:
    [Docs-Link](https://docs.docker.com/)
    - Docker-hub :material-arrow-right-bold:
    [Hub-Link](https://hub.docker.com/)
    - Docker Samples
    [github](https://github.com/dockersamples)
    - Compose Samples
    [awesome-compose](https://github.com/docker/awesome-compose)
