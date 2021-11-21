# 객체 생성하기

### 객체 생성법
 1) 객체 리터럴
 ```javascript
 var card = {suit: "하트", rank: "A"}
 ```
 2) 생성자
 ```javascript
 function Card(Suit,rank) {
  this.suit = suit;
  this.rank = rank;
 }
 var card = new Card("하트","A");
 ```
 3) Object.create
 ```javascript
 var card = Object.create(Object.prototype,{
     suit: {
        value: "하트",
        writable: true,
        enumerable: true,
        configurable: true
      },
      rank: {
         value: "A",
         writable: true,
         enumerable: true,
         configurable: true
       }
   }); 
  ```
  
### 프로토타입 객체
     - 함수도 객체이므로 함수 객체가 기본적으로 prototupe 프로퍼티를 갖고 있음
     - 함수의 prototupe 프로퍼티가 가리키는 객체를 그 함수의 프로토타입 객체라고 함
     - prototype 프로퍼티는 기본적으로 빈 객체임
   
# 프로토타입 상속
   자바스크립트는 프로토타입 상속에 기반을 둔 객체 지향 언어임
 
 1. 프로토타입 상속이란
      상속이란 일반적으로 특정 객체가 다른 객체로부터 기능을 이어받는 것
      쉬운 말로, 자식이 부모에게 유전자를 물려받는 것과 비슷하다.
      자바스크립트의 상속은 프로토타입 체인이라고 부르는 객체의 자료 구조로 구현되어 있으며, 프로토타입 상속이라고 부름

 2. 프로토타입 상속 이유
    중복 코드를 작성하지 않아도 되므로 유지 보수성이 높은 프로그램을 만들 수 있음
    
 3. 프로토타입 체인이란
      객체의 __proto__ 프로퍼티는 그 객체에게 상속을 해 준 부모 객체를 가리킴
      따라서 객체는 __proto__ 프로퍼티가 가리키는 부모 객체의 프로퍼티를 사용할 수 있음
      
      ```javascript
      function Ultra(){}
      Ultra.prototype.ultraProp = true;
      
      function Super(){}
      Super.prototype = new Ultra();
      
      function Sub(){}
      Sub.prototype = new Super();
      
      var o = new Sub();
      console.log(o.ultraProp);
      ```
 ??
# 접근자 프로퍼티
  접근자 프로퍼티를 사용하면 프로퍼티를 읽고 쓸 때 원하는 작업을 자동으로 처리할 수 있음
  접근자 프로퍼티는 대입할 때와 참조할 때 호출되는 일종읨 ㅔ서드
  
  ### 프로퍼티의 종류
  - 데이터 프로퍼티 : 값을 지정하기 위한 프로퍼티
  - 접근자 프로퍼티 : 값이 없음. 프로퍼티를 읽거나 쓸 때 호출하는 함수를 값 대신에 지정할 수 있는 프로퍼티
  
  ### 접근자 프로퍼티
  접근자란?
  - 객체 지향 프로그래밍에서 객체가 지닌 프로퍼티 값을 객체 바깥에서 읽거나 쓸 수 있도록 제공하는 메서드.
  - 데이터의 부적절한 변경을 막고 특정 데이터를 외부로부터 숨길 수 있으며 외부에서 데이터를 읽으려고 시도할 때 
  적절한 값으로 가공해서 넘길 수 있음.
  
  - 게터 함수 : 프로퍼티 읽을 때의 처리 담당
  - 세터 함수 : 프로퍼티 쓸 때의 처리 담당
   → 접근자 프로퍼티는 getter와 setter 중 하나만 정의할 수도 있지만 모두 정의할 수도 있다.
   접근자 프로퍼티에 getter와 setter를 정의하려면 function 키워드 대신 get이나 set 키워드를 사용한 함수를 작성한다.
  
  
 구분  | getter | setter|
  |----- |-----|-----|
  |인수| 없음| 있음(1개)|
   
   
# 프로퍼티의 속성
  프로퍼티에 속성을 설정하면 사요자가 내장 객체와 유사하게 동작하는 객체를 정의할 수 있게 된다.
  프로퍼티 == 프로퍼티의 이름 + 값 + 내부적인 속성 x개
  
  ### 프로퍼티의 내부 속성
    1. 쓰기 기능 
        : 프로퍼티에 스기가 가능한지를 뜻하는 속성. 이 속성 값이 true면 프로퍼티 값을 수정할 수 있다.
        
    2. 열거 기능 
        : 프로퍼티가 for/in 문이나 Object.keys 등의 반복문으로 찾을 수 있는 대상인지를(열거 가능) 뜻하는 속성
        
    3. 재정의 기능 
        : 프로퍼티의 내부 속성을 수정할 수 있는지를 뜻하는 속성. 
          
          이 속성 값이 true면 delete 연산자로 그 프로퍼티를 제거할 수 있으며 프로퍼티가 가진 내부 속성을 수정할 수 있다. 
    
    
   |데이터 프로퍼티|접근자 프로퍼티|
   |-----|-----|
   |값|읽기|
   |쓰기 가능|쓰기|
   |열거 가능|열거 가능|
   |재정의 가능|재정의 가능|
   
   ### 프로퍼티 디스크립터
     프로퍼티 디스크립터란?
      프로퍼티 속성 값을 뜻하는 객체. 이 객체가 가진 프로퍼티 이름은 프로퍼티가 가진 속성 이름과 같다.
      
      데이터 프로퍼티의 프로퍼티 디스크립터
    
    
    
  __데이터 프로퍼티의 프로퍼티 디스크립터__  
  ```javascript
      { 
        value: 프로퍼티의 값,
        writable: 논리값,
        enumerable: 논리값,
        configurable: 논리값
       }
  ```
 
 __접근자 프로퍼티의 프로퍼티 디스크립터__
 ```javascript
       { 
        get: getter함수값,
        set: setter함수값,
        enumerable: 논리값,
        configurable: 논리값
       }
  ```
    
   ### 프로퍼티 디스크립터 가져오기 : Object.getOwnPropertyDescriptor
      - 첫 번째 인수 : 객체의 참조
      - 두 번째 인수 : 프로퍼티 이름을 뜻하는 문자열
      
   ### 객체의 프로퍼티 설정하기 : Object.defineProperty
      - 첫 번째 인수 : 객체의 참조
      - 두 번째 인수 : 프로퍼티 이름을 뜻하는 문자열
      - 세 번째 인수 : 프로퍼티 디스크립터의 참조. 실행 후에는 객체의 참조를 반환
      
      → 이 메서드를 사용할 때 프로퍼티 디스크립터의 각 프로퍼티는 생략 가능
   ### 객체의 프로퍼티 속성 여러 개를 한꺼번에 설정하기 : Object.defineProperties
      - 첫 번째 인수 : 객체의 참조
      - 두 번째 인수 : 새롭게 설정 또는 변경하고자 하는 프로퍼티 이름이 키로 지정된 프로퍼티 여러 개가 모인 객체. 각 키 값은 프로퍼티 디스크립터의 참조. 실행 후에는 객체의 참조를 반환.
   
      
# 프로퍼티가 있는지 확인하기
## 1. in 연산자
  : 객체 안에 지명한 프로퍼티가 있는지 검색
  : 검색 대상은 그 객체가 소유한 프로퍼티와 상속받은 프로퍼티
```javascript
var person = { name: "Tom" };  // true: 이 객체가 소유한 프로퍼티
console.log("name" in person);  // true: 이 객체가 소유한 프로퍼티
console.log("age" in person);  //  false: 프로퍼티가 없음
console.log("toString" in person);  // true: person은 toString을 상속받았음
```

## 2. hasOwnProperty 메서드
   : 지명한 프로퍼티가 그 객체가 소유한 프로퍼티면 true를 반환
   : 상속받은 프로퍼티면 false를 반환
```javascript
var person = { name: "Tom" };
console.log(person.hasOwnProperty("name"));  // true: 이 객체가 소유한 프로퍼티
console.log(person.hasOwnProperty("toString"));  // false: 상속받은 프로퍼티
```

## 3. propertyIsEnumerable 메서드
   : 지정한 프로퍼티가 그 객체가 소유한 프로퍼티이며 열거할 수 있을 때 true를 반환
```javascript
var person1 = {name: "Tom", age: 17};
var person2 = Object.create(person1);
person2.name = "Huck";
console.log(person2.propertyIsEnumerable("name"));  // true: 이 객체가 소유한 열거 가능 프로퍼티
console.log(person2.propertyIsEnumerable("age"));  // false: 상속받은 프로퍼티
console.log(OObject.prototype.propertyIsEnumerable("toString"));  // false: 열거할 수 없는 프로퍼티
```

# 프로퍼티의 열거
## 1. for/in 문
   :  객체와 객체의 프로토타입 체인에서 열거할 수 있는 프로퍼티를 찾아내어 꺼내는 반복문

```javascript
var person1 = { name: "Tom", age: 17 }:
var person2 = Object.create(person1);
person2.name = "Huck";
for(var p in person2) console.log(p);  // name, age... 순서대로 표시됨
```
이때 eprson2 객체는 person1 객체에서 상속받은 name 프로퍼티 대신 객체 자신이 소유한 name 프로퍼티를 사용하게됨


## 2. Object.keys 메서드
   : 지정한 객체가 소유한 프로퍼티 중에서 열거할 수 있는 프로퍼티 이름만 배열로 만들어서 반환
   : 해당 객체가 소유한 프로퍼티 이름만 조회하는 용도로 적합
```javascript
var group = { groupName: "Tennis circle" };
var person = Object.create(group);
person.name = "Tom";
person.age = 17;
person.sayHello = function() { console.log("Hello! " + this.name); };
Object.defineProperty(person, "sayHello", {enumerable: false});
console.log(Object.keys(person));  // ["name", "age"]
```

## 3. Object.getOwnPropertyNames 메서드
   : 인수로 지정한 객체가 소유한 프로퍼티 이름을 배열로 만들어서 반환.
   : 단, 그때 열거할 수 있는 프퍼티와 열거할 수 없는 프로퍼티의 이름을 모두 배열로 만드는 점이 특징
```javascript
var group = { groupName: "Tennis circle" };
var person = Object.create(group);
person.name = "Tom";
person.age = 17;
person.sayHello = function() { console.log("Hello! " + this.name); };
Object.defineProperty(person, "sayHello", {enumerable: false});
console.log(Object.getOwnPropertyNames(person));  // ["name", "age", "sayHello"]
```
# 객체 잠그기
   : 객체의 확장 가능 속성, 재정의 가능 속성, 쓰기 가능 속성을 설정
   : 잠금 강도에 따라 3단계 잠금이 가능
### 확장 가능 속성
  객체의 확장 가능 속성 : 객체에 새로운 프로퍼티를 추가할 수 있는 지를 결정
  true : 새로운 프로퍼티 추가할 수 있음
  false : 새로운 프로퍼티 추가할 수 없음
  : 사용자가 정의한 객체와 내장 객체는 기본적으로 확장이 가능하지만 호스트 객체의 확장 가능 속성은 자바스크립트 실행 환경에 따라 설정된 값이 다름
### 1. 확장 방지 : Object.preventExtension 메서드
  : 인수로 받은 객체를 확장할 수 없게 만듦
  : 두 번 다시 프로퍼티를 추가할 수 없음
```javascript
var person = { name: "Tom" };
Object.preventExtensions(person);
person.age = 17;
console.log("age" in person);  // false

인수로 지정한 객체가 확장 가능한지 확인하는 메서드
console.log(Object.isExtensible(person));  // false
```

### 2. 밀봉 : Object.seal 메서드
   : 인수로 받은 객체를 밀봉
   : 객체에 프로퍼티를 추가하는 것을 금지하고 기존의 모든 프로퍼티를 재정의할 수 없게 만드는 것
   : 프로퍼티의 추가, 삭제, 수정을 할 수 없고 값의 읽기와 쓰기만 가능

```javascript
var person = { name: "Tom" };
Object.seal(person);
person.age = 17;
delete person.name;
Object.defineProperty(person,"name",{enumerable: flase});
console.log("name" in person);  //true: name이 삭제되지 않았음
consoel.log("age" in person); // false: age가 추가되지 않았음
console.log(Object.getOwnPropertyDescriptor(person,"name"));
// {value: "Huck", writable: true, enumerable: true, confugurable: false}
person.name = "Huck";
console.log(person);  // Object {name: "Huck"}

인수로 받은 객체가 밀봉된 상태인지 확인하는 법
console.log(Object.isSealed(person));  //true
```

### 3. 동결 : Objecet.freeze 메서드
   : 인수로 받은 객체를 동결
   : 객체에 프로퍼티를 추가하는 것을 금지하고 기존의 모든 프로퍼티를 재정의할 수 없게 만들며 데이터 프로퍼티를 쓸 수 없게 만드는 것
   : 즉, 객체를 동결하면 객체의 프로퍼티가 읽기만 가능한 상태가 됨.
 ```javascript
 var person = { name: "Tom" };
 Object.freeze(person);

인수로 받은 객체가 동결된 상태인지 확인하는 법
cosnole.log(Object.isFrozen(person));   true
```

# Mixin
  : 특정 객체에 다른 객체가 가지고 있는 프로퍼티를 붙여 넣어 '뒤섞는' 기법
  : 상속을 사용하지 않는 대신에 특정 객체의 프로퍼티를 동적으로 다른 객체에 추가함
  : 믹스인 사용 전에 우선 객체의 프로퍼티를 복사하는 함수를 만들어야함.
  
# JSON
  : 자바스크립트 객체를 문자열로 표현하는 데이터 포맷
  : 객체를 직렬화할 수 있음
  : 다른 프로그래밍 언어와의 데이터 송수신이 간단해짐
  : 웹 애플리케이션에서는 서버와 웹 클라이언트가 데이터를 주고받을 때 자주 사용
  
 * 표기 방법
 ```javascript
 {name: "Tom", age: 17, marriage: false, data -: [2, 5, null]};
 
 JSON 데이터로 바꾸면
 '{"name":"Tom", "age":17, "marriage":false, "data":[2, 5, null]}'
 JSON 데이터는 그 전체를 작은따옴표로 묶은 문자열!!!
 ```
  
# ECMAScript 6부터 추가된 객체의 기능
  1. 프로퍼티 이름으로 심벌 사용하기
  2. 객체 리터럴에 추가된 기능
   * 계산된 프로퍼티 이름 : { [계산식]: value }
 ```javascript
 var prop = "name", i = 1;
 var obj = { [prop+i]: "Tom" };
 console.log(obj);  // Object {name1: "Tom"}
 var obj = { [Symbol("heart")]: "A" };
 console.log(obj); // Object {Symbol(heart): "A"}
 ```
   * 프로퍼티 정의의 약식 표기 : { prop }
  프로퍼티 이름이 변수이름과 같을 때 { prop }로 줄여서 표현 가능. 프로퍼티 값은 그 변수의 값
 ```javascript
 var prop = 2;
 var obj = { prop } ;
 console.log(obj);  // Object { prop: 2}
 ```
 
   * 메서드 정의의 약식 표기 : { metgod() {} }
 ```javascript
 var person = {
   name: "Tom",
   sayHello() { console.log("Gello! " = this.name); }
  };
  
  person.sayHello();  //"Hello! Tom"
  
  이 코드는 아래와 거의 같다
  
  var person = {
    name: "Tom",
    sayHello: function() { console.log("Hello! " + this.name); }
   };
 ```
 
   * 제너레이터 정의의 약식 표기 : { *generator () {} }
  프로퍼티의 값이 제너레이터 함수일 때 사용할 수 있는 약식 
