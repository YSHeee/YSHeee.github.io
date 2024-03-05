# Control flow statements 제어문

## Conditionals 조건문

### if문
``` java
// if
if (조건식){
    실행문;
    실행문;
}

// if : 실행문이 하나라면, {} 생략 가능
if (조건식)
    실행문;

// else if : 조건문이 여러개일 때 사용
if (조건식){
    실행문;  
} else if (조건식2){
    실행문;
} else if (조건식3){
    실행문;
} else {
    실행문;
}
```

### switch문
- 만약 case에 break가 없다면, 값과는 상관없이 다음 case가 연달아 실행된다
``` java
int score = 0;
switch(변수){
    case 값1:
        변수값이 1일 경우 실행문;
        score = 100;
        break;
    case 값2:
        변수값이 2일 경우 실행문;
        score = 200;
        break;
    case 값3:
        변수값이 3일 경우 실행문;
        int result = 100;
        score = result;
        break;
    default:
        변수가 위 값이 모두 아닐 경우 실행문;
        score = 0;
}
```

=== "Java 12 이후부터 사용가능한 Expressions"
    ``` java
    int score = switch(변수){
        case 'A', 'a' -> 100;
        case 'B', 'b' -> 200;
        case 'C', 'c' -> {
            int result = 100;
            System.out.println("result입니다");
            yield result; // Java 13부터 가능
        }
        default -> 0;
    }
    ```
=== "Java 11 이전 문법"
    ``` java
    int score1 = 0;
    switch(변수){
        case "A":
            score1 = 100;
            break;
        case "B":
            int result = 100 - 20;
            score1 = result;
            break;
        default:
            score1 = 50;
    }
    ```
---

## Loop 반복문

- 부동소수점 방식의 float는 0.1을 정확히 표현하지 못하므로 초기화식에서 float 타입은 사용하지 않는다

### for
``` java title="100번 반복"
for (int i=0; i<100; i++){
    System.out.print(i);
}
```

[-> 배열 반복을 위한 for문](./reference-type.md/#배열-반복을-위한-for문)


### while
``` java title="100번 반복"
int i = 0;
while (i<100){
   System.out.print(i);
   i++;
}
```

### do-while
: 실행문을 처음에 우선 실행한 후, 그 다음부터 조건식 검사

``` java
do {
    실행문;
} while (조건식);
```

---

### break
: 반복문을 실행 중지하거나 조건문인 switch문을 종료할 때 사용

``` java title="Label Example"
label: for(int i=0; i<100; i++){
    for(int j=0; j<5; j++){
        if (j==5){
            break label; // 라벨을 통해 바깥쪽 중첩문까지 빠져나옴
        }
    }
}
```

### continue
: 그 이후의 문장을 실행하지 않고 다음 반복문으로 넘어감

``` java
for(int i=1; i<10; i++){
    if(i%2 == 0){
        continue; // 짝수일 경우, 아래 명령어를 실행하지 않고 다음 반복문으로 넘어감
    }
    System.out.println("홀수입니다");
}
```

---
## Exception 예외처리


---
!!! quote
    - 이것이 자바다 (저자: 신용권, 임경균 | 출판사: 한빛미디어)
