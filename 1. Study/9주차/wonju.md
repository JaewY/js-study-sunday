# 생성자와 클래스 구문

## 생성자

### 생성자를 정의하는 방법

1. 함수 선언문으로 정의

```javascript
function Card(suit, rank) {
  this.suit = suit;
  this.rank = rank;
}
```

2. 함수 리터럴로 정의

```javascript
var Card = function (suit, rank) {
  this.suit = suit;
  this.rank = rank;
};
```

3. 클래스 선언문으로 정의

```javascript
class Card {
  constructor(suit, rank) {
    this.suit = suit;
    this.rank = rank;
  }
}
```

4. 클래스 표현식으로 정의

```javascript
var Card = class {
  constructor(suit, rank) {
    this.suit = suit;
    this.rank = rank;
  }
};
```

1번(함수선언문) 으로 정의한 생성자는 자바스크립트 엔진이 프로그램의 시작부분이나 함수의 시작부분으로 끌어올리지만(호이스팅) 2,3,4번은 끌어올리지 않기 때문에 2,3,4번으로 정의한 생성자는 호출 전에 정의해야 합니다.

---

### 생성자로 접근자 프로퍼티 정의하기

접근자 프로퍼티를 활용하면 9절(객체) 에서 배웠듯이 외부에서 그 프로퍼티를 읽고 쓸 수 없게 막고 특정방법으로만 읽고 쓰게 강제할 수 있습니다. 읽을 때 처리를 담당하는 게터(getter)함수와 쓸 때 처리를 담당하는 세터(setter)함수를 접근자 프로퍼티 하나에 대해 정의할 수 있습니다.

접근자 프로퍼티를 가진 객체 생성하려면

`Object.defineProperty` 나 `Object.defineProperties` 메서드를 호출합니다.
두 메서드는 게터와 세터를 정의하는 기능을 내장하고 있습니다.

```javascript
// name 접근자 프로퍼티를 가진 객체를 생성하는 생성자 정의하기
function Person(name) {
  Object.defineProperty(this, "name", {
    get: function () {
      return name;
    },
    set: function (newName) {
      name = newName;
    },
    enumerable: true,
    configurable: true,
  });
}
Person.prototype.sayName = function () {
  console.log(this.name);
};
```

- Person생성자로 만든 인스턴스의 name프로퍼티는 접근자 프로퍼티이며, 인수로 받은 로컬변수 name값을 읽고 씁니다.

- 인수로 받은 name이 클로저 안에 저장된 프라이빗(private)변수가 됐습니다. 게터함수와 세터함수가 인수로 받은 name을 참조하여 클로저 안에 저장했기 때문입니다.

```javascript
var person = new Person("Tom");
console.log(p.name); // Tom
p.name = "Huck";
console.log(p.name); // Huck
p.sayName(); // Huck
```

## 생성자 상속

자바스크립트는 생성자가 클래스의 역할을 합니다. 자바스크립트는 객체의 프로토타입 상속 메커니즘을 채택한 언어로, 생성자 또 한 객체입니다. 그렇기 때문에 객체의 프로토타입 상속을 활용하면 생성자 상속을 구현할 수 있습니다.

자바스크립트에서는 상속하는 생성자를 **'슈퍼타입 생성자'**, 상속받는 생성자를 **'서브타입 생성자'** 라고 부릅니다.

### 슈퍼타입 생성자의 예

### 생성자의 prototype 상속하기

### 생성자 빌려오기

### 슈퍼타입의 메서드 이용하기

---

## ECMAScript 6의 클래스 구문

> 클래스는 객체 지향 프로그래밍에서 특정 객체를 생성하기 위해 변수와 메소드를 정의하는 일종의 틀로, 객체를 정의하기 위한 상태(멤버 변수)와 메서드(함수)로 구성된다. by 위키백과

앞서 배웠던 new연산자와 생성자 함수에 더하여 ECMAScript 6부터 추가된 클래스(class) 문법을 사용할 수 있습니다.

```javascript
class MyClass {
  // 여러 메서드를 정의할 수 있음
  constructor() {
    this.어쩌구 = 어쩌구;
    this.저쩌구 = 저쩌구;
    ...
   }
  method1() { ... }
  method2() { ... }
  method3() { ... }
  ...
}
```

- 이후 new MyClass()를 호출하면 내부에서 정의한 메서드가 들어있는 객체가 생성

- 객체의 기본상태를 설정해주는 constructor()는 new에 의해 자동호출되기 때문에 특별한 절차 없이 객체를 초기화할 수 있다.

- 다시 말해, class 문법은 new연산자 없이 호출이 불가능하다.

```javascript
// 클래스 선언문
class Person {
  // 여러 메서드를 정의할 수 있음

  constructor(name) {
    this.name = name;
  }

  // Person 이라는 함수를 통해 만들어진 모든 객체가 공유하는 메서드
  sayHi() {
    console.log(`Hi! ${this.name}`);
  }
}

// 사용법
const me = new Person("Lee");
me.sayHi(); // Hi! Lee

console.log(me instanceof Person); // true
```

클래스 표현식

```javascript
let Person = class {
  sayHi() {
    console.log(`Hi! ${this.name}`);
  }
};
```

함수표현식에 이름을 붙일 수 있듯 클래스 표현식에도 이름을 붙일 수 있습니다.

이름을 붙일 경우, 함수표현식과 마찬가지로 이 이름은 클래스 내부에서만 사용가능합니다.

> 함수표현식의 변수는 함수에 붙은 이름이 아니라 할당된 함수를 가리키는 참조값을 저장하게 된다. 함수 호출시 함수명이 아니라 함수를 가리키는 변수명을 사용하여야 한다.

```javascript
let Person = class ThisPerson {
  sayHi() {
    console.log(`Hi! ${this.name}`);
  }
};
const me = new Person();
console.log(me);
// ThisPerson {}

new ThisPerson();
// Uncaught ReferenceError: ThisPerson is not defined
```

### constructor

**constructor**는 인스턴스를 생성하고 클래스 필드를 초기화하는 메서드입니다.

> 클래스필드란?
> 클래스 내부의 캡슐화된 변수. 클래스 필드는 인스턴스의 프로퍼티 또는 정적 프로퍼티가 될 수 있다. 자바스크립트의 생성자 함수에서 this에 추가한 프로퍼티를 클래스 기반 객체지향 언어에서는 클래스 필드라고 부른다.

- constructor는 클래스 내에 한개만 존재 가능하며, 2개 이상이 포함된다면
  문법에러(Syntax Error)가 발생합니다.

- constructor는 생략가능합니다. 그러면 클래스에 `constructor(){}`를 포함한 것처럼 작동합니다. 즉 빈 객체를 생성하는 것입니다.
  인스턴스에 프로퍼티를 추가하려면 인스턴스를 생성한 후 동적으로 프로퍼티를 추가해주어야 합니다.

- constructor는 인스턴스 생성 + 클래스필드의 생성과 초기화를 담당하기 때문에 클래스필드를 초기화해야한다면 constructor를 생략하면 안됩니다.

```javascript
class Foo {}

const foo = new Foo();
console.log(foo); // Foo {}

// 프로퍼티 동적 할당 및 초기화
foo.num = 1;
console.log(foo); // Foo{ num: 1 }
```

---

클래스 선언문과 함수 선언문의 차이점

```
- 클래스 선언문은 호이스팅을 하지 않습니다. 따라서 생성자를 사용하기 전에 클래스 선언문을 작성해야 합니다.

- 클래스 선언문은 한 번만 작성할 수 있으며, 같은 이름을 가진 클래스 선언문을 두 번 이상 작성하면 타입 오류가 발생합니다.

- 클래스 선언문에 정의한 생성자만 따로 호출 불가능합니다.
```

### 접근자 작성하기

```javascript
class Person {
  // 생성자를 사용한 초기화
  constructor(name) {
    this.name = name;
  }
  // prototype 메서드
  get name() {
    return this._name;
  }
  set name(value) {
    this._name = value;
  }
  sayName() {
    console.log(this.name);
  }
}

var person = new Person("Tom");
console.log(person.name); // Tom
person.name = "Huck";
console.log(person.name); // Huck
person.sayName(); // Huck
```

### 정적 메서드 작성하기

클래스 자체에 메서드를 설정할 수 있는 것을 "정적 메서드" 라고 합니다.

정적 메서드는 클래스 안에서 "static" 키워드를 붙여 만듭니다.

정적 메서드는 클래스 이름으로 호출되기 때문에 **클래스의 인스턴스를 생성하지 않아도 호출할 수 있습니다.**

```javascript
class Foo {
  constructor(prop) {
    this.prop = prop;
  }

  static staticMethod() {
    /*
    정적 메소드는 this를 사용할 수 없다.
    정적 메소드 내부에서 this는 클래스의 인스턴스가 아닌 클래스 자신을 가리킨다.
    */
    return "staticMethod";
  }

  prototypeMethod() {
    return this.prop;
  }
}

// 정적 메소드는 클래스 이름으로 호출한다.
console.log(Foo.staticMethod());
// staticMethod

const foo = new Foo(123);
// 정적 메소드는 인스턴스로 호출할 수 없다.
console.log(foo.staticMethod()); // Uncaught TypeError: foo.staticMethod is not a function
```

> 정적 메소드는 Math 객체의 메소드처럼 전역에서 사용할 유틸리티(utility) 함수를 생성할 때 주로 사용한다.

---

### 상속으로 클래스 확장

**상속** 은 코드 재사용 관점에서 매우 유용합니다. 새롭게 사용할 클래스가 기존 클래스와 비슷하다면 상속을 통해 그대로 사용하되 다른 점만 구현하면 되기 때문입니다.

- extends 키워드

부모 클래스(base class)를 상속받는 자식 클래스(sub class)를 정의할 때 사용

```javascript
class Animal {
  constructor(name) {
    this.speed = 0;
    this.name = name;
  }
  run(speed) {
    this.speed = speed;
    console.log(`${this.name} 은/는 속도 ${this.speed}로 달립니다.`);
  }
  stop() {
    this.speed = 0;
    console.log(`${this.name} 이/가 멈췄습니다.`);
  }
}

let animal = new Animal("동물");
```

Animal을 상속받는 Rabbit

```javascript
class Rabbit extends Animal {
  constructor(name, earLength) {
    //부모클래스의 생성자를 호출하는 super
    super(name);
    this.earLength = earLength;
  }

  hide() {
    alert(`${this.name} 이/가 숨었습니다!`);
  }
}

let rabbit = new Rabbit("흰 토끼");

rabbit.run(5); // 흰 토끼 은/는 속도 5로 달립니다.
rabbit.hide(); // 흰 토끼 이/가 숨었습니다!
```

클래스 Rabbit을 통해 만든 객체 rabbit은 Rabbit에 정의된 메서드인 hide()에도 접근할 수 있고, Animal에서 정의된 메서드인 run()에도 접근할 수 있습니다.

프로토타입기반으로 작동하기 때문에 Rabbit.prototype에서 메서드를 찾지 못하면 Animal.prototype에서 메서드를 찾는 것입니다.

메서드 오버라이딩

부모 메서드를 토대로 일부 기능만 변경, 확장, 혹은 메서드 전후에 부모 메서드를 호출하고 싶을 때 **super** 키워드를 사용합니다.

```javascript
class Rabbit extends Animal {
  constructor(name, earLength) {
    super(name);
    this.earLength = earLength;
  }

  hide() {
    console.log(`${this.name}가 숨었습니다!`);
  }

  stop() {
    super.stop(); // 부모 클래스의 stop을 호출해 멈추고,
    this.hide(); // 숨습니다.
  }
}

let rabbit = new Rabbit("흰 토끼");

rabbit.run(5); // 흰 토끼가 속도 5로 달립니다.
rabbit.stop(); // 흰 토끼가 멈췄습니다. 흰 토끼가 숨었습니다!
```

> super 키워드는 반드시 this 를 사용하기 전에 호출해야 에러가 나지 않습니다.

### 슈퍼타입 메서드 호출

---

### 생활코딩

```javascript
function Person(name, first, second) {
  this.name = name;
  this.first = first;
  this.second = second;
}

Person.prototype.sum = function () {
  return "prototype : " + (this.first + this.second);
};

var kim = new Person("kim", 10, 20);
// 위의 Person 이라는 함수 앞에 new 를 붙여주면 객체를 리턴한다.
// this.name 등의 코드로 인해 객체의 속성이 세팅된 객체가 리턴된다는 것이다.
// 그러면 Person이라는 함수는 "생성자함수"가 되며, constructor라 한다.
kim.sum = function () {
  return "this : " + (this.first + this.second);
};
var lee = new Person("lee", 10, 10);
console.log("kim.sum()", kim.sum());
console.log("lee.sum()", lee.sum());

// constructor의 역할: 객체를 만듦 + 객체를 초기화
```

```javascript
// 객체를 만드는 공장 class
class Person {
  // 객체가 생성되기 전에 자동으로 실행되도록 약속된 constructor함수
  constructor(name, first, second) {
    this.name = name;
    this.first = first;
    this.second = second;
  }
  // 메소드는 여기에
  // abc(){
  // 어쩌구저쩌구
  // }
}

var kim = new Person();
console.log("kim", kim);
// kim, Person{} : 이라는 이름의 객체가 생성됨
```

---

생활코딩 상속 class랑 생성자함수 비교

```javascript
// class

class Person {
  constructor(name, first, second) {
    this.name = name;
    this.first = first;
    this.second = second;
  }
  sum() {
    return this.first + this.second;
  }
  // Person.prototype.sum = function () {
  // return this.first + this.second; 해도 똑같이 작동
}

class PersonPlus extends Person {
  constructor(name, first, second, third) {
    // 부모클래스의 생성자호출하는 super
    super(name, first, second);
    this.third = third;
  }
  sum() {
    return super.sum() + this.third;
  }
  avg() {
    return (this.first + this.second + this.third) / 3;
  }
}

var kim = new PersonPlus("kim", 10, 20, 30);
console.log("kim.sum()", kim.sum());
console.log("kim.avg()", kim.avg());
```

```javascript
// 생성자함수

function Person(name, first, second) {
  this.name = name;
  this.first = first;
  this.second = second;
}
Person.prototype.sum = function () {
  return this.first + this.second;
};

function PersonPlus(name, first, second, third) {
  Person.call(this, name, first, second);
  // 위 줄이 class상속에서 super 코드줄과 같음

  // this.name = name;
  // this.first = first;
  // this.second = second;
  this.third = third;
}
// 부모와 연결시키기
PersonPlus.prototype = Object.create(Person.prototype);
PersonPlus.prototype.constructor = PersonPlus;
//PersonPlus.prototype.__proto__ = Person.prototype; : 비표준
PersonPlus.prototype.avg = function () {
  return (this.first + this.second + this.third) / 3;
};

var kim = new PersonPlus("kim", 10, 20, 30);
console.log("kim.sum()", kim.sum());
console.log("kim.avg()", kim.avg());
```

```javascript
var a = new Date();
a.constructor;
// f Date()

var b = new a.constructor();
```

---

### 참고자료

생활코딩유투브
https://www.youtube.com/c/%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A91

모던 JavaScript 튜토리얼
https://ko.javascript.info/class

웹프로그래밍튜토리얼
https://poiemaweb.com/
