# 함수

# 이름 공간 (Namespace)

## 1. 네임스페이스 오염(전역 이름 공간의 오염)
 
✓ 자바스크립트에서 모든 객체는 기본적으로 전역객체의 프로퍼티다.   
아래와 같이 전역 변수, 전역함수를 생성할 때, 그것들은 전역 객체의 멤버로서 생성된다.
```javascript
// 브라우저에서의 window 객체 (window 객체는 브라우저에서 전역 객체이다)
var a = "hello";  // var로 선언한 변수를 전역변수로 사용하면 전역객체의 프로퍼티가 되지만, let,const는 안된다.

console.log(window.a); // "hello" 

function b() {
  return "bye"
}

console.log(window.b()) // "bye"
```
>웹브라우저 자바스크립트에서는 alert()이라는 전역객체의 메소드가 존재하지만 node.js에는 존재하지 않는다.   
또한 전역객체의 이름도 호스트환경에 따라서 다른데, 웹브라우저에서 전역객체는 window이지만 node.js에서는 global이다. 

#### 예시 코드 : 전역변수와 지역변수의 이름이 같을시 가장 가까운 변수를 참조한다.

```javascript
// node에서는 global객체 선언시 아래와 같이 사용한다.
global.num = 10;

function sameNameWithGlobalVariable() {
    var num = 999;
    // 가까운 지역변수를 참조한다.
    console.log('num :', num); // num : 999
    // 전역변수를 접근하고 싶다면 global를 붙인다.
    console.log('global.num :: ', global.num); // global.num : 10
}

sameNameWithGlobalVariable();
console.log('num :', num); // num : 10
console.log('global.num : ', global.num); // global.num : 10
```

---

### 이렇게 자바스크립트는 가령 파일이 분리되어 있더라도 전역스코프를 공유하기 때문에 동일한 이름의 전역변수나 전역함수를 재할당하는 경우 프로그램이 올바르게 작동되지 않을 수 있다. 
### 이를 "네임스페이스 오염(전역 이름 공간의 오염)"이라고 한다. 

```javascript
var globalNum = 99;

function globalScope() {
    console.log('globalNum :', globalNum); // globalNum : 99
    globalNum = 1
}

globalScope();
console.log('globalNum :', globalNum); // globalNum : 1
```

## 2. 객체를 이름 공간으로 활용
자바스크립트는 기본적으로 이름 공간 기능을 제공하지 않기에 객체를 이름 공간으로 활용하고 있다.
- 이름 공간(name space)란 변수 이름과 함수 이름을 한곳에 모아 두어 이름 충돌을 미리 방지

활용 방법 : 객체를 값으로 가지는 전역 변수를 하나 생성하고 그 객체에 프로그램 전체에서 사용하는 모든 변수와 함수를 프로퍼티로 정의

```javascript
//하나의 전역 객체를 생성한다음, 
// 함수,객체, 변수를 g에 추가하여 구현한방법.
// 이름 충돌 방지.
var g = {};
g.num =1;
g.inc = function(){
  console.log('g')
}


// myApp 이라는 전역 변수를 이름 공간으로 활용
var myApp = myApp || {};
console.log(myApp); //{} 

// myApp이 이미 정의되어 있을때는 그것을 사용하고 
// 그렇지 않으면 빈 객체를 myApp에 할당

// 전역 유효 범위에서 사용하고자 하는 
//모든 변수와 함수를 프로퍼티로 추가
myApp.name = "Jalee";
myApp.showName = function() { 
  console.log("showname");
};
myApp.num = 1;
console.log(myApp)  
// myApp만이 사용자가 정의한 전역 변수가 되므로 전역 유효범위 오염을 최소화
//{name: "Jalee", num: 1, showName: ƒ} 


//부분 이름 공간(sub name space) 
myApp.view = {};
myApp.controls = {};

myApp.view.draw = function(){
  console.log("drao");
}
myApp.controls.timeInterval = 16;
console.log(myApp.view); //{draw: ƒ}
console.log(myApp.controls); //{timeInterval: 16}

```

## 3. 함수를 이름 공간으로 활용하기















