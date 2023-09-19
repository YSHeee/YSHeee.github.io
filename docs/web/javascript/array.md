# 배열 Array
: 이름과 인덱스로 참조되는 정렬된 값의 집합

- 배열 요소 Element : 배열을 구성하는 각각의 값
- Index : 배열에서의 위치를 가리키는 숫자

### 특징
- 요소의 타입이 고정되어 있지 않으므로. 같은 배열 내 요소끼리의 타입이 서로 다를 수 있음
- 배열 요소의 인덱스가 연속적이지 않아도 되며, 따라서 특정 배열 요소가 비어 있을 수 있음
- 배열의 길이는 자동으로 연장됨
- JS에서 배열은 Array 객체로 다루어진다

### 생성

- `document.write(arr);` : 배열 요소 모두 출력
- `document.write(arr.length)` : 배열 길이 출력
``` javascript
var arr = [element, element, ...]; // 배열 리터럴 이용
var arr = Array(element, element, ...); // Array 객체의 생성자 이용
var arr = new Array(element, element, ...); // new 연산자 이용
```

### 요소 추가
- push()
- index
``` javascript
arr.push(element);
arr[arr.length] = element;
arr[index] = element;
```

### 순회
``` javascript
var arr = [element1, element2, element3];
var result = "<table><tr>";
for (var val in arr)
    result += "<td>" + arr[val] + "</td>"
result += "</tr></table>";
```

### 희소 배열
: 배열에 속한 요소의 위치가 연속적이지 않은 배열
<br> 배열의 length 값보다 배열 요소의 개수가 항상 적다

### 연관 배열 Associative array = 객체
: 숫자로 된 Index 대신, 문자열로 된 Key를 사용하는 배열

- JS는 연관 배열을 별도로 제공하지 않지만, 인덱스로 문자열을 사용하여 연관 배열처럼 사용할 수 있는 객체를 생성할 수 있다
- 이렇게 생성된 배열은 JS 내부적으로 Array 객체에서 **기본 객체로 재선언**되어 모든 Array 메서드와 property가 **정확하지 않은 결과값을 반환**한다
- ECMAScript6부터는 Map 객체를 별도로 제공
```javascript
var arr = [];
arr["하나"] = 1;
arr["둘"] = 2;
document.write(arr["하나"]);
document.write(arr.length); // Array 객체가 아니므로 0 반환
document.write(arr[0]); //undefined
```

### 문자열을 배열처럼 접근하기
: JS에서 문자열은 Immutable하므로 읽기 전용 배열로서 다룰 수 있다

- charAt()
- 문자열[index]
- split()으로 배열로 변환 후 사용
``` javascript
var str = "Hello, world!"
document.write(str.charAt(2)); // l
document.write(str[2]); // l
```

### 배열 여부 확인
: JS에서 배열은 Object 타입이므로 typeof 연산자로는 배열 여부를 알 수 없다

- Array.isArray() 메서드 (ECMAScript5~)
- instanceof 연산자
- constructor 프로퍼티
