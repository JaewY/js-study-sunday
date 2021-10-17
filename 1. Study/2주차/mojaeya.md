# 함수
- 함수는 프로그램을 구성하는 주요 '구성 요소(building block)'입니다.
- 함수를 이용하면 중복 없이 유사한 동작을 하는 코드를 여러 번 호출할 수 있다.

# 함수 선언 및 호출
<img width="50%" src="https://user-images.githubusercontent.com/76654131/137621650-c7969034-2596-4ae4-ae59-946ca6dc8273.png">

- 함수 호출할 때 전달하는 값 : 인수 (argument)
- 함수 선언문의 인수 : 인자=매개변수 (parameter)
- 함수의 출력값 : 반환값
# 인수
- 함수는 인수를 여러개 받을수도, 안받을수도 있다.
- 자바스크립트 함수는 리턴값이 없어도 항상 리턴값을 반환!!!
```javascript
let 원주 = function() { console.log("바보")}
console.log(원주()) // undefined
```
# 함수 선언문 끌어올림 (hoisting)
- 변수 선언문 호이스팅처럼 함수 선언문을 프로그램의 첫머리로 끌어올린다.
- 그래서 함수 선언문은 프로그램의 어떤 위치에도 작성해도 문제없이 작동!!!
```javascript
conosole.log(square(5) // 25
function square(x) { return x * x }
```

# 함수 리터럴로 정의한 함수는 hoisting X
- 함수 선언문 끝에 세미콜론이 있으면, 함수 리터럴로 정의한 익명함수(무명함수)이다.
- 일반적인 함수선언문과 사용법은 같은데, 함수 리터럴로 정의한 함수는 호이스팅이 안된다.
- 그래서 아래처럼 정의하지 않은 상태에서 함수를 호출하면 타입 오류 발생
```javascript
conosole.log(square(5) // TypeError : square is not a function
function square(x) { return x * x };
```

# 함수 안에서의 변수 선언과 변수 hoisting
- 함수 안에서 선언된 지역변수의 유효범위는 함수 전체이다.
즉, 일반적인 변수선언문의 호이스팅과 마찬가지로 함수안의 변수 선언부를 함수의 첫머리로 끌어올린다.
```javascript
function f() {
   console.log(a) // undefined
   var a = "local".  // var => 변수 선언을 생략하면, 전역변수로 선언되는거 주의!
   console.log(a) // local
   retuan a
}
```

# 자바스크립트에서는 함수가 객체이다
- 즉 함수의 기본 기능인 코드 실행뿐만 아니라, 함수 자체가 일반 객체처럼 프로퍼티들을 가질 수 있다.
```javascript
function add(x, y) { return x+y }

add.result = add(3,2)
add.status = 'ok'

console.log(add.result) // 5
console.log(add.status) // 'ok'
```
#### 📌 자바스크립트 함수는 다음과 같은 동작이 가능하기에 "일급 객체" 라고도 부른다.
- 리터털에 의해 생성
- 변수나 배열의 요소, 객체의 프로퍼티 등에 할당 가능
- 함수의 인자로 전달 가능
- 함수의 리턴값으로 리턴 가능
- 동적으로 프로퍼티를 생성 및 할당 가능

# 참조에 의한 호출
- 함수는 원시값을 인수로 넘겼을 때랑, 객체를 인수로 넘겼을 때 다르게 동작한다.
- 왜냐하면, 원시값과는 다르게 변수에 객체의 참조가 저장되기 떄문이다.
```javascript
// 원시값을 인수로 넘길 경우
function add1(x) { return x = x+1 }
var a = 3
var b = add1(a) // 값의 전달(복사) => 변수 a와 x는 다른 메모리에 위치한 별개의 변수
console.log("a = " + a + ", b = " + b) // a = 3, b = 4

// 객체를 인수로 넘길 경우
function add1(p) {
    p.x = p.x + 1
    p.y = p.y + 1
    return p
}
var a = {x:3, y:4}
var b = add1(a) // 참조 전달 => 변수 a와 인자 p가 똑같은 객체를 참조하고 있는거임
console.log(a, b) // Object {x=4, y=5} Object {x=4, y=5}
```

# 인수 여러개를 우아하게 전달해보자
#### 함수에 넘거야 하는 인수 개수가 많아지면 발생하는 문제
- 인수의 순서를 착각하기 쉽다.
- 함수가 받는 인수 개수를 바꾸면, 함수의 호출 방법이 바뀌므로 프로그램 전체를 수정해야하는 대참사

```javascript
// 인수가 많은 함수
function setBallProperties(x, y, vx, vy, radius){...}
...
setBallProperties(0, 0, 10, 15, 15)

// 객체의 프로퍼티에 담아서 함수에 넘김
var parameters = {
	x: 0, y: 0, vx: 10, vy: 15, radius: 5
 };
 function setProperties(params) {...}
 ...
 setBallProperties(parameters)
 
 이렇게 하면, 인수를 추가하는 경우 객체에 프로퍼티만 추가하면 되기 때문에 간편!
 
 단, 함수 안에서 객체의 프로퍼티를 수정하면, 호출한 코드에 있는 인수 객체의 프로퍼티가 함께 바뀌므로 주의!
 => 객체를 인수로 넘기면, 함수에는 객체의 참조가 전달되기 때문이다.
```

# 변수의 유효범위
- 변수에 접근할 수 있는 범위 : 유효범위 
```javascript
// 전역변수 a의 유효범위와 지역변수 b의 유효범위
var a = "global";
function f(){
	var b = "local";
    console.log(a); // "global"
    return b;
}
f();
console.log(b); ReferenceError: b is not defined
```

# 변수의 충돌
- 변수에 유효범위가 있는 이유는 프로그램의 다른 부분에서 선언된 이름이 같은 변수와 충돌하지 않기 위함.   
덕분에 함수안에서 변수 이름 지을 때 신경 안쓰고 지어도 된다. 
- 하지만, 전역 변수 이름과 지역 변수 이름이 같으면 충돌한다. 이때는 아래처럼 전역변수를 숨기고 지역변수를 사용하게 된다.
```javascript
var a = "global"
function f() {
    var a = "local"
    console.log(a) // local
    return a
}
f();
console.log(a) // global
```
# 블록 유효 범위 : let 과 const
- var로 선언한 변수와 let으로 선언한 변수의 가장 큰차이점은 let으로 선언한 변수의 유효 범위가 블록 안이라는 점이다.
```javascript
// let으로 선언한 변수의 유효범위
let x = "outer x"
{
	let x = "inner x"
  let y = "inner y"
  console.log(x); // inner x
  console.log(y); // inner y
}
console.log(x)	// outer x
console.log(y)  // ReferenceError : y is not defined
```
- var 문으로 선언한 변수를 읽으려고 시도할때 오류가 발생하지 않는것과 대조적 (TDZ)
```javascript
console.log(x) // ReferenceError: x is not defined
let x = 5
```
👋 const문으로 선언한 상수값은 수정 불가능하다고 변수 시간에 배웠는데, 상수 값이 객체나 배열인 경우는 수정 가능하다~


# 객체의 메서드 : 1주차 mojaeya 정리 참조








