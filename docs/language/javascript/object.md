# Object 객체 
: 자바의 Data type이자 name, value로 구성된 property의 정렬되지 않은 집합

- Object: cat
- Property
    - cat.name
    - cat.age
    - cat.weight
- Method
    - cat.eat()
    - cat.sleep()
    - cat.play()

## 객체의 Property & Method 참조
- objectName.propertyName
- objectName["propertyName"]
- objectName.methodName()
- objectName.methodName <br>: 괄호를 붙이지 않으면, 메서드가 아닌 프로퍼티 그 자체를 참조하게 되어 해당 메서드의 정의 반환
``` javascript
var dog = {
    name: "초코",
    birthday: "000330",
    pid: "115"
    fullId: function(){return this.birthday + this.pid;}
};
dog.name //초코
dog["name"] //초코

dog.fullId() // 000330115
dog.fullId; // function(){return this.birthday + this.pid;}
```

## 객체의 생성
: 아래 방법들로 생성되어 메모리에 대입된 객체를 인스턴스 Instance 라고 한다 
<br> 객체 리터럴 방식, 생성자 함수 방식

- 리터럴 
    - 하나의 객체만 생성 (싱글톤 객체)
    - prototype 속성 사용 불가
- 생성자 함수 Constructor function
    - 동일한 속성 사양을 갖는 객체들을 여러개 생성 가능
    - prototype 속성 사용 가능
    - 정적 멤버 정의 가능
- Object.create() 
    - 지정된 prototype 객체와 property를 가지고 새로운 객체 생성
    - Object.create( prototypeObject[, newObjectProperty1, newObjectProperty, ...] )

=== "Literal notation"
    ``` javascript
    // 1
    var dog = {
        name: "초코",
        birthday: "000330",
        pid: "115"
        fullId: function(){return this.birthday + this.pid;}
    };

    // 2
	const person = { };        
	person.이름 = '홍길동';
	person.취미 = '악기';
	person.특기 = '프로그래밍';
	person.장래희망 = '생명공학자';
    ```
=== "Constructor && Object.create()"
    ``` javascript
    var date = new Date(); // 생성자 new : Date 타입의 객체 생성

    // Object.create()
    // null 프로토타입을 사용하여 새로운 객체를 생성하고 x좌표, y좌표 프로퍼티 추가
    var obj = Object.create(
            null, 
            {x: {value:100, enumeratble:true}, y: {value:200, enumerable:true}}
            );
    obj.x; // x좌표
    obj.y; // y좌표
    Object.getPrototypeOf(obj); // 객체의 프로토타입 반환
    ```

## 객체에 Proeprty 및 Method 추가

- 새롭게 추가된 property와 method는 오직 해당 인스턴스에만 추가됨
``` javascript
function Dog(name, birthday, pid){
    this.name = name;
    this.birthday = birthday;
    this.pid = pid;
};
var myDog = new Dog("초코", "000330", "115"); // Dog.prototype

myDog.family = "푸들" // 품종에 관한 property 추가
myDog.introduce = function(){return this.name+"는 "+this.family;} // 자기소개 메서드 추가
```

## 객체 Property 삭제
- delete objectName.propertyName;
``` javascript
function Dog(name, birthday, pid){
    this.name = name;
    this.birthday = birthday;
    this.pid = pid;
};
var myDog = new Dog("초코", "000330", "115"); 

delete myDog.name; // name property 삭제
myDog.name; // undefined 출력
```

## 객체 property 순회
- for (var i in obj)
- Object.keys() : 해당 객체가 가진 고유 property 중 열거할 수 있는 property의 이름을 배열에 담아 반환
- Object.getOwnPropertyNames() : 해당 객체가 가진 모든 고유 property의 이름을 배열에 담아 반환
``` javascript
function Dog(name, birthday, pid){
    this.name = name;
    this.birthday = birthday;
    this.pid = pid;
};
var myDog = new Dog("초코", "000330", "115"); 

for(var key in myDog) {
	console.log(key + ":" + obj[key]);
}

// name property의 enumerable 속성을 false로 설정
Object.defineProperty(myDog, "name", {enumerable: false});

Object.keys(myDog); // birthday, pid
Object.getOwnPropertyNames(myDog); // name, birthday, pid
```

## 객체간의 비교
``` javascript
function Dog(name, birthday, pid){
    this.name = name;
    this.birthday = birthday;
    this.pid = pid;
};
var myDog = new Dog("초코", "000330", "115"); 
var yourDog = new Dog("바닐라", "000331", "114");
myDog == yourDog; // false
myDog === yourDog; // false

var hisDog = myDog;
myDog == hisDog; // true
myDog === hisDog; // true
```

## this
: 호출된 자바스크립트 코드 영역을 포함하고 있는 객체를 가리키는 키워드

- 메서드 내부에서 사용된 this : 해당 메서드를 포함하고 있는 객체를 가리킴
- 객체 내부에서 사용된 this : 객체 그 자신을 가리킴
- 객체 생성자 함수 내부에서 사용된 this : 어떠한 값도 가지지 않고, 새로운 객체로 대체됨

---
## 상속 Inheritance
: Ptorotype-based의 객체 지향 언어인 JS에서 현재 존재하고 있는 객체를 프로토타입으로 사용하여 해당 객체를 복제하여 재사용하는 것을 의미

- 기존 클래스를 상속받아 수정하여 재사용할 수 있는 기능 
- 새로운 클래스에서 기존 클래스의 모든 property와 method를 사용할 수 있음 
- 클래스 간의 종속 관계를 형성함으로써 객체의 관계 조직화

---
## 프로토타입 Prototype
: 모든 객체가 최소 하나 이상의 다른 객체로부터 상속을 받는 JS에서 상속되는 정보를 제공하는 객체를 뜻함

- JS의 모든 객체는 prototype이라는 객체를 가지고 있고,
- 모든 객체는 그들의 prototype으로부터 property와 method를 상속받는다


### 프로토타입 체인 Prototype Chain
: 자신의 프로퍼티나 메소드 뿐만 아니라 __proto__가 가리키는 링크를 따라서 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티나 메소드에 접근할 수 있다

- JS에서 객체 이니셜라이저를 사용해 생성된 같은 타입의 객체들은 모두 같은 prototype을 가짐
- new 연산자를 사용해 생성한 객체는 생성자의 프로토타입을 상속받음
- Object.prototype 객체는 어떠한 프로토타입과 프로퍼티를 상속받지 않고 (최상위 prototype)
- 자바스크립트에 내장된 모든 생성자는 Obejct.prototype을 상속받는다
``` javascript
var obj = new Object(); // 해당 객체의 프로토타입 : Object.prototype
var arr = new Array(); // Prototype Chain: Array.prototype && Object.prototype 
var date = new Date(); // Prototype Chain: Date.prototype && Object.prototype
```

### 프로토타입의 생성
: 객체 생성자 함수 작성 (첫글자는 대문자)

``` javascript
// Dog 생성자 함수
function Dog(name, birthday, pid){
    this.name = name;
    this.birthday = birthday;
    this.pid = pid;
};
var myDog = new Dog("초코", "000330", "115"); // Dog.prototype

```

### 프로토타입에 Proeprty 및 Method 추가 :star:
: Method는 인스턴스별 메모리 할당보다 독자적으로 메모리 할당됨으로써 공유되는 것이 효율적이므로 생성자 함수에 선언하기보다 prototype에 선언하는 것이 효율적이다

``` javascript
function Dog(name, birthday, pid){
    this.name = name;
    this.birthday = birthday;
    this.pid = pid;
};

Dog.prototype.family = "푸들"; // Dog 프로토타입에 family property 추가
Dog.prototype.introduce = function(){return this.name+"는 "+this.family;}; // Dog 프로토타입에 introduce method 추가

var myDog = new Dog("초코", "000330", "115");
myDog.introduce();
```

---
## 자주 사용되는 Object Method

#### hasOwnProperty()
: 특정 property가 해당 객체에 존재하는지 검사
<br>같은 이름의 property라도 **상속받은 property는 false 반환**

``` javascript
myDog.hasOwnProperty("name"); // true
myDog.hasOwnProperty("nickname"); // false
myDog.hasOwnProperty("class"); // 상속받은 property이므로 false 반환
```

#### propertyIsEnumerable()
: 특정 property가 해당 객체에 존재하고, 열거할 수 있는 프로퍼티인지 검사

``` javascript
// name property의 enumerable 속성을 false로 설정
Object.defineProperty(myDog, "name", {enumerable: false});

myDog.propertyIsEnumerable("name"); // false
myDog.propertyIsEnumerable("birthday"); // true
```

#### isPrototypeOf()
: 특정 객체의 프로토타입 체인에 현재 객체가 존재하는지 검사

``` javascript
var day = new Date();

Date.prototype.isPrototypeOf(day); // true
Date.prototype.isPrototypeOf(new String()); // false
```

#### isExtensible()
: 객체에 새로운 property를 추가할 수 있는지 여부 반환

- JS의 모든 객체는 기본적으로 새로운 프로퍼티를 추가할 수 있다
- preventExtensions() : 해당 객체에 새로운 property를 추가할 수 없도록 설정
``` javascript
var day = new Date();
Object.isExtensible(day); // true

var myDay = Object.preventExtensions(day); // property를 추가할 수 없도록 설정
Object.isExtensible(myDay); // false
```

#### toString()
: 메소드를 호출한 객체의 값을 문자열로 반환

``` javascript
var arr = [10, "문자열", true]
arr.toString(); // 10,문자열,true

var bool = false;
bool.toString(); // false

function func() {return;}
func.toString(); // 함수의 소스 코드 전부 문자열로 반환
```

#### valueOf()
: 특정 객체의 primitive type의 값을 반환

- JS에서는 primitive type 값이 기대되는 곳에 객체가 사용되면, 내부적으로 해당 메서드를 호출하여 처리
- 객체가 primitive type을 갖고 있지 않다면, 해당 메서드는 객체 자신을 반환함

``` javascript
function func(n){
    this.number = n;
}

f = new func(4);
f + 5; // [object Object]5 : valueOf()가 정의되지 않아 객체 자신을 반환

func.prototype.valueOf = function(){ // valueOf() 메서드 정의
    return this.number;
} 
f + 5; // 9 : number의 property 반환
```

#### getter와 setter 메서드의 정의
: getter와 setter 메소드로 정의된 property는 접근자 property라 부른다

- getter : 특정 property의 값을 받아오기 위한 메서드
- setter : 특정 property의 값을 설정하기 위한 메서드

=== "getter"
    ``` javascript
    var dog = {age: 5};
    dog.age; // 5

    Object.defineProperty(dog, "personAge", {get: function() {return this.age * 7}});
    dog.personAge; // 35
    ```
=== "setter"
    ``` javascript
    var dog = {age: 5};
    dog.age = 7;
    dog.age; // 7

    Object.defineProperty(dog, "changeAge", {set: function(n) {this.age = this.age - n;}});
    dog.changeAge = 5;
    dog.age; // 2
    ```


---
!!! quote
    - [TCP School](https://www.tcpschool.com/javascript/intro)