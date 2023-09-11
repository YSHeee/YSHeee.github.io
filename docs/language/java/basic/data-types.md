# Data Type

#### 기본형(Primitive) 
- 정수 : byte, char, short, int, long
- 실수 : float, double 
- 논리(true/false) : boolean

![1](../images/type_1.png)
![2](../images/type_2.png)
└ S는 부호 MSBit(양수 0, 음수 1)

- 오버플로우(Overflow) 
: 해당 타입이 표현할 수 있는 범위보다 큰 수 저장
<br> 최상위 비트를 벗어난 데이터가 인접 비트를 덮어씀으로써 잘못된 결과를 얻을 수 있음
- 언더플로우(Underflow) 
: 해당 타입이 표현할 수 있는 범위보다 작은 수 저장하여 잘못된 결과값 저장

## 정수형 : byte, short, char, int, long

- 2진수 : `0b` 또는 `0B`로 시작하여 0과 1로 작성
- 8진수 : `0`으로 시작하고 0~7 숫자로 작성
- 10진수 : 소수점이 없는 0~9 숫자로 작성
- 16진수 : `0x` 또는 `0X`로 시작하고 0~9 숫자/A,B,C,D,E,F/a,b,c,d,e,f로 작성 

## 부동소수점


## 문자 리터럴

Escape Sequence
- `\b` : 백스페이스
- `\t` : 탭
- `\n` : 줄바꿈 
- `\f` : 새 페이지 문자
- `r` : 리턴 문자


!!! quote
    - [Java의 정석](https://github.com/castello/javajungsuk_basic/tree/master)
    - [점프 투 자바](https://wikidocs.net/book/31)
    - [TCP school](http://www.tcpschool.com/java/intro)
    - 이것이 자바다 (저자: 신용권, 임경균 | 출판사: 한빛미디어)
    - 뇌를 자극하는 Java Programming