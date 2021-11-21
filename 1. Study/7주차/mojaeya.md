# 객체
## 객체의 생성
```javascript
// 1. 객체 리터럴로 생성하는 법
var card = {suit: "하트", rank: "A"}

// 2. 생성자로 생성하는 법
function Card(Suit,rank) {
 this.suit = suit;
 this.rank = rank;
}
var card = new Card("하트","A");

// 3. Object.create로 생성하는 방법 
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

## 프로토타입
### 생성자 안에서 메서드를 정의하는 방식의 문제점 
- 생성자 안에서 this 뒤에 메서드를 정의하면 그 생성자로 생성한 모든 인스턴스에 똑같은 메서드가 추가 된다. 그래서 메모리를 많이 소비하게 된다. 

```javascript
function Circle(center,radius) {
    this.center = center;
    this.radius = radius;
    this.area = function() {
        return Math.PI*this.radius*this.radius;
    };
}
var c1 = new Circle({x:0, y:0}, 2.0);
var c2 = new Circle({x:0, y:1}, 3.0);
var c3 = new Circle({x:1, y:0}, 1.0);
```
- 각각의 인스턴스가 똑같은 메서드 area를 소유한다.
<p align="center"><img width="70%" src="https://user-images.githubusercontent.com/76654131/142760833-6e7c177d-3c42-4cde-bb5d-5f7e77771d22.png">
</p>

## 프로토타입 객체 
- 자바스크립트에서는 함수도 객체이므로 함수 객체가 기본적으로 prototype 프로퍼티를 갖고 있다. (__proto__ 프로퍼티랑은 다른거다!)
```javascript
function F() {};
console.log(F.prototype) // Object {}
```
- prototype 속성은 자신의 prototype 객체로 자식 객체(생성자로 생성한 인스턴스)가 참조하는 객체이다.

<p align="center"><img width="50%" src="https://user-images.githubusercontent.com/76654131/142761533-1a3ba4f8-2565-471d-b029-53a1d9152faa.png"></p>

- 프로토타입 객체의 프로퍼티는 생성자로 생성한 모든 인스턴스에서 그 인스턴스의 프로퍼티처럼 사용 가능하다.
```javascript
F.protoype.prop = "prototype value";
var obj = new F(); 
console.log(obj.prop); // prototype value
```
#### 🔥 프로토타입 객체의 프로퍼티는 읽기만 가능하고 수정이 불가능!!!
```javascript
// 인스터스의 프로퍼티에 값을 대입했을 때 이름이 같은 프로퍼티가 있으면 그 프로퍼티에 값을 대입.
obj.prop = "instance value"; //  그렇지 않은 경우 인스턴스에 그 이름으로 프로퍼티를 추가한 후에 값을 대입
console.log(obj.prop); // instance value
console.log(F.prototype.prop); // prototype value
```

### ✓ 이렇게 프로토타입 객체의 프로퍼티를 인스터스에서 참조할 수 있는 상황을 가리켜 '인스턴스가 프로토타입 객체를 상속하고 있다' 라고 한다.

#### 📌 앞에서 얘기한 생성자 안에서 메서드를 정의하는 방식의 문제점을 해결하는 법 (메모리 낭비 피하는 법)
```javascript
// Circle 생성자
function Circle(center,radius) {
    this.center = center;
    this.radius = radius;
}
// Circle 생성자의의 prototype 프로퍼티에 area 메서드를 추가
Circle.prototype.area = function() {
  return Math.PI*this.radius*this.radius;  // 메서드 안의 this는 생성자로 생성한 인스턴스를 가리킨다.
};
// Circle 생성자로 인스턴스를 생성
var c1 = new Circle({x:0, y:0}, 2.0);
var c2 = new Circle({x:0, y:1}, 3.0);
var c3 = new Circle({x:1, y:0}, 1.0);
console.log("넓이 = " + c1.area()); // 넓이 = 12.566370614359172
```

- 위의 코드에서 인스턴스 c1,c2,c3 안에는 area 메서드가 존재하지 않지만 프로토타입에 정의했기 때문에 area 메서드를 사용할 수 있다.
- 이처럼 생성자의 프로토타입 객체에 메서드를 추가하면 인스턴스에 메서드를 추가하지 않아도 인스턴스가 프로토타입 객체의 메서드를 상속 받아 사용 할 수 있어 메모리 낭비를 피할 수 있다.
<p align="center"><img width="70%" src="https://user-images.githubusercontent.com/76654131/142762495-2233e2be-ffc5-472e-9e80-bf7b9bbb7d99.png">
</p>

---

## 프로토타입 상속











