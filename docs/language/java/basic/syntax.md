# Basic Syntax

### 자바 프로그램
- 한 개 이상의 클래스(class)로 구성
- 클래스는 한 개 이상의 필드(Field)나 메소드(Method)로 구성
- 자바 클래스 파일(.java)에 public 클래스가 존재하면, **해당 소스파일의 이름은 반드시 public 클래스의 이름과 같아야** 하며,
- public 클래스는 자바 클래스 파일마다 단 **한 개**만 가질 수 있다

###  `main()` 메소드
- 자바 프로그램이 실행되면 제일 먼저 main() 메소드를 찾아 그 안의 모든 명령문을 차례대로 실행
- 하나의 자바 프로그램에는 main() 메소드를 가지는 클래스가 **반드시 하나 존재**해야 한다
``` java
public class Example {
	public static void main(String[] args) {
        System.out.println("Hello world"); // 데이터를 출력한 후 줄바꿈까지 진행
    }
}
```

### 명령문 (Statement)
: 자바 프로그램의 동작을 명시하고, 이러한 동작을 컴퓨터에 알려주는 데 사용되는 문장
<br> 자바의 모든 명령문은 세미콜론(;)으로 끝남

### 주석 (Comment)
: 코드에 대한 이해를 돕는 설명을 적거나 디버깅을 위해 작성하는 메모

- `//` : 한 줄 주석
- `/* */` : 여러 줄 주석
- `/* // */` : 여러 줄 주석안에 한 줄 주석 포함 가능

### 자바 표준 입출력 클래스
: System 클래스에 정의된 표준 입출력을 위한 클래스 변수(static variable)

- System.in
- System.out
- System.err

### Running
- `.java` : 자바소스코드
- `.class` : 자바실행파일
- `.jar` : 여러 개의 클래스들을 하나의 파일로 압축한 것 (LIKE .zip, .tar)
    - `jar cvf xxx.jar *.class` : 압축 파일 생성
    - `jar tvf xxx.jar` : 파일 확인
    - `jar xvf xxx.jar` : 압축 해제
- javac : 
- javap : 
```bash
java package.class
javac package.class.java
```

### Java 8 변경 사항 [tcpschool](https://www.tcpschool.com/java/java_intro_java8)
- 람다 표현식 -> 함수형 프로그래밍
- 스트림 API -> 데이터 추상화
- java.time 패키지 -> Joda-time을 이용한 새로운 날짜와 시간 API
- 나즈혼(Nashorn) : javascript의 새로운 엔진 

### Keywords(Reserved words)
| abstract | assert | boolean | break | byte | case |
| :------: | :----: | :-----: | :---: | :--: | :--: |
| catch | char | class | const | continue | default | 
| do | double | else | enum | extends | final |
| finally | float | for | goto | if | implements | 
| import | instanceof | int | interface | long | native | 
| new | package | private | protected | public | return | 
| short | static | strictfp | super | switch | synchronized | 
| this | throw | throws | transient | try | void|
| volatile | while

---

!!! quote
    - [Java의 정석](https://github.com/castello/javajungsuk_basic/tree/master)
    - [점프 투 자바](https://wikidocs.net/book/31)
    - [TCP school](http://www.tcpschool.com/java/intro)
    - 이것이 자바다 (저자: 신용권, 임경균 | 출판사: 한빛미디어)