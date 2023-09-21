# 정규표현식 Regular Expression
: 문자열에서 특정한 규칙을 가지는 문자열의 집합을 찾아내기 위한 검색 패턴

- 정규 표현식 리터럴 `/검색패턴/플래그`
- RegExp 객체 생성 `new RegExp("검색패턴")`

### 단순 패턴 검색 search
- search() : 인수로 전달받은 정규표현식과 일치하는 첫번째 문자열의 위치 반환 (없으면 -1 반환)

``` javascript
var targetStr = "간장 공장 공장장은 강 공장장이고, 된장 공장 공장장은 장 공장장이다."
var strReg1 = /공장/;
var strReg2 = /장공/;

targetStr.search(strReg1); // 3
targetStr.search(strReg2); // -1
```

### 플래그 flags
: 기본 검색 설정을 변경할 수 있음

- `i` : 검색 패턴을 비교할 때, 대소문자를 구분하지 않도록 설정 (default)
- `g` : 검색 패턴을 비교할 때, 일치하는 모든 부분을 선택하도록 설정
- `m` : 검색 패턴을 비교할 때, 여러 줄의 입력문자열을 그 상태 그대로 여러 줄로 비교하도록 설정
- `y` : 대상 문자열의 현재 위치부터 비교를 시작하도록 설정

``` javascript
var strUsingFlag = /AB/i; 
var strUsingFlagNew = new RegExp("AB", "i");
```

### 특수문자 

|  특수 문자  |  설명  |
| :-------:  | :-----:|
| \  | 역슬래시(`\`) 다음에 일반 문자가 나오면 이스케이프 문자로 해석하고, 특수 문자가 나오면 일반 문자로 해석 |
| \d | 숫자 검색 `/[0-9]/`와 같음 |
| \D | 문자 검색 ` /[^0-9]/`와 같음 |
| \w | 언더스코어(_)를 포함한 영문자 및 숫자 검색 `/[A-Za-z0-9_]/` |
| \W | 언더스코어(_), 영문자, 숫자가 아닌 문자 검색 `/[^A-Za-z0-9_]/` |
| \s | 띄어쓰기, 탭, 줄 바꿈 문자 등의 공백 문자 검색 |
| \S | 띄어쓰기, 탭, 줄 바꿈 문자 등의 공백 문자가 아닌 문자 검색 |
| \b | 단어의 맨 앞이나 맨 뒤가 패턴과 일치하는지 검색 |
| \xhh   | 16진수 hh에 해당하는 유니코드 문자 검색 |
| \uhhhh | 16진수 hhhh에 해당하는 유니코드 문자 검색 |

``` javascript title="Example"
var targetStr = "abc 123";
var reg = /\w\s\w/; // c 1 : 공백 문자를 사이에 두는 언더스코어(_)를 포함한 영문자 및 숫자로 이루어진 문자열 검색

var targetStr1 = "abc123abc"; // 7
var reg = /bc\b/; // 단어의 맨 앞이나 맨 뒤에 부분 문자열 "bc"가 존재하는지를 검색
```

### 양화사 quantifier
: 수량을 나타내는 특수 문자

|  괄호  |  설명  |
| :-------:  | :-----:|
| n* | 바로 앞의 문자가 0번 이상 나타나는 경우 검색 `/{0, }/` |
| n+ | 	바로 앞의 문자가 1번 이상 나타나는 경우 검색  ` /{1, }/` |
| n? | 바로 앞의 문자가 0번 또는 1번만 나타나는 경우 검색 `/{0,1}/`|

``` javascript title="Example"
var targetStr = "Hello World!";
var zeroReg = /lo*/;  // 2 : 문자 'l' 다음에 문자 'o'가 0번 이상 나타나는 경우 검색
var oneReg = /lo+/;  // 3 : 문자 'l' 다음에 문자 'o'가 1번 이상 나타나는 경우 검색
var zeroOneReg = /lo?/;  // 2 : 문자 'l' 다음에 문자 'o'가 0 또는 1번만 나타나는 경우 검색
```

- `?` 기호가 정규 표현식의 양화사(`*`, `+`, `?`, `{}`) 바로 다음에 위치하면, 가능한 많은 문자를 가지는 패턴을 찾는 기본 설정과는 달리 가능한 적은 수의 문자만을 가지는 패턴을 찾도록 변경
``` javascript title="Example"
var targetStr = "123abc";
var oneReg = /\d+/;  // 123 : 숫자 검색함. /[0-9]/
var anotherReg = /\d+?/; // 1 : 숫자를 검색하지만, 가능한 적은 수의 문자를 가지는 패턴을 검색
```

### 괄호 bracket

|  특수 문자  |  설명  |
| :-------:  | :-----:|
| a(b)c  | 전체 패턴을 검색한 후에 괄호 안에 명시된 문자열을 저장 (ex : "abc"를 검색한 후에 b 저장) |
| [abc] | 꺾쇠 괄호([]) 안에 명시된 문자 검색 (ex : "abc"를 검색) |
| [0-3] | 꺾쇠 괄호([]) 안에 명시된 숫자 검색 (ex : 0부터 3까지의 숫자 검색) |
| [\b] | 백스페이스 문자 검색 <br> :exploding_head: `\b`는 단어의 맨앞이나 맨 뒤가 패턴과 일치하는지 검색하는 특수 문자 |
| {n} | 앞의 문자가 정확히 n번 나타나는 경우 검색. n은 반드시 양의 정수 |
| {m,n} | 앞의 문자가 최소 m번 이상 최대 n번 이하로 나타나는 경우 검색. m과 n은 반드시 양의 정수 |

#### replace()
``` javascript title="Example"
var targetStr = "Hong Gil Dong";
var nameReg = /(\w+)\s(\w+)\s(\w+)/;  // 공백 문자를 기준으로 각 부분문자열 저장
var engName = targetStr.replace(nameReg, "$2 $3 $1"); // 첫 번째 부분문자열을 맨 마지막으로 위치시킴

engName; // Gil Dong Hong
```

#### match()
: 정규 표현식과 모두 일치하는 부분 문자열뿐만 아니라, 괄호를 사용하여 저장된 부분 문자열도 함께 반환

``` javascript title="Example"
var targetStr = "abc 123 abc 123";
var oneReg = /(\w+) (\d+)/; // _를 포함한 영문자/숫자로 이루어진 부분 문자열과 띄어쓰기로 구분되는 숫자 부분 문자열 검색
var anotherReg = /(\w+) (\d+) \1 \2/; // 저장된 부분 문자열을 정규표현식 내에서 재사용

targetStr.match(oneReg);     // abc 123, abc, 123
targetStr.match(anotherReg); // abc 123 abc 123, abc, 123
```

### 위치 문자

|  괄호  |  설명  |
| :-------:  | :-----:|
| ^a | 단어의 맨 앞에 위치한 해당 패턴만을 검색 (ex : 'a'로 시작하는 단어의 'a'만 검색) |
| a$ | 단어의 맨 뒤에 위치한 해당 패턴만을 검색 (ex : 'a'로 끝나는 단어의 'a'만 검색) |

``` javascript title="Example"
var firstStr = "Php";
var secondStr = "phP";
var strReg = /^p/;       // 'p'로 시작하는 단어의 'p'만을 검색

firstStr.match(strReg);  // null
secondStr.match(strReg); // p
```

---

## RegExp 객체
: 정규 표현식을 구현한 자바스크립트 표준 내장 객체

### RegExp.prototype Method
- RegExp.prototype.exec()
- RegExp.prototype.test()
- RegExp.prototype.toString() : RegExp 객체의 정규 표현식과 같은 의미를 가지는 정규 표현식 리터럴 문자열 반환

#### exec()
: 인수로 전달된 문자열에서 특정 패턴을 검색하여 패턴과 일치하는 문자열 반환. 없다면 null 반환

``` javascript title="Example"
var targetStr = "abbcdefabgh";
var firstResult = /ab+/.exec(targetStr);    // 패턴과 일치하는 문자열이 여러 개인 경우
var secondResult = /abbb+/.exec(targetStr); // 패턴과 일치하는 문자열이 하나도 없는 경우

firstResult;  // abb -> 가장 맨 처음으로 일치하는 문자열 반환
secondResult; // null
```

#### test()
: 인수로 전달된 문자열에 특정 패턴과 일치하는 문자열이 있는지 검색. 있으면 true, 없으면 false 반환

``` javascript title="Example"
var targetStr = "abbcdefabgh";
var firstResult = /ab+/.test(targetStr);    // 패턴과 일치하는 문자열이 여러 개인 경우
var secondResult = /abbb+/.test(targetStr); // 패턴과 일치하는 문자열이 하나도 없는 경우

firstResult;  // true
secondResult; // false
```

### RegExp.prototype Property

- RegExp.prototype.global 
: 검색 패턴을 비교할 때 일치하는 모든 부분을 선택하도록 설정하는 플래그인 'g'를 가리킴
- RegExp.prototype.ignoreCase 
: 검색 패턴을 비교할 때 대소문자를 구분하지 않도록 설정하는 플래그인 'i'를 가리킴
- RegExp.prototype.multiline 
: 검색 패턴을 비교할 때 여러 줄의 입력 문자열을 그 상태 그대로 여러 줄로 비교하도록 설정하는 플래그인 'm'을 가리킴
- RegExp.prototype.source 
: 검색 패턴이 포함하고 있는 문자열을 가리킴

---
!!! quote
    - [TCP School](https://www.tcpschool.com/javascript/intro)