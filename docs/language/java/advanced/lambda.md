# lambda 람다

- 함수형 프로그래밍 : 함수를 정의하고 이 함수를 데이터 처리부로 보내 데이터를 처리하는 기법
- 람다식 : 메서드 정의를 하나의 식으로 표현한 것
<br> - 자바는 람다식을 **익명 클래스 객체**로 변환한다
<br> - 인터페이스는 단 **하나**의 추상 메서드만 가져야 한다

=== "Base Example"
    ``` java
    interface Sample {
        int calc(int n);
    }

    class MyTest {
        static void pr(Sample p) {
            System.out.println(p.calc(10));
        }
    }

    class SampleImpl implements Sample {
        public int calc(int n) {
            return n + 1;
        }
    }

    Sample obj = new SampleImpl();
    MyTest.pr(obj);
    ```
=== "original"
    ``` java
    MyTest.pr(new Sample() {
        public int calc(int n) {
            return n + 10;
        }
    });
    ```
=== "lambda"
    ``` java
    // 1
    MyTest.pr((int n) -> {
        return n + 100;
    });
    // 2
    MyTest.pr((n) -> {
        return n + 100;
    });
    // 3
    MyTest.pr(n -> {
        return n + 100;
    });
    // 4
    MyTest.pr(n -> n + 100);
    ```
=== "Example2"
    ``` java
    interface Calculation {
        public int add(int a, int b);
    }

    public class LambdaTest2 {
        public static void exec(Calculation com) {
            int k = 10;
            int m = 20;
            int value = com.add(k, m);
            System.out.println("덧셈 결과 : " + value);
        }

        public static void main(String[] args) {
            exec(new Calculation() {
                public int add(int a, int b) {
                    return a + b;
                }
            });

            exec((int a, int b) -> {
                return a + b;
            });
            
            exec((a, b) -> a*a + b*b);
        }
    }
    ```

## 함수형 인터페이스
: 인터페이스가 단 하나의 추상 메서드를 가지는 것

- `@FunctionalInterface`
    - 함수형 인터페이스 체크 어노테이션
    - 인터페이스가 함수형 인터페이스임을 보장
    - 컴파일 과정에서 추상 메서드가 하나인지 검사함으로써 정확한 함수형 인터페이스를 작성할 수 있도록 도와주는 역할

---
## 매개변수가 없는 람다식
: 함수형 인터페이스의 추상 메서드에 매개변수가 없는 경우
<br> 실행문이 두 개 이상일 경우에는 중괄호를 생략할 수 없고, 하나일 경우에만 생략할 수 있다

=== "구조"
    ``` java
    // 실행문 2개 이상
    () -> {
        실행문;
        실행문;
    }

    // 실행문 하나
    () -> 실행문
    ```
=== "예제"
    ``` java
    @FunctionalInterface
    interface MyFunctionalInterface1 {
        public void method1();
    }

    // 실행문 2개 이상
    MyFunctionalInterface1 fi = () -> {
        String str = "method call1";
        System.out.println(str);
    };

    // 실행문 하나
    MyFunctionalInterface1 fi = () -> System.out.println("method call2");	
    fi.method1();
    ```

## 매개변수가 있는 람다식
: 함수형 인터페이스의 추상 메서드에 매개변수가 있는 경우
<br> 타입은 생략 가능하며, 매개변수가 하나라면 괄호도  생략할 수 있다

=== "구조"
    ``` java
    // 타입 + 매개변수
    (타입 매개변수, ...) -> {
        실행문;
        실행문;
    }
    (타입 매개변수, ...) -> 실행문

    // 타입 생략
    (매개변수, ...) -> {
        실행문;
        실행문;
    }
    (매개변수, ...) -> 실행문

    // 매개변수가 하나인 경우, 괄호 생략
    매개변수 -> {
        실행문;
        실행문;   
    }
    매개변수 -> 실행문
    ```
=== "예제"
    ``` java
    @FunctionalInterface
    interface MyFunctionalInterface2 {
        public void method2(int x);
    }

    // 1
    MyFunctionalInterface2 fi = (x) -> {
        System.out.println(x);
    };

    // 2
    MyFunctionalInterface2 fi = x -> System.out.println(x);

    // 3
    MyFunctionalInterface2 fi = System.out::println;
    fi.method2(2);
    ```

## 리턴값이 있는 람다식
: 함수형 인터페이스의 추상 메서드에 리턴값이 있는 경우
<br> - return문이 하나인 경우, 중괄호와 함께 return 키워드 생략 가능
<br> - return =  값/연산식/리턴값이 있는 메서드의 호출식

=== "구조"
    ``` java
    (매개변수, ...) -> {
        실행문;
        return 값;
    }

    (매개변수, ...) -> 값 ⭐
    ```
=== "예제"
    ``` java
    @FunctionalInterface // 함수형 인터페이스 체크 어노테이션
    interface MyNumber {
        int getMax(int num1, int num2);
    }

    // 1
    MyNumber max1 = new MyNumber() {
        public int getMax(int x, int y) {
            return (x >= y) ? x : y;
        }
    };

    // 2 : 리턴문 하나 (연산식)
    MyNumber max2 = (int x, int y) -> {
        return (x >= y) ? x : y;
    };

    // 3 : 리턴문 하나 (메서드)
    MyNumber max3 = (x, y) -> sum(x,y);
    System.out.println(max3.getMax(100, 300));		
    ```


## 메서드 참조
: 메서드를 참조하여 매개변수의 정보/리턴 타입을 알아냄으로써 람다식에서 불필요한 매개변수 제거

``` java
(left, right) -> Math.max(left, right);

// Example
@FunctionalInterface
interface MyFunctionalInterface3 {
	public int method3(int x, int y);
}

// 1
MyFunctionalInterface3 fi = (x, y) -> Math.addExact(x, y); 

// 2
MyFunctionalInterface3 fi = (x, y) -> Math::addExact;
System.out.println(fi.method3(7, 1));
```

- 정적 메서드 참조 : `클래스 :: 메서드`
- 인스턴스 메서드 참조 : `참조변수 :: 메서드`


## 매개변수의 메서드 참조
: 람다식에서 제공되는 a 매개변수의 메서드를 호출해서 b 매개변수를 매개값으로 사용

- 클래스 :: instanceMethod
``` java
(a,b) -> {a.instanceMethod(b);}
```

## 생성자 참조
: 객체를 생성하는 것

- 단순히 객체를 생성하고 리턴하는 구성이라면, 람다식을 생성자 참조로 대치할 수 있다
    - `(a,b) -> {return new 클래스(a,b);}`
- 생성자가 오버로딩 되어 여러 개 있는 경우 
    - 컴파일러는 함수형 인터페이스의 추상 메서드와 동일한 매개변수 타입과 개수를 가진 생성자를 찾아 호출
    - 해당 생성자가 존재하지 않으면 컴파일 오류 발생
- 클래스 :: new

``` java
// Example
@FunctionalInterface
interface MyFunctionalInterface4 {
	public Date method4();
}

// 1
MyFunctionalInterface4 fi = () -> {
    return new Date();
};

// 2
MyFunctionalInterface4 fi = () -> new Date();

// 3
MyFunctionalInterface4 fi =  Date::new;
System.out.println(fi.method4());
```

---
## Sort 활용
``` java
List<String> list = Arrays.asList("abc", "aaa", "bbb", "ccc");

// 오름차순 1
Collections.sort(list, new Comparator<String>() {
    public int compare(String s1, String s2) {
        return s2.compareTo(s1);
    }
});

// 2
Collections.sort(list, String::compareTo);

// 두 번째 아규먼트를 기준으로 비교하는 내림차순
Collections.sort(list, (String s1, String s2) -> {
    return s1.compareTo(s2);
});
```

---
## Generics 활용
``` java
interface ActionExpression {
	void exec(Object... param);
}

interface FuncExpression<T> { // type 반환
	T exec(Object... param);
}

public class LambdaTest12 {
	// Test1
	public static void Test1(ActionExpression action) {
		action.exec("hello world");
	}
	// Test2
	public static void Test2(FuncExpression<String> func) {
		String ret = func.exec("hello world");
		System.out.println(ret);
	}
    // main
	public static void main(String[] args) throws Exception {
		
		Test1(new ActionExpression() {
			public void exec(Object... data) {
				System.out.println("Test1 - " + data[0]);
			}
		});
		
		Test2(new FuncExpression<String>() {
			public String exec(Object... data) {
				System.out.println(data[0]);
				return "OK1";
			}
		});

		Test1((Object... data) -> System.out.println("Test2 - " + data[0]));

		Test2((Object... data) -> {
			System.out.println(data[0]);
			return "OK2";
		});
	}
}
```






---
!!! quote
    - 이것이 자바다 (저자: 신용권, 임경균 | 출판사: 한빛미디어)
    - 김정현 강사님