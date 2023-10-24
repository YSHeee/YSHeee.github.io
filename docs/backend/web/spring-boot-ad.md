# Sprint Boot Advanced

## @Service
``` java title="Example"
package com.example.springedu.service;
import org.springframework.stereotype.Service;
import com.example.springedu.domain.FriendDTO;

@Service
public class FriendService {
	public FriendDTO get(int num) {
		FriendDTO vo = null;
		if (num == 10) {
			vo = new FriendDTO();
			vo.setPhoneNum("010-1111-2222");
			vo.setName("Dooly");			
		}
		return vo;
	}
}
```

---
## Spring Scheduling(TASK)

: 특정 시간에 반복적으로 처리되는 코드를 스케줄링 할 수 있으며 이때 반복되는 코드를 Task라 한다

### Setting

1. [Spring.io](https://start.spring.io)
    - Dependencies에 Quartz Scheduler 추가
    - EXPLOR -> build.gradle 추가
    ```gradle
    dependencies {
        implementation 'org.springframework.boot:spring-boot-starter-quartz'
        testImplementation 'org.springframework.boot:spring-boot-starter-test'
    }
    ```
2. [mvnrepository](https://mvnrepository.com)

### Use
: 설정된 Scheduling에 맞춰 호출되는 Task Method 앞에 `@Scheduled`라는 어노테이션 제시한 다음 속성 정의

- `cron` : CronTab에서의 설정과 같이 cron="0/10 * * * * ?" 과 같은 설정 가능
- `fixedDelay` : 이전에 실행된 Task의 종료시간으로 부터 정의된 시간만큼 지난 후 Task 실행
- `fixedRate` : 이전에 실행된 Task의 시작시간으로 부터 정의된 시간만큼 지난 후 Task 실행

``` java title="Example"
package com.example.springedu.service;
import org.springframework.scheduling.annotation.Scheduled;
import java.text.SimpleDateFormat;
import java.util.Calendar;

//@Component
public class SpringSchedulerTest {	
	//@Scheduled(cron = "10 08 18 * * 2")// 초, 분, 시, 일, 월, 요일(0:일요일)
	@Scheduled(fixedDelay = 5000) // 5초에 한 번씩
	public void scheduleRun() {
		Calendar calendar = Calendar.getInstance();
		SimpleDateFormat dateFormat = 
				new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		System.out.println("**** 스케줄 실행 : " + 
				dateFormat.format(calendar.getTime()));	
	}
}
```

### Cron

|  시간  |  단위  | |  기호  |  의미  |
| :----:| :---: | :--: | :--: | :--: |
| Seconds | 0 ~ 59 | | ? | Day of Month, Day of Week에만 사용 특별한 값이 없음을 의미 |
| Minutes | 0 ~ 59 | | - | 기간 설정 |
| Hours | 0 ~ 23 | | , | 특정 시간 설정 |
| Day of Month | 1 ~ 31 | | / | 증가 표현 |
| Month | 1 ~ 12 | | L | Day of Month, 마지막날에 실행하라는 의미 | 
| Day of Week | 1 ~ 7 (일요일~토요일) | | W | Day of Month, 가장 가까운 평일을 의미 | 
| Years(optional) | 1970 ~ 2099 | | LW | L+W, 그 달의 마지막 평일 |
| | | | # | Day of Week, 6#3의 경우 3번째 주 금요일 실행 
| | | | * | 모든 수, Minutes일때 매분마다를 의미 |


---
## 오류 처리
: @ExceptionHandler, @ControllerAdvice 둘 다 존재할 때는 더 가까운 @ExceptionHandler 수행

### @ExceptionHandler
: 에러나 예외를 지역적으로 처리하며 컨트롤러 클래스마다 각각 정의된다
<br>- 컨트롤러에서 정의한 메서드(@RequestMapping)에서 기술한 예외가 발생되면 자동으로 받아냄
<br>- 이를 이용하여 컨트롤러에서 발생하는 예외를 View단인 JSP나 타임리프로 보내서 처리할 수 있다

``` java title="Example"
package com.example.springedu.controller;
import ...

@Controller
public class ExceptionLocalController {

	@Autowired
	FriendService ms;

    @RequestMapping("/exceptionTest")
	public String detail(int num, Model model) throws FriendNotFoundException {
		FriendDTO vo = ms.get(num);
		if (vo == null) {
			throw new FriendNotFoundException();
		}
		model.addAttribute("friend", vo);
		return "friendView";
	}

	@ExceptionHandler(MethodArgumentTypeMismatchException.class)
	public ModelAndView handleTypeMismatchException(MethodArgumentTypeMismatchException ex) {
		System.out.println("TypeMismatchException 발생시 처리하는 핸들러가 오류 처리합니다.");
		ModelAndView mav = new ModelAndView();
		mav.addObject("msg", "타입을 맞춰주세용!!");
		mav.setViewName("errorPage");
		return mav;
	}

	@ExceptionHandler(FriendNotFoundException.class)
	public String handleNotFoundException() throws IOException {
		System.out.println("FriendNotFoundException 발생시 처리하는 핸들러가 오류 처리합니다.");
		return "noFriend";
	}

	@ExceptionHandler(IllegalStateException.class)
	public ModelAndView handleIllegalStateException() throws IOException {
		System.out.println("IllegalStateException 발생시 처리하는 핸들러가 오류 처리합니다.");
		ModelAndView mav = new ModelAndView();
		mav.addObject("msg", "num=숫자 형식의 쿼리를 전달하세요!!");
		mav.setViewName("errorPage");
		return mav;
	}
}

```

### @ControllerAdvice
: 스프링 3.2 이상에서 사용 가능, @Controller/@RestController 에서 발생하는 예외 등을 catch
<br> -> 예외처리를 전담하는 클래스 생성

- 클래스 위에 @ControllerAdvice를 붙이고, 어떤 예외를 잡아낼 것인지 내부 메서드를 선언하여 메서드 상단에 `@ExceptionHandler(예외클래스명.class)`와 같이 기술
``` java title="Example"
// 모든 RuntimeException에 대해 적용
package com.example.springedu.service;
import ...

@ControllerAdvice
public class CommonExceptionHandler {
    @ExceptionHandler(RuntimeException.class)
    private ModelAndView errorModelAndView(Exception ex) {
       ModelAndView modelAndView = new ModelAndView();
       modelAndView.setViewName("commonErrorPage");
       modelAndView.addObject("exceptionInfo", ex );
       return modelAndView;
   }
}
```

---