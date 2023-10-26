# Spring + DB

## Mybatis
: DB 연동 구현시 사용되는 Java Persistence Framework, SQL Mapper 기능 지원
<br> SQL 파일을 별도로 분리하여 관리할 수 있고, 객체-SQL 사이의 파라미터를 자동으로 매핑해준다

특징

- 생산성 : 62%정도 줄어드는 코드, 간단한 설정, 선택적 예외 처리
- 성능 : 구조적 강점(데이터 접근 속도를 높여주는 Join 매핑)
- SQL문과 애플리케이션 소스 코드의 분리<br>(SQL쿼리 변경 시마다 자바코드를 수정하거나 따로 컴파일 할 필요가 없다)
- 이식성 : 어떤 프로그래밍 언어로도 구현가능 (자바,C#,.NET,RUBY)
- 오픈소스 & 무료

### Install (Spring Boot)

1. 프로젝트 생성 시 https://start.spring.io에서 Mybatis Framework 선택하거나 <br>또는 build.gradle에 dependencies 항목 추가
``` bash
implementation 'org.mybatis.spring.boot:mybatis-spring-boot-starter:3.0.2'
```
2. application.properties 파일에 DB 접속 정보 추가
``` bash
spring.datasource.url: jdbc:{mysql}://{localhost:3306}/{db_name}?characterEncoding=UTF-8
spring.datasource.username: user
spring.datasource.password: password
spring.datasource.driver-class-name: com.mysql.cj.jdbc.Driver
```
3. SpringeduApplication 에 Mapper 파일들이 존재하는 패키지 정보 설정
``` java
@SpringBootApplication //(exclude = DataSourceAutoConfiguration.class)
@ComponentScan(basePackages={"com.example.springedu", "thymeleaf.exam"})
@MapperScan(value={"com.example.springedu.dao"})
public class SpringeduApplication {
	public static void main(String[] args) {
		SpringApplication.run(SpringeduApplication.class, args);
	}
}
```

--- 
### Example

=== "SQL Mapper Interface" 
    ``` java
    @Mapper
    public interface EmpMapper {
        @Select("select count(*) from emp")
        public int getAllDataNum();

        @Select("select empno, ename, job, date_format(hiredate, '%Y년 %m월 %d일') hiredate, sal  from emp")
        public List<EmpVO> listAll();

        @Select("select empno, ename, job, date_format(hiredate, '%Y년 %m월 %d일') hiredate, sal  from emp where empno = #{no}") // findEmp1 함수의 매개변수 사용
        public EmpVO findEmp1(int no);

        @Select("select empno, ename, job, date_format(hiredate, '%Y년 %m월 %d일') hiredate, sal  from emp where ename = #{name}")
        public EmpVO findEmp2(String name);

        // 페이징
        @Select("select empno, ename, job, date_format(hiredate, '%Y년 %m월 %d일') hiredate, sal from emp order by sal limit #{startNum}, #{countNum}")
        public List<EmpVO> listPart(PageDTO vo);
    }
    ```
=== "Mapper를 사용하는 컨트롤러 클래스"
    ``` java
    @Controller
    public class EmpController {
        @Autowired
        EmpMapper dao;
        
        @GetMapping("/empnum") // 수정
        public ModelAndView count() {
            ModelAndView mav = new ModelAndView();
            int num = dao.getAllDataNum();
            mav.addObject("num", num);
            mav.setViewName("empResult");
            return mav;
        }
        
        @GetMapping("/list")
        public ModelAndView list() {
            ModelAndView mav = new ModelAndView();
            List<EmpVO> list = dao.listAll();
            mav.addObject("list", list);
            mav.setViewName("empResult");
            return mav;
        }

        @GetMapping("/findEmp1")
        public ModelAndView findEmp1(@RequestParam(defaultValue="7788") int empno) {
            ModelAndView mav = new ModelAndView();
            EmpVO emp = dao.findEmp1(empno);
            if (emp == null)
                mav.addObject("msg", "사번이 "+empno+"인 직원은 없어요~~");
            else
                mav.addObject("emp", emp);
            mav.setViewName("empResult");
            return mav;
        }

        @GetMapping("/findEmp2")
        public ModelAndView findEmp2(String ename) {
            ModelAndView mav = new ModelAndView();
            EmpVO emp = dao.findEmp2(ename);
            if (emp == null)
                mav.addObject("msg", "성명이 "+ename+"인 직원은 없어요~~");
            else
                mav.addObject("emp", emp);
            mav.setViewName("empResult");
            return mav;
        }
        
        @GetMapping("/part")
        public ModelAndView part(PageDTO vo) {
            ModelAndView mav = new ModelAndView();
            List<EmpVO> list = dao.listPart(vo);
            mav.addObject("list", list);
            mav.setViewName("empResult");
            return mav;
        }
    }
    ```

---
## JPA 
: Java Persistence API, RDBMS와 OOP 객체 사이의 불일치에서 오는 패러다임을 해결하기 위해서 만들어진 ORM 기술
<br> 자바 ORM에 대한 API 표준 명세이자 인터페이스의 모음이므로 구현체가 없다. 따라서 ORM 프레임워크를 사용해야 하는데, 가장 대중적인 것은 **하이버네이트**이다

특징

- 생산성 : JPA에게 저장할 객체를 전달하기만 하면 되므로 코드 작성 필요 X, DDL문도 자동으로 생성해주기 때문에 데이터베이스 설계 중심을 객체 설계 중심으로 변경할 수 있다
- 유지보수 : 유지보수해야 하는 코드 :material-arrow-down:
- 패러다임의 불일치 해결 : JPA는 연관된 객체를 사용하는 시점에 SQL을 전달할 수 있고, 같은 트랜잭션 내에서 조회할 때 동 일성도 보장하기 때문에 다양한 패러다임의 불일치를 해결한다

!!! note
    **ORM**

    - Object Relational Mapping
    - 객체-관계 매핑의 줄임말로써 OOP의 객체 구현 클래스와 RDBMS에서 사용하는 테이블을 자동으로 매핑하는 것을 의미
    - SQL문을 구현할 필요 없이 객체를 통해 간접적으로 데이터베이스 조작 가능
    - 클래스와 테이블 매핑 시, 둘은 호환 가능성을 두고 만들어진 것이 아니므로 불일치가 발생하는데, ORM을 통해 객체 간의 관계를 바탕으로 SQL문을 자동 생성함으로써 해결한다

