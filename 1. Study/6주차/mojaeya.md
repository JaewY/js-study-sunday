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
- 함수 안에서 선언된 변수의 유효 범위는 함수 내부인 성질을 이용해 함수를 이름공간으로 활용 할 수 있다.

전역 변수를 줄이기 위해, 즉시 실행 함수를 사용하는 방법이 있다. 이 함수는 선언과 동시에 바로 실행되므로 전역 변수를 만들지 않아, 플러그인이나 라이브러리 등을 만들 때 많이 사용된다. 또한 즉시 실행 함수는 모듈 패턴의 기반이 되기도 한다.

```javascript
var x = "global x";
(function(){
  var x = "local x";
  var y = "local y";
})();
console.log(x); // global x 
console.log(y); // Uncaught ReferenceError: y is not defined
```

### 모듈 패턴 
- 모듈은 기능(함수) 여러개를 하나로 묶은것이다. 일반적으로 모듈은 함수 여러개와 함수가 공유하는 데이터로 구성.
- 모듈은 다양한 곳에서 사용하면 변수 이름이나 함수 이름이 충돌할 가능성이 있다. 그렇기에 모듈도 즉시 실행 함수를 써서 충돌을 막을 수 있다.
- 하지만 함수 안에 있는 함수나 변수는 바깥에서 사용할 수 없기에 즉시 실행 함수에 객체로 구현한 이름 공간을 전역 변수로 넘겨서 공개할 함수를 이름 공간에 추가한다. 이를 통해 모듈의 내부구조는 은폐하고 원하는 함수만 공개 할 수 있다. 

```javascript
var Module = Module || {};
(function(_Module){
	var name = "NoName";
    
    function getName(){
    	return name;
     }
     _Module.showName = function(){
     	console.log(getName());
     }
     _Module.setName = function(){
     	name = x;
     };
})(Module);

Module.setName("Tom");
Module.showName(); //-> Tom;
```
위의 코드에서 showName 메서드는 getName을 참조하고 있으며 setName 메서드는 name을 참조하고 있다. 이로 인해 '클로저'가 생성
즉시 실행 함수의 지연변수 name과 지역함수 getName은 클로저의 내부 상태로 저장된다(=name과 getName은 렉시컬 환경 컴포넌트에서 지워지지 않고 유지되게 된다.) ?????? 아직 클로저 이해 제대로 못함

---

# 콜백 함수 

- 콜백 함수(Callback)는 함수 안에서 어떤 특정한 시점에 호출되는 함수를 말한다.   
- 보통 콜백함수는 함수의 매개변수로 전달하여 특정 시점에서 콜백함수를 호출한다.   
- 쉽게 말하자면 어떤 일을 다른 객체에게 시키고, 그 일이 끝나는 것은 기다리지 않고 끝나고 부를 때까지 다른 일을 하는 것을 말한다.   
- 그렇기 때문에 non-block이며, 비동기 방식의 함수를 사용합니다.
 
즉, 콜백 함수란
1. 다른 함수의 인자로써 이용되는 함수.
2. 어떤 이벤트에 의해 호출되어지는 함수.

콜백함수는 아래와 같은 원리로 작동한다.
 
▶ 함수 정의
```javascript
// 콜백 함수가 될 매개변수 설정
function plus(a, b, callback) {  
  var sum = a + b
  callback(sum) // 매개변수(callback)을 함수 형태로 실행
}
```
plus 함수를 보면 callback 이라는 매개변수를 넣어주고 plus 함수 내부에서 callback 매개변수를 함수 형태로 실행하고 있다.
 
▶ 정의한 함수 호출
```javascript
// 위에서 정의한 plus 함수에 익명 함수를 인자로 전달하며 plus 함수 호출
plus(1, 2, function(result) {  // 콜백 함수 
  console.log(result)   // 3
})
```
위에서 정의한 plus 함수에 익명 함수를 인자로 전달하며 plus 함수를 호출하는 모습이다.
그러면 함수에서 정의하고 있는 로직대로  계산이 되어 sum이 익명 함수로 전달되면서 콘솔에 3을 출력

---

## 콜백 지옥 (Callback Hell)
```javascript
// 따로 따로 선언된 콜백함수 2개와 그냥 출력문 1개
setTimeout(() => {
    console.log('sleep')
}, 3000);
setTimeout(() => {
    console.log('wake up!')
}, 1000);
console.log('eat');

// 출력순서
// eat
// wake up!
// sleep

// ---------------------------------------

// 콜백 헬
setTimeout(() => {
    console.log('sleep')
     setTimeout(() => {
        console.log('wake up!')        
        setTimeout(() => {            
            console.log('eat');
        }, 1000);    
    }, 1000);    
}, 1000);
// 순서대로 출력
```

# ES6부터 추가된 함수의 기능

## 1. 화살표 함수 (arrow function)
<img width="50%" src="https://user-images.githubusercontent.com/76654131/141679525-0920ff32-4cd4-44bc-949d-4982a126ab21.png">

<img width="50%" src="https://user-images.githubusercontent.com/76654131/141679673-d988e664-a49c-4332-a5ca-18a8f6ee460c.png">

 ## 2. 나머지 매개변수
 
 ```javascript
 // 일반함수에서는 arguments 변수 사용 가능 : 가변인자함수
var print = function() {
    var length = arguments.length;

    if(length === 0) {
        console.log('전달된 인자 없어유')
    } else if (length === 1) {
        console.log(arguments[0])
    } else console.log(arguments[0], arguments[1])
}

print()
print(1)
print(1, 2)
 ```
 
### 나머지 매개변수 ...

```javascript
function sum(a, b) {
  return a + b;
}

alert( sum(1, 2, 3, 4, 5) );
```

```javascript
function sumAll(...args) { // args는 배열의 이름입니다.
  let sum = 0;

  for (let arg of args) sum += arg;

  return sum;
}

alert( sumAll(1) ); // 1
alert( sumAll(1, 2) ); // 3
alert( sumAll(1, 2, 3) ); // 6
```

### 앞부분의 매개변수는 변수로, 그 이외의 매개변수들은 배열로 모을 수도 있습니다.
```javascript
function showName(firstName, lastName, ...titles) {
  alert( firstName + ' ' + lastName ); // Julius Caesar

  // 나머지 인수들은 배열 titles의 요소가 됩니다.
  // titles = ["Consul", "Imperator"]
  alert( titles[0] ); // Consul
  alert( titles[1] ); // Imperator
  alert( titles.length ); // 2
}

showName("Julius", "Caesar", "Consul", "Imperator");
```
#### 나머지 매개변수는 항상 마지막에 있어야 합니다.
나머지 매개변수는 남아있는 인수를 모으는 역할을 하므로 마지막이 아닌 부분에 있으면 에러가 발생한다.


[ES6의 심볼, 이터레이터, 제네레이터에 대해 알아보자](https://gist.github.com/qodot/ecf8d90ce291196817f8cf6117036997)

<br>
<br>
<br>

참조 및 인용)
https://jeongah-story.tistory.com/124   
https://ko.javascript.info/rest-parameters-spread   
https://www.youtube.com/watch?v=5kRgzyGRPrU    
https://gist.github.com/qodot/ecf8d90ce291196817f8cf6117036997   







