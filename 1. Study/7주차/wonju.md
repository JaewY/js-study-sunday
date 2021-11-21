# 객체

## ✅ 객체 생성하기

### 객체 생성하기

- 객체란?

자바스크립트는 객체(object) 기반의 스크립트 언어이며 자바스크립트를 이루고 있는 거의 “모든 것”이 객체

원시 타입(Primitives)을 제외한 나머지 값들(함수, 배열, 정규표현식 등)은 모두 객체

- 키와 값을 한 쌍으로 묶은 집합(프로퍼티)

- 함수의 참조를 값으로 가진 프로퍼티는 메서드

- 객체 생성의 3가지 방법

  1. 객체 리터럴로 생성
     ```javascript
     var card = { suit: "하트", rank: "A" };
     ```
  2. 생성자로 생성
     ```javascript
     function Card(suit, rank) {
       this.suit = suit;
       this.rank = rank;
     }
     var card = new Card("하트", "A");
     ```
  3. Object.create로 생성하는 방법

     ```javascript
     var card = Object.create(Object.prototype, {

         suit: {
             value: "하트",
             writable: true;
             enumerable: true;
             configurable: true
         },
         rank: {
             value: "A",
             writable: true,
             enumerable: true;
             configurable: true
         }
     });
                // ECMAScript 5부터 추가된 방법으로 9.2절부터 배움
     ```

### 프로토타입

- 생성자 안에서 메서드를 정의하는 법의 문제점:

  생성자 안에서 this 뒤에 메서드를 정의하면 그 생성자로 만든 모든 인스턴스에 메서드가 똑같이 추가됩니다. 따라서 메서드 포함한 인스턴스를 여러개 생성하면 각각의 인스턴스만큼 메서드를 생성하게 되며 메모리 소모가 증가합니다.

  > 이러한 문제는 프로토타입 객체에 메서드를 정의해주는 것으로 해결할 수 있다!

```javascript

생성자로 만든것

  function Circle(center, radius) {
    this.center = center;
    this.radius = radius;
    this.area = function(){
      return Math.PI*this.radius*this.radius;
    };
  };
  var c1 = new Circle({ x: 0, y: 0 }, 2.0);
  var c2 = new Circle({ x: 0, y: 1 }, 3.0);
  var c3 = new Circle({ x: 1, y: 0 }, 1.0);

//생성자 안에서 this 뒤에 메서드 정의하면 모든 인스턴스에 똑같은 메서드가 추가
//같은 작업을 하는 메서드를 인스턴스 개수만큼 생성 => 메모리 소비 多

-----------------


  function Circle(center, radius) {
    this.center = center;
    this.radius = radius;
  }
  // Circle 생성자의 prototype 프로퍼티에 area 메서드를 추가
  Circle.prototype.area = function () {
    return Math.PI * this.radius * this.radius;
  };
  // Circle 생성자로 인스턴스 생성
  var c1 = new Circle({ x: 0, y: 0 }, 2.0);
  var c2 = new Circle({ x: 0, y: 1 }, 3.0);
  var c3 = new Circle({ x: 1, y: 0 }, 1.0);
  console.log("넓이 = " + c1.area()); // 넓이 = 12.566370614359172
```

위 코드의 모든 인스턴스 c1, c2, c3 안에는 area 메서드가 없지만 프로토타입객체의 area 메서드를 사용할 수 있습니다.

---

## ✅ 프로토타입 상속

Java, C++과 같은 클래스 기반 객체지향 프로그래밍 언어와 달리 자바스크립트는 프로토타입 기반 객체지향 프로그래밍 언어입니다.

자바스크립트의 모든 객체는 자신의 부모 역할을 담당하는 객체와 연결되어 있으며 프로토타입 상속이라고 부릅니다.

상속은 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 그대로 사용할 수 있는 것을 말하며, 코드의 재사용이란 관점에서 매우 유용합니다.

---

#### prototype 프로퍼티와 내부프로퍼티 [[Prototype]] 프로퍼티

프로토타입 객체

모든 객체는 [[Prototype]] 이라는 내부 슬롯이 있습니다.

객체가 생성될 때 프로토타입이 [[Prototype]]에 저장됩니다. 모든 객체는 프로토타입을 가지며 모든 프로토타입은 생성자함수와 연결되어 있습니다.

[[Prototype]]에는 직접 접근이 불가능하며, \_\_proto\_\_ 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 자신의 [[Prototype]]이 가리키는 프로토타입에 간접적으로 접근이 가능합니다.

그리고 프로토타입 객체는 자신의 constructor 를 통해 생성자함수에 접근할 수 있습니다.

생성자함수는 자신의 프로토타입을 통해 프로토타입에 접근할 수 있습니다.

- prototype 프로퍼티: 함수 객체만 가지고 있는 프로퍼티. 함수 객체가 생성자로 사용될 때 이 함수를 통해 생성될 객체의 부모역할, 즉 어떤 객체가 만들어지기 위해 그 객체의 모태가 되는 객체이며, 속성들

- 내부 프로퍼티 : 모든 객체는 내부 프로퍼티 [[Prototype]] 을 가지고 있습니다.

  ```javascript
  var obj = {};
  console.log(obj.__proto__); //    Object{}
  ```

\_\_proto\_\_프로퍼티는 자신의 부모역할하는 객체, 즉 상속을 해준 부모 객체를 가리킵니다.

> prototype 프로퍼티: 함수의 입장에서 자신과 링크된 자식에게 물려줄 프로토타입 객체를 가리킴

> \_\_proto\_\_ 프로퍼티: 객체의 입장에서 자신의 부모 객체인 프로토타입 객체를 내부의 숨겨진 링크로 가지고 있는 것

### 프로토타입 체인

자바스크립트는 특정 객체의 프로퍼티/메소드에 접근할 때 객체뿐 아니라 \_\_proto\_\_가 가리키는 링크를 따라서 부모역할의 프로토타입 객체의 프로퍼티/메소드에 접근할 수 있습니다.

즉 특정 객체의 프로퍼티/메소드에 접근할 때 해당 프로퍼티가 없다면 부모역할을 하는 프로토타입 객체의 그것들로 차근차근 검색해나가는 것이 프로토타입 체인입니다.

```javascript
const car = {
  wheels: 4,
  drive() {
    console.log("drive...");
  },
};
const bmw = {
  color: "red",
  navigation: 1,
};

const x5 = {
  color: "white",
  name: "x5",
};

bmw.__proto__ = car; // bmw는 car를 상속한다. 다시말해 car는 bmw의 프로토타입

x5.__proto__ = bmw; // x5는 bmw를 상속한다. 다시말해 bmw는 x5의 프로토타입
```

```javascript
생성자 함수로 만들기

const bmw = function (color) {
  this.color = color;
};

bmw.prototype.wheels = 4;
bmw.prototype.drive = function () {
  console.log("drive...");
};
bmw.prototype.navigation = 1;
bmw.prototype.stop = function () {
  console.log("STOP!");
}

  // x5.__proto__ = car; 이거 일일이 쓰기 귀찮으니까 위의 프로토타입 활용
  // z4.__proto__ = car;

const x5 = new bmw("red"); // 생성자함수가 새로운 객체 만들어낼때 그 객체는 '생성자의 인스턴스'라고 한다.
const z4 = new bmw("blue"); // 인스턴스객체에는 constructor라는 프로퍼티 존재. constructor는 생성자, 즉 bmw를 가르킴

  -----------더 깔끔하게-----
const bmw = function (color) {
  this.color = color;
};

  bmw.prototype = {
    wheels: 4,
    drive(){
      console.log("drive...");
    },
    navigation: 1,
    stop(){
      console.log("STOP!");
    },
  }
// 이때는 constructor 사라진다. 쓰지말거나, constructor: bmw 넣어주기
```

![Cap 2021-11-16 18-37-30-619](https://user-images.githubusercontent.com/75517083/142761416-505528eb-a6b0-4d74-983c-db77f25b97f5.jpg)


> 이처럼 차례대로 자신이 갖고 있지 않은 프로퍼티를 \_\_proto\_\_ 프로퍼티가 가리키는 객체를 차례대로 거슬러 올라가며 검색하는 것을 프로토타입 체인이라고 합니다.

<br>

- 실제 프로그래밍을 할 땐 \_\_proto\_\_ 프로퍼티 값을 직접 입력해 상속하지 않습니다.
  보통은

  - 생성자로 객체 생성할 때 생성자의 prototype 프로퍼티에 추가
  - Object.create 메서드(뒤에나옴)로 상속받을 프로토타입을 지정해 객체 생성

    합니다.

프로토타입 가져오기: Object.getPrototypeOf 메서드로 객체의 프로토타입을 가져올 수 있습니다.

```javascript
function F() {}
var obj = new F();
console.log(Object.getPrototypeOf(obj)); // Object{}
```

---

### new 연산자의 역할

생성자를 new연산자로 호출해 인스턴스를 생성하면 나타나는 내부작업

```javascript
 function Circle(center, radius) {
    this.center = center;
    this.radius = radius;
  }
  Circle.prototype.area = function () {
    return Math.PI * this.radius * this.radius;

    var c = new Circle({ x: 0, y: 0 }, 2.0);
```

new 연산자로 Circle 생성자를 사용하면 내부적으로는

```javascript
1. 빈 객체를 생성
var newObj = {};

2. Circle.prototype을 생성된 객체의 프로토타입으로 설정
newObj.__proto__ = Circle.prototype;
// 이때 Circle.prototype이 가리키는 값이 객체가 아니라면 Object.prototype을 프로토타입으로 설정

3. Circle 생성자를 실행하고 newObj를 초기화합니다.
Circle.apply(newObj, arguments);

4. 완성된 객체를 결과값으로 반환합니다.
return newObj;
```

- 2번 에서 생성자의 prototype 프로퍼티값을 인스턴스의 \_\_proto\_\_ 프로퍼티 값으로 대입함으로서 프로토타입체인이 정의되고,

생성자로 만든 모든 인스턴스가 생성자의 프로토타입 객체의 프로퍼티를 사용할 수 있게 됩니다. 이것이 prototype 프로퍼티의 역할입니다.

이렇게 new연산자로 생성자를 호출하면 객체의 생성, 프로토타입설정, 객체초기화를 수행합니다.

### 프로토타입의 확인

특정 프로토타입 객체가 그 객체의 프로토타입 체인에 포함되어있는지 확인하는 방법은 instanceOf연산자, isPrototpypeOf 메서드 가 있습니다.

1. instanceof 연산자: 인스턴스가 생성자의 프로토타입 객체를 상속받았는지 확인. 해당 생성자로 생성되었는지 여부가 아님.

```javascript
객체 instanceOf 생성자

예)

function F(){};
var obj = new F();
console.log(obj instanceof F);  //  true
console.log(obj instanceof Object)  //  true
console.log(obj instanceof Date)    //  false
```

2. isPrototypeOf 메서드: 특정 객체가 다른 객체의 프로토타입체인에 포함되어있는지 확인

```javascript
프로토타입객체.isPrototypeOf(객체)

예)

function F(){};
var obj = new F();
console.log(F.prototype.isPrototypeOf(Obj));    //  true
console.log(Object.prototype.isPrototypeOf(Obj));    //  true
console.log(Date.prototype.isPrototypeOf(Obj));    //  false
```

---

### Object.prototype

Object.prototype 의 메서드는 모든 내장 객체로 전파되며 모든 인스턴스에서 사용할 수 있습니다.

Object 생성자는 내장생성자로 일반적인 객체를 생성합니다.

Object 생성자를 인수 없이 실행하면 빈 객체를 생성합니다.

```javascript

var obj = new Object();
= 객체 리터럴로 작성한 빈 객체와 같음: var obj = {};

인수에 값을 지정하면 그 값을 Object 객체로 변환한 인스턴스를 생성
var obj = new Object("ABC");

Object 생성자는 new 없이 호출해도 new붙여서 호출 한 것과 같은 방식으로 동작
var obj = Object(); // = var obj = new Object();

```

Object 생성자는 일반적인 객체를 조작하기 위한 메서드와 프로퍼티를 제공하는 내장생성자로, 앞서 설명한 Object.create는 Object 생성자의 메서드 중 하나입니다.

Object.create 메서드를 사용하면 프로토타입을 지정해서 객체를 생성할 수 있으며, 간단하게 상속을 표현할 수 있습니다.

Object.create 메서드의 첫번째 인수: 생성할 객체의 프로토타입

두번째 인수: 선택사항이며, 객체의 프로퍼티를 지정가능

```javascript
var person1 = {
  name: "Tom",
  sayHello: function () {
    console.log("Hello! " + this.name);
  },
};
var person2 = Object.create(person1);
person2.name = "Huck";
person2.sayHello(); //  Hello! Huck
```

Person2는 person1의 name프로퍼티와 sayHello메서드(함수형태니까 메서드)를 상속받았으며,

person2 객체는 name 프로퍼티를 이미 가지고 있으므로 person2의 name 프로퍼티값을 사용합니다.

> 프로토타입 체인에서는 해당 객체와 가장 가까운 프로퍼티를 사용합니다!

---

## ✅ 접근자 프로퍼티

프로퍼티는

- 데이터 프로퍼티: 값을 저장하기 위한 프로퍼티
- 접근자 프로퍼티: 값이 없음. 프로퍼티를 읽거나 쓸 때 호출하는 함수를! 값 대신 지정할 수 있는 프로퍼티

로 나눌 수 있습니다. 앞선 프로퍼티는 모두 데이터 프로퍼티이며,

접근자 프로퍼티를 사용해 프로퍼티를 읽고 쓸 수 있게 하면 프로그램의 유지보수성을 높일 수 있습니다.

접근 프로퍼티는 특정 프로퍼티의 값을 받아오기 위한 게터(getter)와 특정 프로퍼티의 값의 설정을 담당하는 세터(setter) 가 있습니다.

getter 메서드는 아무런 인수를 전달받지 않고,

setter 메서드는 대입하고자 하는 인수를 전달받습니다.

접근자 프로퍼티는 내부적으로 Function 객체를 생성하고 호출해 함수처럼 작동하지만 외부적으로는 프로퍼티 형태를 갖고 key값을 통해 접근해 동작합니다.

```javascript
var user = {
  _name: "wonju",
  get name() {
    console.log(`내 이름은 ${this._name}이지만`);
    return this._name;
  },
  set name(value) {
    this._name = value;
    console.log(`${value}가 되었습니다`);
  },
};

user.name;
user.name = "hojae";

//  내 이름은 wonju이지만
// hojae가 되었습니다
```

### 데이터의 캡슐화

즉시실행함수로 클로저를 생성하면 데이터를 객체 외부에서 읽고 쓸 수 없도록 숨기고
접근자 프로퍼티만 읽고 쓰도록 만들 수 있습니다.

---

## ✅ 프로퍼티의 속성

프로퍼티의 3가지 내부 속성 혹은 플래그(flag)는 다음과 같으며 각 속성 값은 논리값(boolean)입니다.

1. 쓰기 가능(writable)

   프로퍼티에 쓰기가 가능한지를 뜻하는 속성으로, 속성값이 true면 프로퍼티 값을 수정할 수 있습니다.

2. 열거 가능(enumerable)

   프로퍼티가 for/in 문이나 Object.keys 등 반복문으로 찾을 수 있는 대상인지(열거 가능한지) 를 뜻합니다.

3. 재정의 가능(configurable)

   프로퍼티의 내부 속성을 수정할 수 있는지를 뜻하는 속성으로, 속성값이 true면 delete 연산자로 프로퍼티를 제거할 수 있고, 내부속성을 수정할 수 있습니다.

   프로퍼티 플래그는 특별한 경우가 아니면 다룰 일이 없으며, 그냥 알던대로 프로퍼티를 만들면 플래그들은 true가 됩니다.

### 프로퍼티 디스크립터와 프로퍼티를 읽고 쓰는 메서드

- 프로퍼티 디스크립터
  프로퍼티의 속성 값을 뜻하는 객체.

```
데이터 프로퍼티의 프로퍼티 디스크립터:
    {
        value: 프로퍼티의 값,
        writable: 논리값,
        enumerable: 논리값,
        configurable: 논리값
    }
접근자 프로퍼티의 프로퍼티 디스크립터:
    {
        get: getter함수값,
        set: setter함수값,
        enumerable: 논리값,
        configurable: 논리값
    }
```

---

- 프로퍼티를 읽고 쓰는 메서드

1.  Object.getOwnPropertyDescriptor 메서드는 객체 프로퍼티의 프로퍼티 디스크립터를 가져옵니다.

첫번째 인수는 객체의 참조(속성찾을 대상객체), 두번째 인수는 프로퍼티 이름을 뜻하는 문자열(설명검색될 속성)입니다.

```javascript
예)
    var tom = { name: "Tom" };
    Object.getOwnPropertyDescriptor(tom, "name");
    //  {value: "Tom", writable: true, enumerable: true, configurable: true}

없는 프로퍼티나 상속받은 프로퍼티를 지정하면 undefined를 반환합니다.
즉 그 객체의 프로퍼티 디스크립터만 가져올 수 있습니다.

Object.getOwnPropertyDescriptor({}, "name");    // undefined
Object.getOwnPropertyDescriptor(tom, "toString");    // undefined
```

2. Object.defineProperty 메서드는 객체의 프로퍼티에 프로퍼티 디스크립터를 설정합니다.

첫번째 인수: 객체의 참조

두번째 인수: 프로퍼티 이름 뜻하는 문자열

세번째 인수: 프로퍼티 디스크립터의 참조

그리고 실행 후 수정한 객체의 참조를 반환합니다.

```javascript
예)
    var obj = {};
    Object.defineProperty(obj, "name", {
        value: "Tom",
        writable: true,
        enumerable: false,
        configurable: true
    });
    Object.getOwnPropertyDescriptor(obj, "name");
    //  {value: "Tom", writable: true, enumerable: false, configurable: true}
```

이 메서드를 사용할 때 프로퍼티 디스크립터의 각 프로퍼티는 생략이 가능하고,

일부 프로퍼티 생략 후 특정 객체에 새로운 프로퍼티를 추가하면 그 프로퍼티의 속성값 중 생략한 프로퍼티에 대응하는 속성값이 false 또는 undefined로 설정됩니다.

```javascript
var person = { name: "Tom" };
Object.defineProperty(person, "name", {
  writabale: false,
});
Object.getOwnPropertyDescriptor(person, "name");
//  {value: "Tom", writable: false, enumerable: false, configurable: true}
person.name = "Huck";
console.log(person.name); // 그대로 Tom
```

3. Object.defineProperties 메서드는 객체가 가진 프로퍼티 여러개를 한번에 정의할 수 있습니다.

```javascript
Object.defineProperties(user, {
  name: { value: "John", writable: false },
  surname: { value: "Smith", writable: false },
  // ...
});
```

### Object.create 의 두번째 인수

Object.create() 메소드의 첫 번째 인수로는 프로토타입으로 사용할 객체를 전달합니다.

두 번째 인수로는 새로운 객체의 추가할 프로퍼티 정보를 전달합니다.

## ✅ 프로퍼티가 있는지 확인하기

자바스크립트는 객체를 생성한 후 프로퍼티를 추가/제거 할 수 있기 때문에 객체에 포함된 프로퍼티가 동적으로 바뀝니다.

그렇기 때문에 원하는 프로퍼티가 있는지 확인할 필요성이 있습니다.

또한 객체가 소유한 프로퍼티와 프로토타입으로 상속받은 프로퍼티를 구분할 필요도 있기 때문에 앞서 말한 것들을 확인해야 합니다.

### 1. in 연산자

4장(객체의 기초)에서 배운 in연산자는 객체안에 찾고싶은 프로퍼티가 있는지 검색하고, 검색대상은 객체소유 프로퍼티와 상속받은 프로퍼티 모두 입니다.

```javascript
var person = { name: "Tom" };
console.log("name" in person); // true : 이 객체가 소유한 프로퍼티
console.log("age" in person); // false: 없는 프로퍼티
console.log("toString" in person); // true: person은 toString을 상속받음(Object.prototype의 메서드)
```

### 2. hasOwnProperty 메서드

hasOwnProperty 메서드는 선택한 프로퍼티가 객체가 소유한 프로퍼티면 true, 상속받은 프로퍼티면 false를 반환합니다.

```javascript
var person = { name: "Tom" };
console.log(person.hasOwnProperty("name")); // true: 이 객체가 소유한 프로퍼티
console.log(person.hasOwnProperty("toString")); // false: 상속받은 프로퍼티 : Object.prototype에서 상속받은 메서드임.
```

### 3. propertyIsEnumerable 메서드

propertyIsEnumerable 메서드는 지정한 프로퍼티가 객체가 소유한 프로퍼티 + 열거할 수 있을 때 true를 반환합니다.

```javascript
var person1 = { name: "Tom", age: 17 };
var person2 = Object.create(person1);
person2.name = "Huck";
console.log(person2.propertyIsEnumerable("name"));
//  true: 이 객체가 소유한 열거가능 프로퍼티
console.log(person2.propertyIsEnumerable("age"));
//  false: 상속받은 프로퍼티
console.log(Object.prototype.propertyIsEnumerable("toString"));
//  false: 열거할 수 없는 프로퍼티
```

## ✅ 프로퍼티의 열거

객체 안의 프로퍼티 열거방법을 알면 객체안의 모든 프로퍼티를 대상으로 작업을 수행할 수 있고, 프로퍼티 목록을 가져올 수 있습니다.

### for/in 문

7장(제어구문)에서 배운 '객체 안의 프로퍼티를 순회' 하는 반복문입니다.

```javascript
var person1 = { name: "Tom", age: 17 };
var person2 = Object.create(person1);
person2.name = "Huck";
for (var p in person2) console.log(p); // name, age... 순서대로 표시됨
```

### Object.keys 메서드

Object.keys 메서드는 지정한 객체가 소유한 프로퍼티 중 열거할 수 있는 프로퍼티 이름만 배열로 만들어 반환합니다.

```javascript
var group = { groupName: "pizza circle"};
var person = Object.create(group);
person.name = "Tom";
person.age = 17;
person.sayHello = function() {console.log("Hello! " + this.name;)};
Object.defineProperty(person, "sayHello", {enumerable: false});
console.log(Object.keys(person));   // ["name", "age"]
```

person 객체가 소유한 프로퍼티는 name, age, sayHello와, group에서 상속받은 groupName 입니다. Object.prototype에서 상속받은 프로퍼티도 사용 가능합니다.

Object.keys 메서드는 이 중 객체가 소유하면서 열거가능한 프로퍼티인 name과 age의 이름만 배열로 만들어 반환합니다.

해당 객체가 소유한 프로퍼티 이름만 조회하는 용도로 적합합니다.

### Object.getOwnPropertyNames 메서드

Object.getOwnPropertyNames 메서드는 Object.keys 메서드와 같이 객체가 소유한 프로퍼티 이름을 배열로 만들어 반환하고, 열거할 수 없는 프로퍼티 이름도 모두 배열로 만들어 반환한다는 차이가 있습니다.

앞선 예시의 person 객체에서 Object.getOwnPropertyNames메서드를 사용한다면

```javascript
console.log(Object.getOwnPropertyNames(person));
//  ["name", "age", "sayHello"] : 열거할 수 없는 "sayHello"도 열거
```

## ✅ 객체 잠그기

객체를 잠글 때는 객체확장가능/재정의가능/쓰기가능 속성을 설정합니다.

### 1. 확장 가능 속성

새로운 프로퍼티를 추가할 수 있는지를 결정합니다. 확장가능속성값이 true인 객체는 프로퍼티를 추가할 수 있지만, false인 객체는 불가능합니다.

### 2. 확장방지 Object.preventExtensions 메서드

Object.preventExtensions 메서드는 인수로 받은 객체를 확장할 수 없게 만듭니다. 그 객체는 프로퍼티를 더이상 추가할 수 없습니다.

```javascript
var person = { name: "Tom" };
Object.preventExtensions(person);
person.age = 17;
console.log("age" in person); //  false
```

person 이라는 객체를 확장할 수 없게 만들어 age 프로퍼티를 추가해도 false가 출력되는 것을 알 수 있습니다.

Object.isExtensible 메서드를 사용하면 인수로 지정한 객체가 확장가능한지 알아볼 수 있습니다.

```javascript
console.log(Object.isExtensible(person)); // false
```

### 3. 재정의 방지 Object.seal 메서드

Object.seal 메서드는 인수로 받은 객체를 밀봉(프로퍼티추가+기존프로퍼티 재정의 불가능)합니다. 오직 **읽기와 쓰기** 만 가능해집니다.

```javascript
var person = { name: "Tom" };
Object.seal(person);
person.age = 17;
delete person.name;
Object.defineProperty(person, "name", { enumerable: false });
console.log("name" in person); // true : name이 삭제되지 않음
console.log("age" in person); // false : age가 추가되지 않음
console.log(Object.getOwnPropertyDescriptor(person, "name"));
//  {value: "Huck", writable: true, enumerable: true, configurable: false}
person.name = "Huck";
console.log(person); // Object {name: "Huck"}
```

밀봉된 객체를 대상으로 한 프로퍼티의 추가/삭제/수정은 무시됩니다.

Object.isSealed 메서드를 통하면 인수로 받은 객체가 밀봉된 상태인지 확인할 수 있습니다.

```javascript
console.log(Object.isSealed(person)); // true
```

### 4. 쓰기 가능 방지 Object.freeze 메서드

Object.freeze 메서드는 인수로 받은 객체를 동결(추가/재정의/쓰기 불가능)합니다. 다시말해 객체의 프로퍼티가 읽기만 가능한 상태입니다.

단, 객체에 접근자 프로퍼티가 정의되어 있다면 게터/세터 함수 모두 호출할 수 있습니다.

```javascript
var person = { name: "Tom" };
Object.freeze(person);
```

이렇게 설정하면 person 객체의 프로퍼티는 읽기만 가능합니다.

Object.isFrozen 메서드를 사용하면 인수로 받은 객체가 동결된 상태인지 확인가능합니다.

```javascript
console.log(Object.isFrozen(person)); // true
```

## ✅ Mixin(믹스인)

### Mixin 함수

믹스인은 상속을 사용하지 않는 대신 특정 객체의 프로퍼티를 다른 객체에 '복사'해서 사용하는 방식 입니다.

```javascript
function mixin(receiver, supplier) {
  for (var property in supplier) {
    if (supplier.hasOwnProperty(property)) {
      receiver[property] = supplier[property];
    }
  }
  return receiver;
}
```

첫 번째 객체 receiver는 두 번째 객체인 supplier로 부터 프로토 타입을 복사 받습니다.

supplier의 프로퍼티들을 순회하면서 프로토 타입이 같을 경우에만 첫 번째 객체 receiver에 복사해서 주는 방식입니다.

```javascript
var obj1 = { a: 1, b: 2 };
var obj2 = { b: 3, c: 4 };
var obj = mixin(obj1, obj2);

console.log(obj);
//  Object {a: 1, b: 3, c: 4}
```

이미 obj1에 있는 프로퍼티 값은 덮어쓰고 obj1에 없는 프로퍼티는 추가합니다.

이 방식은 얕은 복사로, 프로퍼티 값이 객체이면 receiver와 supplier가 같은 객체를 가르킵니다.

## ✅ JSON

JSON은 자바스크립트 객체를 문자열로 표현하는 데이터 포맷입니다.

JSON 표현식은 사람과 기계 모두 이해하기 쉬우며 용량이 작아서, 최근에는 JSON이 XML을 대체해서 데이터 전송 등에 많이 사용합니다.

### 표기법

JSON포맷은 자바스크립트의 리터럴 표기법과 유사합니다.

다음과 같은 객체 리터럴은

```javascript
{name: "Tom", age: 17, marriage: false, data: [2, 5, null]};
```

JSON 데이터로 바꾸면 다음과 같습니다.

```javascript
'{"name":"Tom", "age":17, "marriage":false, "data":[2, 5, null]}';
```

- JSON 데이터는 전체를 **작은 따옴표** 로 묶은 문자열입니다.

- 객체의 프로퍼티 이름은 큰따옴표로 묶은 문자열입니다.

- 숫자, 논리값, 배열 등은 자바스크립트의 표기법과 같지만 문자열만큼은 큰따옴표로 묶어야 합니다.

### JSON 변환과 환원

- 자바스크립트 객체를 JSON문자열로 변환: JSON.stringify

#### JSON.stringify 메서드는 인수로 받은 객체를 JSON 문자열로 변환합니다.(=직렬화)

```javascript
JSON.stringify(value, replacer, space);
```

첫번째 인수: 변환할 객체
두번째 인수인 replacer: 함수 또는 배열로 지정
세번째 인수인 space: 출력하는 문자열 구분할 때 사용할 공백 문자 지정

1. 변환할 객체

```javascript
JSON.stringify({}); // '{}'
JSON.stringify(3.14); // '3.14'
JSON.stringify("abc"); // '"abc"'
JSON.stringify(true); // 'true'
JSON.stringify([2, 4, null]); // '[2, 4, null]'
JSON.stringify({ x: 1, y: 2 }); // '{"x":1, "y":2}'
```

2. 인수로 배열 지정하기:

```javascript
JSON.stringify({ x: 1, y: 2, z: 3 }, ["x", "z"]); //  '{"x":1, "z":3}`

//원본객체 프로퍼티 중 두번째 인수의 배열요소와 이름이 같은 프로퍼티만 걸러짐
```

3. 인수에 문자열 구분 위한 공백문자 지정(탭 문자)

```javascript
JSON.stringify({ x: 1, y: 2 }, null, "\t");
//  '{
//       "x":1,
//       "y":2
//  }'
```

JSON.stringify 메서드 사용시 유의점

- NaN, Infinity, -Infinity는 null로 직렬화
- Function, RegExp, Error 객체, undefined, 심벌은 직렬화X
- 객체 자신이 가진 열거 가능한 프로퍼티만 직렬화
- 직렬화할 수 없는 프로퍼티는 문자열로 출력X
- 프로퍼티 중 키가 심벌인 프로퍼티는 직렬화X

#### JSON 문자열을 자바스크립트 객체로 환원하기: JSON.parse

JSON.parse 메서드는 인수로 받은 문자열을 자바스크립트 객체로 환원해 반환합니다.

```javascript
JSON.parse(text, replacer);
```

첫번째 인수: 자바스크립트의 객체로 환원하고자 하는 JSON문자열
두번째 인수: 프로퍼티키와 값을 인수로 받는 함수 지정(선택)

사용법은 JSON.stringify 메서드와 똑같으며, 거꾸로 써주기만 하면 됩니다.

## ✅ ECMAScript 6 부터 추가된 객체의 기능

### 프로퍼티 이름으로 심벌 사용하기

ECMAScript 6 부터는 프로퍼티이름으로 식별자/문자열 뿐만 아니라 심벌도 사용할 수 있습니다.

```javascript
var obj = { [Symbol("heart")]: "A" };
```

이름이 심벌로 지정된 프로퍼티는 ECMAScript6 부터 추가된 Object.getOwnPropertySymbols 메서드를 이용해 이름을 심벌로 지정한 프로퍼티 이름 목록을 가져올 수 있지만,

그밖에 for/in반복문, Object.keys, Object.getOwnPorpertyNames 로는 찾아낼 수 없습니다.

- 심벌을 사용하면 이름을 겹치는 걸 방지하면서 기본생성자의 프로토타입을 확장할 수 있어서 Array, Date 등 기본 생성자의 프로토타입을 안전하게 확장할 수 있습니다.

### 객체 리터럴에 추가된 기능

객체 리터럴에 새로운 표기법이 추가되었습니다.

1. 계산된 프로퍼티 이름 : { [계산식]: value}

계산식이 평가된 값을 프로퍼티 이름으로 사용할 수 있습니다. 평가값이 Symbol타입이라면 그대로, 그렇지 않으면 문자열 타입으로 변환합니다.

```javascript
var prop = "name",
  i = 1;
var obj = { [prop + i]: "Tom" };
console.log(obj); //  Object {name1: "Tom"}

var obj = { [Symbol("heart")]: "A" };
// 심벌을 프로퍼티 이름으로 사용하려면 심벌을 대괄호로 묶어주기
console.log(obj); //  Object {Symbol(heart): "A"}
```

2. 프로퍼티 정의의 약식 표기 : { prop }

프로퍼티 이름이 변수 이름과 같을 때 { prop } 으로 줄여서 표현할 수 있습니다.
프로퍼티 값은 그 변수의 값이 됩니다.

```javascript
var prop = 2;
var obj = { prop };
console.log(obj); //  Object {prop: 2}
```

3. 메서드 정의의 약식 표기 : { method ( ) }

프로퍼티 값으로 함수를 지정할 때 사용하는 약식 표기법이 추가되었습니다.

```javascript
var person = {
  name: "Tom",
  sayHello(){ console.log("Hello! " + this.name);}
};
person.sayHello();  //  "Hello! Tom"

------------------------------------------------------------
var person = {
  name: "Tom",
  sayHello: function(){ console.log("Hello! " + this.name);}
};

```

4. 제너레이터 정의의 약식 표기: { \*generator ( ) { } }

프로퍼티 값이 제너레이터 함수일 때 사용할 수 있는 약식 표기법입니다.

---

참고자료

https://iamsjy17.github.io/javascript/2019/06/10/js33_17_prototype.html

http://vnthf.logdown.com/posts/2016/03/18/650616

https://www.youtube.com/watch?v=ddJcDZHBRm0
