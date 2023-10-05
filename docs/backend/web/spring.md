# Spring Framework
: 자바 기반의 애플리케이션 프레임워크
<br> - 엔터프라이즈급 애플리케이션을 개발하기 위한 다양한 기능 제공
<br> - 애플리케이션 개발에 필요한 기반을 제공함으로써 비즈니스 로직 구현에만 집중 가능

## 구조

### IoC 제어 역전
: Inversion of control, 객체의 관리를 컨테이너에 맡김으로써 제어권이 넘어간 것

- 일반적인 자바 개발에서는 개발자가 직접 객체를 생성 및 사용하는 등 직접 제어
- 스프링에서는 객체를 직접 생성하지 않고 객체의 생명주기 관리를 **스프링 컨테이너**에 위임
- 의존성 주입(DI), 관점지향프로그래밍(AOP) 등을 가능케 함

### DI 의존성 주입 
: Dependency Injection, 사용할 객체를 직접 생성하지 않고 외부 컨테이너가 생성한 객체를 주입받아 사용하는 방식

- 생성자를 통한 의존성 주입(객체 바인딩) Constructor injection
- 필드 객체 선언을 통한 의존성 주입 Field injection
- setter method를 통한 의존성 주입 Setter injection
- 어노테이션을 정의한 method를 이용한 의존성 주입 Method injection

=== "생성자"
    ``` java
    @Controller
    public class DIController { 
        MyService myService;

        @Autowired // 생략 가능
        public DIController(MyService myService) { 
            this.myService = myService;
        } 
    }
    ```
=== "필드 객체 선언"
    ``` java
    @Controller
    public class FieldInjectionController{
        @Autowired
        private MyService myService;
    }
    ```
=== "setter method"
    ``` java
    @Controller
    public class SetterInjectionController { 
        MyService myService;

        @Autowired // 생략 가능
        public void setMyService(MyService myService) { 
            this.myService = myService;
        } 
    }
    ```

### AOP 관점 지향 프로그래밍
: Aspect Oriented Programming, 여러 비즈니스 로직에 반복되는 부가 기능을 하나의 공통 로직으로 처리하도록 모듈화하여 삽입하는 방식

관점 : 어떤 기능을 구현함에 있어서 **핵심 기능**과 **부가 기능**으로 구분한 각각의 기능을 뜻함

|    핵심 기능    |    부가 기능    |
| :----------: | :-----------: |
| 비즈니스 로직이 처리하려는 목적 기능 | 여러 비즈니스 로직 사이에서 공통적이고 반복적으로 필요한 기능 |
| 회원서비스, 커뮤니티 서비스, 상품서비스 | 로깅, 보안, 트랜잭션 | 

구현 방법

- 컴파일 과정에 삽입
- 바이트코드를 메모리에 로드하는 과정에서 삽입 (LTW)
- 프록시 패턴 이용


---
## Spring IoC & DI

``` mermaid
graph LR
    I(IoC) --> DL(DL)
    I --> DI(DI)
    DI --> S(Setter Injection)
    DI --> C(Constructor Injection)
    DI --> M(Method Injection)
```

### Spring FW
: 프로그램에서 필요한 객체의 생성 관리, 객체를 필요로 하는 곳에 주입 및 제공한다

- **bean** : Spring FW에 의해 관리되는 Java 객체
- 스프링 컨테이너(IoC 컨테이너) : Spring FW의 구성요소
- **Spring DI** : 객체간의 결합도를 느슨하게 하는 스프링의 핵심 기술

``` java
// Spring IoC 컨테이너 초기화
ApplicationContext factory = new ClassPathXmlApplicationContext(빈설정XML파일);
ApplicationContext context = new AnnotationConfigApplicationContext(빈설정클래스객체);
((ClassPathXmlApplicationContext)factory).close();

// DL (Dependency Lookup)
타입명 bean = (타입명)context.getBean("빈이름");

// DL : 형변환 없이 UserService 타입으로 생성
UserService u2 = context.getBean("빈이름", UserService.class);
```

---
### XML 설정

#### `<bean>` 태그
: Spring IoC 컨테이너가 관리할 Bean 객체(자바 클래스) 설정

- id : 주입받을 곳에서 호출할 이름
- class : 주입할 객체의 클래스명
- factory-method : 객체 생성시 사용될 factory 메서드
- scope : Bean 객체의 유효 범위 설정 (singleton, prototype 등)

#### `<constructor-arg>` 태그
: `<bean>`의 하위태그. 다른 bean 객체 또는 값을 **생성자**를 통해 주입하도록 설정
<br> 해당 태그가 없다면, argument를 받지 않는 생성자를 호출함을 의미

- 객체 주입 : `<ref bean="bean name"/>`
- String, Primitive data 주입 : `<value>값</value>`
- 값의 타입 명시 : `type 속성`
    - `ref="bean 이름"`
    - `value="값"`

#### `<property>` 태그
: `<bean>`의 하위태그. 다른 bean 객체 또는 값을 **setter 메서드**를 통해 주입하도록 설정

- 객체 주입 : `<ref bean="bean name"/>`
- String, Primitive data 주입 : `<value>값</value>`
- 속성
    - name 속성 : 객체 또는 값을 주입할 property 이름을 설정(setter의 이름)
    - `ref="bean 이름"`
    - `value="값"`

``` xml
<!-- Example 1 : 값 주입-->
<bean id="messageBean1" class="sample1.MessageBeanImpl">
    <constructor-arg> <value>strawberry</value> </constructor-arg>	
    <property name="cost"> <value>3000</value> </property> 
</bean>	

<!-- Example 2 : 속성 -->
<bean id="f1" class="sample5.DateVo"> 
    <constructor-arg name="emp"  ref="emp1" />
    <property name="name" value="Duke" /> 
</bean>

<!-- Example 3 : factory-method -->
<bean id="test" class="sample4.AbstractTest" factory-method="getInstance"/> </beans>
```

### ANNOTATION 설정 :star:
: annotation이 적용되려면 다음과 같은 태그들이 설정 파일에 정의되어 있어야 한다

``` bash
<context:annotation-config> # @Autowired
<context:component-scan base-package="xml_name"/> # 모든 annotation
```

#### @Component
: 클래스에 선언하며, 해당 클래스를 bean 객체로 등록함
<br> - bean의 이름은 해당 클래스명(첫글자는 소문자로 변경) 사용
<br> - default 범위는 singleton, **@Scope**를 사용하여 지정

#### @Scope
: bean의 범위 지정, default는 singleton
<br> - prototype, singleton, request, session, globalSession

``` java
@Component
@Scope(value="prototype") // <bean id="" class="" scope="prototype" />
public class Worker { ... }
```

#### @Autowired
: 의존관계를 자동으로 설정할 때 사용, **생성자, 필드, 메서드** 세 곳에 적용 가능
<br> - 주입 가능한 빈 객체가 1개인 경우, 타입을 이용한 프로퍼티 자동 설정기능 제공
<br> - 주입 가능한 빈 객체가 2개 이상인 경우, 멤버 변수명과 동일 이름으로 생성된 빈 객체를 찾아 주입

#### @Qualifier
: 동일 타입의 bean 중, **특정 이름의 bean**으로 주입하려는 경우 사용
<br> 주입이 필수가 아닌 경우에는 `@Autowired(required=false)` (default=true)

``` java
@Autowired
@Qualifier("mytest")
private Test test1;
```

#### @Resource
: 어플리케이션에서 필요로 하는 자원을 자동 연결할 때 사용. 의존하는 Bean 객체 전달

- @Autowired와 기능은 동일하지만
    - @Autowired는 타입으로 연결(by type) 
    - @Resource는 이름으로 연결(by name)
- 설정 파일에서 `<context:annotation-config>` 태그를 사용해야함
- name 속성에 자동으로 연결될 Bean 객체의 이름 입력 `@Resource(name="testDao")`

#### @Inject
: JSR-330 표준 어노테이션. 특정 Framework에 종속되지 않은 어플리케이션을 구성하고자 할 때 권장
<br> Inject를 사용하기 위해서는 JSR-330 라이브러리인 `javax.inject-x.x.x.jar` 파일 필요


#### @Autowired, @Resource, @Inject 비교
: 세 annotation 모두 멤버 변수에 정의하는 경우에는 별도의 setter method를 정의하지 않아도 된다

|        |  @Autowired  |  @Resource  |  @Inject  |
| :----: | :----------: | :---------: | :-------: |
| 범용    |  스프링 전용    |  자바에서 지원 | 자바에서 지원 | 
| 연결방식 |  by type     |  by name    | by type   |
| 적용범위 | 멤버변수, setter, 생성자, 일반 method | 멤버변수, setter | 멤버변수, setter, 생성자, 일반 method |

``` mermaid
graph LR
    MD(MetaData) --> IC(IoC Container)
    IC --> Beans
```

---
### Config
: xml 없이 java 코드만으로 bean 생성

- @Configuration
- @ComponentScan
- @Bean

=== "sampleconfig/test.java"
    ``` java
    ApplicationContext factory = new AnnotationConfigApplicationContext(MyConfiguration.class);
    String[] beanNames = factory.getBeanDefinitionNames();
    MyFoodMgr ob=factory.getBean("myFood", MyFoodMgr.class);
    ```
=== "MyConfiguration"
    ``` java
    @Configuration
    @ComponentScan("sampleconfig")
    public class MyConfiguration {
        @Bean
        public Food favoriteFood(){
            System.out.println("빵 객체 생성");
            Food f = new Food();
            f.setFoodName("Bread");
            f.setFoodPrice(1500);
            return f;
        }
        @Bean
        public Food unFavoriteFood(){
            System.out.println("누들 객체 생성");
            Food f = new Food();
            f.setFoodName("Noodle");
            f.setFoodPrice(2500);
            return f;
        }
    }
    ```


---
!!! quote
    - 김정현 강사님