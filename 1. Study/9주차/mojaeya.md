# 생성자와 클래스 구문 

1. 함수 선언문으로 생성자 정의 
```javascript
let test = new Card(1,2)

console.log(test) // 호이스팅 ㅇ 

function Card(suit, rank) {
    this.suit = suit
    this.rank = rank 
}
```
2. 함수 리터럴로 생성자 정의
```javascript
let test = new Card(1,2)

console.log(test) // 호이스팅 X

let Card = function(suit, rank) {
    this.suit = suit
    this.rank = rank 
}
```

3. 접근자 프로퍼티를 가진 객체를 정의
```javascript
let person = {
    _name: "Tom",
    get name() {
        return this._name;
    },
    set name(value) {
        var str = value.charAt(0).toUpperCase() + value.substring(1);
        this._name = str;
    }
}

console.log(person.name)
person.name = "mojaeya"
console.log(person.name)
```

4. 접근자 프로퍼티를 가진 객체를 생성하는 생성자 정의 
- 객체를 생성한 후에 접근자 프로퍼티를 추가하거나 생성자 안에 접근자 프로퍼티를 정의하려면 Object.defineProperty나 Object.defineProperties (getter, setter를 정의하는 기능 내장) 메서드 사용.
```javascript
// name 접근자 프로퍼티를 가진 객체를 생성하는 생성자 정의
function Person(name) {
    Object.defineProperty(this, "name", {
        get: function() {
            return name;
        },
        set: function(newName) {
            name = newName;
        },
        enumerable: true,
        configurable: true
    })
}
Person.prototype.sayName = function() {
    console.log(this.name)
}

let p = new Person("Tom")
console.log(p.name)
p.sayName()
```

#### Closure
```javascript
function makeFunc() {
    var name = 'Mozilla';
    function displayName() { // closure
      console.log(name);
    }
    return displayName;
  }
  
  var myFunc = makeFunc();
  myFunc();
  ```

---
# 클래스

ES6부터 추가된 클래스 구문은  기존의 프로토타입 기반 객체지향 모델을 폐지하고 새로운 객체지향 모델을 제공하는 것은 아니다.   
사실 클래스도 함수이며 흔히 기존 프로토타입 기반 패턴의 문법적 설탕(Syntactic sugar)이라고들 하지만,
클래스와 생성자 함수는 모두 프로토타입 기반의 인스턴스를 생성하지만 정확히 동일하게 동작하지는 않는다.
클래스는 생성자 함수보다 엄격하며 생성자 함수에서는 제공하지 않는 기능도 제공합니다. 따라서 클래스를 프로토타입 기반 객체 생성 패턴의 단순한 문법적 설탕이라고 보기보다는 새로운 객체 생성 메커니즘으로 보는 것이 좀 더 적당핟.
클래스 구문을 사용하면 다양한 종류의 생성자 정의문과 생성자 상속 방법을 통일된 문법으로 간결하게 표현할 수 있다.   

## 클래스 선언문

 
class 키워드 뒤에 생성자 함수의 이름을 표기합니다. 이 함수 이름은 클래스 이름이다.   

{...} 안은 클래스 몸통(class body)이다. 클래스 몸통에는 클래스 멤버를 정의한다.   
클래스 멤버는 함수 선언문에서 function 키워드를 생략한 표현식이다.   

클래스의 멤버인 constructor () {...}에는 특별한 의미가 있다. constructor는 생성자로 객체를 생성할 때 초기화 처리를 담당하는 메서드다.     
지금까지 생성자 함수에 작성했던 작업들을 이곳에 작성해서 객체에 프로퍼티를 추가할 수 있다.   

constructor 다음에 작성된 클래스 멤버는 생성자 함수의 prototype에 메서드로 추가된다.
 
클래스 선언문으로 정의한 생성자는 함수 선언문으로 정의한 생성자와 같다. 그러나 클래스 선언문과 함수 선언문은 차이점이 있다.
 
 
❗️ 클래스 선언문과 함수 선언문의 차이점
 
클래스 선언문은 자바스크립트 엔진이 호이스팅하지 않는다. 따라서 생성자를 사용하기 전에 클래스 선언문을 작성해야 한다.   
클래스 선언문은 한 번만 작성할 수 있다. 같은 이름을 가진 클래스 선언문을 두 번 이상 작성하면 타입 오류가 발생.   
클래스 선언문에 정의한 생성자만 따로 호출할 수 없다.   

```javascript
class Person{
   // 생성자를 이용한 초기화
    constructor(name) {
        this.name = name;
    }
   // 프로토타입 메서드
    get name() {
        return this._name;
    }
    set name(value) {
        this._name = value;
    }
    sayName() {
        console.log(this.name)
    }
}

var Person = new Person("Tom")
console.log(person.name)
person.name = "mojaeya"
console.log(person.name)
person.sayName()
```

❗️ constructor가 인수로 받은 name, name 접근자 프로퍼티, _name 프로퍼티는 모두 다른 존재임을 기억!   
또한 getter setter가 Person.prototype에 정의 된다는 점도 기억!   
반면, 4. 접근자 프로퍼티를 가진 객체를 생성하는 생성자 정의 코드에서는 getter setter 모두 pesron 객체 하나에만 연결된 메서드로 정의된다.   

---

>정적 메서드

prototype이 아닌 클래스 함수 자체에도 메서드를 설정할 수 있다. 이런 메서드를 정적(static) 메서드라고 한다. 즉 정적 메서드는 인스턴스 없이 클래스에서 바로 호출이 가능하고 이런 특성 때문에 유틸리티 함수를 만드는데 유용하게 사용된다.

정적 메서드를 선언하는 방법은 아주 간단하다. 메서드 앞에 static키워드를 붙여 선언할 수 있다.

#### 정적 메서드와 프로토타입 메서드의 차이

1. 정적 메서드와 프로토타입 메서드는 자신이 속해 있는 프로토타입 체인이 다릅니다.   
2. 정적 메서드는 클래스로 호출하고 프로토타입 메서드는 인스턴스로 호출합니다.   
3. 정적 메서드는 인스턴스 프로퍼티를 참조할 수 없지만 프로토타입 메서드는 인스턴스 프로퍼티를 참조할 수 있습니다.   

   
## 클래스 상속 

<img width="1343" alt="스크린샷 2021-12-19 오후 7 32 55" src="https://user-images.githubusercontent.com/76654131/146671937-a5415ca3-2379-41ca-99d0-122f6be4de3f.png">

- 프로토타입 문법을 깔끔하게 작성할 수 있는 Class 문법 도입
- Constructor(생성자), Extends(상속) 등을 깔끔하게 처리할 수 있음
- 코드가 그룹화되어 가독성이 향상됨.

<img width="1498" alt="스크린샷 2021-12-19 오후 7 28 58" src="https://user-images.githubusercontent.com/76654131/146671932-6e8b26fe-0520-435a-8e21-93badd7380e4.png">

- 전반적으로 코드 구성이 깔끔해짐
- Class 내부에 관련된 코드들이 묶임
- Super로 부모 Class 호출
- Static 키워드로 클래스 메서드 생성

<img width="1343" alt="스크린샷 2021-12-19 오후 7 33 00" src="https://user-images.githubusercontent.com/76654131/146671939-83008207-4f70-4863-bd59-e6969c49b381.png">



- 참조 및 인용 링크   
[https://poiemaweb.com/es6-class](https://poiemaweb.com/es6-class).  
[https://hyojin96.tistory.com/entry/ES6-class](https://hyojin96.tistory.com/entry/ES6-class).  
[https://wookshin.github.io/2021/12/14/modernjs-25-class.html](https://wookshin.github.io/2021/12/14/modernjs-25-class.html).  
[https://chanyeong.com/blog/post/24](https://chanyeong.com/blog/post/24)
[https://www.inflearn.com/course/노드-교과서/dashboard](https://www.inflearn.com/course/노드-교과서/dashboard)





  
