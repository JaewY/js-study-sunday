# 이름 공간

전역 변수와 전역 함수를 함수 객체에 선언하는 행위를 '전역 유효 범위를 오염시킨다'라고 합니다. 다음과 같은 상황에서 변수&함수의 이름이 겹칠 수 있습니다.

- 라이브러리 파일을 여러 개 읽어 들여 사용할 때
- 규모가 큰 프로그램을 만들 때
- 여러 사람이 한 프로그램을 만들 때

문제: 목적이 다른 코드가 같은 변수나 함수를 공유하여 오류가 발생할 가능성 ⬆ + 프로그램 오류 표시가 뜨지 않기 때문에 문제점을 찾기도 쉽지 않음

> 프로그램 오류를 피하기 위해 전역 유효 범위의 오염을 최소화해야 합니다

---

## 방법 1. 객체를 이름 공간으로 활용하기

자바스크립트는 C++이나 Java 등과는 달리 기본제공을 하지 않습니다.

이름 공간이란?

- 변수 이름과 함수 이름을 한곳에 모아두어 충돌을 미리 방지 + 쉽게 가져다 쓸 수 있도록 만든 메커니즘

- 대신 자바스크립트는 객체를 이름 공간으로 활용할 수 있습니다.

  객체를 값으로 갖는 전역 변수를 생성하고 이름 공간으로 활용하기!

```javascript
var myapp = myapp || {};
```

전역 변수 myapp이 이미 정의되어 있으면 그것을 사용하고, 그렇지 않으면 빈 객체를 myapp에 할당합니다.

그리고 아래와 같이 이 객체에다가 전역유효범위 에서 사용할 변수와 함수를 프로퍼티로 추가합니다.

```javascript
// 변수 선언
var myapp = myapp || {};


//이하 이름공간

myapp.wonju = {
  name = "Wonju",
  age = 27
};

myapp.hello  = function() {
    console.log("원주ㅎㅇ");
 };

console.log(myapp.wonju.age);
myapp.hello();

//  27, "원주ㅎㅇ" 출력
```

이렇게 해서 myapp만이 사용자가 정의한 전역 변수가 되어 전역유효범위의 오염을 최소화 합니다.

이렇게 객체를 이름 공간으로 사용하면 변수/함수 이름을 계층적으로 관리할 수 있습니다.

하지만 객체를 생성할때마다 앞에 선언을 해야하고 코드량이 늘어나는 단점이 있습니다.

---

## 방법 2. 함수를 이름 공간으로 활용하기

함수 안에서 선언된 변수의 유효 범위는 함수 내부입니다. 때문에 바깥에서는 그 변수를 읽거나 쓸 수 없습니다.

```javascript
var x = "global x";
(function () {
  var x = "local x";
  var y = "local y";
})();
console.log(x); // global x 출력
console.log(y); // Uncaught ReferenceError: y is not defined
```

- 즉시실행함수 내부에서 선언한 변수 x와 y는 이 함수의 지역변수로 전역변수 x와 이름이 충돌하지 않습니다. 이 성질을 이용해 처리하려는 내용물을 즉시 실행 함수 안에 작성하면 유효 공간을 오염시키지 않을 수 있습니다.

```javascript
즉시실행함수 문법:

(function () {
  //do something
})();

```

즉시실행함수는 선언과 동시에 바로 실행되기 때문에 전역변수를 만들지 않아 라이브러리 등을 만들 때 많이 사용됩니다. 라이브러리 안의 전역변수와 충돌하지 않기 때문입니다.

```javascript
console.log(
  typeof function wonju() {
    let name = "Wonju";
    let age = 27;
  }
);

// function 출력
```

```javascript
console.log(
  typeof (function () {
    let name = "Wonju";
    let age = 27;
  })()
);
// undefined 출력
```

이렇게 하면 프로그램 안에 선언한 모든 변수가 즉시 실행 함수의 지역 변수가 되기 때문에 전역 유효 공간을 오염시키지 않습니다. 즉시실행함수는 모듈패턴의 기반이 되기도 합니다.

### 모듈 패턴

모듈이란?

> 기능(함수) 여러개를 하나로 묶은 것으로, 보통 함수 여러개와 함수가 공유하는 데이터로 구성

- 모듈은 전체 어플리케이션의 일부를 독립된 코드로 분리해 놓은 것

모듈 패턴은 어플리케이션이나 라이브러리를 위한 하나의 전역객체를 만들고 모든기능을 객체에서 추가하는것.

많이 사용하는 제이쿼리도 하나의 모듈이라고 볼 수 있습니다.

그렇기 때문에 여러 라이브러리를 함께 받아도 충돌하지 않는 것입니다.

- 모듈을 즉시실행함수 안에 작성, 실행할 수 있습니다.

---

# 객체로서의 함수

## 함수는 객체

JS에서는 함수도 일종의 객체입니다.

함수는 Function 객체이며, 다른 객체와 마찬가지로

- 함수는 변수/프로퍼티/배열 요소에 대입 가능

- 함수는 함수의 인수로 사용이 가능

- 함수는 함수의 반환값으로 사용 가능

- 함수는 프로퍼티와 메서드 가질 수 있음

- 함수는 이름 없는 리터럴로 표현 가능 ( 익명 함수)

- 함수는 동적으로 생성 가능

위와 같은 작업이 가능한 객체를 **일급 객체** 라고 합니다. 자바스크립트에서의 함수는 일급 함수라고 합니다. 그렇기 때문에 스킴(Scheme) 과 같은 함수형 언어처럼 함수형 프로그래밍이 가능합니다.

## 함수의 프로퍼티

| 프로퍼티 이름 |               설명               |
| :-----------: | :------------------------------: |
|    caller     | 현재 실행중인 함수를 호출한 함수 |
|    length     |         함수의 인자 개수         |
|     name      |  함수를 표시할 때 사용하는 이름  |
|   prototype   |      프로토타입 객체의 참조      |

- Function.prototype의 프로퍼티 상속 (apply, bind, call, constructor, toString())은 9장에서 설명합니다.

- apply, bind, call 메서드는 이 절에서 설명합니다.

| 프로퍼티 이름 |                                설명                                |
| :-----------: | :----------------------------------------------------------------: |
|    apply()    |    선택한 this와 인수를 사용해 함수 호출한다. 인수는 배열 객체     |
|    call()     | 선택한 this와 인수를 사용해 함수 호출한다. 인수는 쉼표로 구분한 값 |
|    bind()     |        선택한 this와 인수를 적용한 새로운 함수를 반환한다.         |
|  constructor  |                       Function 생성자의 참조                       |
|  toString()   |            함수의 소스 코드를 문자열로 만들어 반환한다.            |

## apply, call 메서드 그리고 bind 메서드

함수를 호출하는 방법은

1. 함수이름()
2. 함수이름.call/apply/bind(객체, 인수)

- 함수 객체의 메서드 apply와 call은 this 값과 함수의 인수를 사용해 함수를 실행하는 메서드입니다.

  - 기존함수호출과의 차이점은 메소드를 이용해 호출해 실행한다면

  그 함수의 첫번째 인자로 전달하는 객체에 this를 지정할 수 있다는 것.

  - apply의 인수는 배열이고 call의 인수는 쉼표로 구분한 값의 목록 이라는 차이뿐

- bind 메서드는 객체에 함수를 말그대로 바인드(묶다, 속박하다)함

  - call이나 apply 메서드와 달리 함수를 바로 호출하지 않고 반환합니다.

```javascript
function a(x, y, z) {
  console.log(this, x, y, z);
}
var b = { c: "eee" };
// call
a.call(b, 1, 2, 3);

// apply
a.apply(b, [1, 2, 3]);

// bind
var c = a.bind(b);
c(1, 2, 3);

// 결과는 모두
// {c: "eee"} 1 2 3
```

a.call은 this를 b로 받도록 명시하고, 1,2,3을 차례대로 받음

a.apply도 this를 b로 받도록 명시하고, [1,2,3]을 배열형태로 받음

bind는 즉시호출없이 함수생성을 하므로
변수 c에 this를 b로 명시하여 넣고 나중에 1,2,3을 추가

## 함수에 프로퍼티 추가하기

다른 객체와 마찬가지로 함수에도 프로퍼티를 추가할 수 있습니다.

---

# 고차 함수

> 고차 함수란?
>
> > 함수를 인자로 받거나 함수를 리턴하는 함수
> >
> > > 즉 인자로 받은 함수를 필요한 시점에 호출하거나 클로저를 생성해 리턴하는 것

이때 다른 함수의 인자로 전달되는 함수를 **콜백함수**라고 하며, 콜백함수를 전달받는 함수를 고차함수라고 합니다.

콜백함수 외에도 10장의 map, filter, reduce 등의 배열 메서드도 고차함수의 예로 들 수 있습니다.

- 합성 함수

```javascript
함수 f(x)와 g(x)가 있을 때 f(g(x))를 의미

예)
function compose(f, g){
  return function(x) {
    return
  }
}
```

- 부분 적용

```javascript
function product(x, y) {
  return x * y
}
라는 함수가 있을 때,
인수를 부분 적용한 product2(x)의 정의:

product2 = function(y) {
  return product(2, y);

  product2(3) // 6
}

bind 메서드를 사용하면

product2 = product.bind(null, 2);
```

bind 메서드의 2번째 이후 인수가 원래 함수의 인수에 할당되고, 그러면
함수 product의 인수를 부분적용한 함수 prodcut2 가 만들어집니다.

# 콜백 함수

> 함수 안에 인자로 들어가는 함수 - 순차적으로 실행하고 싶을 때 사용

클론코딩하면서 익숙하게 접한 addEventListener! 에도 콜백함수가 있습니다.

```javascript
document.querySelector('.className').addEventListener('click', function(){
    버튼누르면 실행하고 싶은 코드~
})
```

동기적: 정해진 순서에 맞게 코드가 실행
비동기적: 언제 코드가 실행될지 예측할 수 없음(setTimeout과 같이)

자주 접해본 자바스크립트 코드.

addEventListener 라는 함수 인자 자리에 있는 function 이 콜백함수!!

setTimeout 이라는 함수에서도 콜백함수를 발견할 수 있습니다.

```javascript
setTimeout(function () {
    어쩌구저쩌구 실행원하는 코드
}, 1000);

// 1 초 이후에 { } 안의 코드 실행해주세요~
```

- 다른 곳에서 만든 함수도 콜백함수로 넣어줄 수 있습니다.

- 콜백함수로 쓰일 함수 이름도 지어줄 수는 있습니다.

- 콜백함수가 필요한 함수에만 콜백함수를 사용 가능합니다. (아무 함수나 사용X)

예)

```javascript
function first() {
  console.log(1);
}

function second() {
  console.log(2);
}
```

두 함수를 순차적으로 사용하려면 그냥

```javascript
first();
second();
```

이렇게 작성해도 문제는 없습니다.

하지만 번거로울 수도 있고, first() 가 비동기적 상황(순차적실행X)이 있을 수 있기 때문에

```javascript
function first(인자) {
  console.log(1);
  인자();
}
function second() {
  console.log(2);
}

first(second);
// 1
// 2 순서대로 출력
```

위와 같이 first() 인자 자리를 하나 뚫어놓고 그 안에 second 함수를 넣으면 바로 순차적으로 실행됩니다.

유의사항

콜백함수를 계속 쓰게되면, 즉
A 불러오고 B 불러오고 C 불러오고...

함수가 너무 길어집니다.

이걸 해결한다면 promise, async와 같은 방법으로 해결할 수 있습니다.

---

# ECMAScript 6부터 추가된 함수

## 화살표 함수 표현식으로 함수 정의하기

기존의 함수 표현식

```javascript
var square = function (x) {
  return x * x;
};
```

화살표 함수로 표현하기

```javascript
var square = (x) => {
  return x * x;
};
```

인수가 여러개일 경우 인수와 인수를 쉼표로 구분하기

```javascript
var f = (x, y, z) => { ... };
```

인수가 한개일 경우 인수 묶어주는 괄호를 생략 가능

```javascript
var square = (x) => {
  return x * x;
};
```

인수가 없으면 인수 묶어주는 괄호 생략 불가능

```javascript
var f = () => { ... };
```

함수 몸통 안의 문장이 return 만 있으면 중괄호와 return 키워드 생략 가능

```javascript
var square = (x) => x * x;
```

몸통 안의 문장이 return만 있어도 반환값이 객체 리터럴이면 그룹 연산자인 ()로 묶어주기

```javascript
var f = (a, b) => ({ x: a, y: b });
```

화살표 함수도 즉시실행함수(IIFE)로 사용 가능

```javascript
((x) => x * x)(3); //9 출력
```

## 화살표 함수와 함수 표현식의 차이

1. this 값이 함수를 정의할 때 결정된다.

함수 표현식의 this 값은 함수를 호출할 때 결정됩니다. 그러나 화살표함수의 this값은 함수를 정의할 때 결정됩니다. 즉 화살표 함수 바깥의 this값이 화살표 함수의 this값이 됩니다.

2. arguments 변수가 없다.

화살표 함수 안에는 arguments 변수가 정의되어있지 않아 사용 불가능합니다.

```javascript
var f = () = > console.log(arguments);
f(); // ReferenceError: arguments is not defined
```

3. 생성자로 사용할 수 없다.

화살표 함수 앞에 new 연산자 붙여서 호출이 불가능합니다.

```javascript
var Person = (name, age) => {
  this.name = name;
  this.age = age;
};
var tom = new Person("Tom", 17);
// TypeError: Person is not a constructor
```

4. yield 키워드를 사용할 수 없다.

따라서 제너레이터로 사용할 수 없습니다(324쪽 '제너레이터' 참고)

## 인수에 추가된 기능

### 1. 나머지 매개변수

- ECMAScript 6 부터는 함수의 인자 부분에 ... 을 입력하면 그만큼의 인수를 배열로 받을 수 있습니다. 이렇게 ... 로 표현한 인자를 '나머지 매개변수' 라고 부릅니다.

```javascript
function f(a, b, ...args) {
  console.log(a, b, args);
}
f(1, 2, 3, 4, 5, 6); // 1 2 [3, 4, 5, 6] 출력
```

ECMAScript 5 까지는 가변인수 이용하기 위해선 arguments 변수를 사용해야 했지만 arguments는 유사배열객체이기 때문에 forEach 등의 배열 메서드로 조작하기 위해서는 배열로 변환해야하는 번거로움이 있었습니다.

나머지 매개변수는 인수를 배열로 받기 때문에 번거로움이 줄어듭니다.

화살표 함수 안에서 arguments를 사용할 수 없지만 나머지 매개변수는 사용 가능합니다.

```javascript
var sum = (...args) => {
  for (var i = 0, s = 0; i < args.length; i++) s += args[i];
  return s;
};

sum(1, 2, 3, 4, 5); // 15 출력
```

### 2. 인수의 기본값

ECMAScript 6 부터는 함수 인자에 대입연산자(=) 를 사용해서 기본값 설정이 가능합니다. 기본값 설정한 인자에 호응하는 인수를 생략하거나 undefined를 넘기면 대입연산자 우변값이 기본값이 됩니다.

```javascript
function abcd(a, b = 1) {
  return a * b;
}
abcd(3); // 3 출력
abcd(3, 2); // 6 출력
```

다른 인자의 값도 기본값으로 사용 가능합니다.

```javascript
function add(a, b = a + 1) {
  return a + b;
}
add(2); // 5 출력
add(2, 1); // 3 출력
```

### 3. 이터레이터와 for/of 문

- <h3>이터러블</h3>: 이터레이터를 리턴하는 Symbol.iterator 를 가진 객체이며, for...of 문에서 순회할 수 있습니다.

```javascript
const array = [1, 2, 3];

// 배열은 Symbol.iterator 메소드를 소유하기 때문에 이터러블이다.
console.log(Symbol.iterator in array); // true

// 이터러블 프로토콜을 준수한 배열은 for...of 문에서 순회 가능하다.
for (const item of array) {
  console.log(item);
}
// 1, 2, 3 각각 출력
```

```javascript
const obj = { a: 1, b: 2 };

// 일반 객체는 Symbol.iterator 메소드를 소유하지 않기 때문에 이터러블 아니다.
console.log(Symbol.iterator in obj); // false

for (const p of obj) {
  console.log(p);
}
// TypeError: obj is not iterable
```

> 일반 객체도 이터러블 프로토콜(데이터순회 위한 규약) 준수하면 이터러블 가능!

- <h3>이터레이터</h3>: next 메서드를 소유하며, next 메서드를 호출하면 이터러블을 순회하며 value와 done 프로퍼티를 갖는 이터레이터 리절트를 리턴하는 객체

```javascript
const array = [5, 4, 3];
const iter = array[Symbol.iterator]();
// Symbol.iterator 메서드는 이터레이터를 리턴하며,

console.log("next" in iter);
// 이터레이터는 next 메서드를 갖는다.

const iterResult = iter.next();
console.log(iterResult);
// {value: 5, done: false} 출력 하는 것에서 알 수 있듯
// 이터레이터의 next메서드를 호출하면 value, done 프로퍼티를 갖는 이터레이터 리절트 객체를 리턴한다.

console.log(iter.next()); // Object { value : 5, done : false}
console.log(iter.next()); // Object { value : 4, done : false}
console.log(iter.next()); // Object { value : 3, done : false}
console.log(iter.next()); // Object { value : undefined, done: true}
console.log(iter.next()); // Object { value : undefined, done: true}

// next메서드 호출할 때마다 이터러블을 순회하며 이터레이터리절트 객체를 리턴한다.
// value 프로퍼티는 순회중인 이터러블 값을,
// done 프로퍼티는 이터러블 순회 완료 여부를 리턴한다.
```

<h3>for...of 문</h3>
: 내부적으로 이터레이터의 next 메서드를 호출해 이터러블을 순회하며 이터레이터 리절트 객체의 value값을 for...of 문의 변수로 할당합니다. 그리고 이터레이터 리절트 객체의 done 값이 true면 순회를 중단합니다.

또한 아래와 같은 생성자로 생성한 내장 객체는 Symbol.iterator 메서드를 내장하고 있습니다. 즉 이터러블 입니다.

- Array, String, TypedArray, Map, Set

```javascript
// 배열
for (const item of ["a", "b", "c"]) {
  console.log(item);
  // 각각 1, 2, 3 출력
}

// 문자열
for (const letter of "abc") {
  console.log(letter);
}
// 각각 a, b, c 출력
```

- for...of 문의 내부동작을 for 문으로 표현했을 때

```javascript
// 이터러블
const iterable = [1, 2, 3];

// 이터레이터
const iterator = iterable[Symbol.iterator]();

for (;;) {
  // 이터레이터의 next 메소드를 호출하여 이터러블을 순회
  const res = iterator.next();

  // next 메소드가 반환하는 이터레이터 리절트 객체의 done 프로퍼티가 true가 될 때까지 반복
  if (res.done) break;

  console.log(res);
}
```

문자열의 예시:

```javascript
for (var v of "ABC") console.log(v);
// "A", "B", "C" 를 순서대로 출력
```

반복가능객체(이터러블)은 for/of문, 전개연산자, yield, 비구조화 할당 등에 활용할 수 있습니다.

---

## 제너레이터

- 제너레이터 함수는 이터러블을 생성하는 함수입니다. 제너레이터는 이터레이터를 유연하게 사용할 수 있으며 제너레이터는 코드를 일시정지 했다가 필요할 때 재시작 할 수 있습니다.

- 일반 함수를 호출하면 return 문으로 반환값을 리턴하지만
  제너레이터 함수를 호출하면 제너레이터를 반환합니다.

- 제너레이터는 이터러블(iterable)이면서 동시에 이터레이터(iterator)인 객체입니다. 다시 말해 제너레이터 함수가 생성한 제너레이터는 Symbol.iterator 메소드를 소유한 이터러블입니다.

- 제너레이터는 next 메소드를 소유하며 next 메소드를 호출하면 value, done 프로퍼티를 갖는 이터레이터 리절트 객체를 반환하는 이터레이터입니다.

- 제너레이터는 function\* 로 정의하며, 하나 이상의 yield 문을 포함합니다.

```javascript
 제너레이터 함수 선언문


function* gen() {
  yield 1;
}

let genObj = gen();
```

제너레이터 함수를 호출하면 바로 실행되지 않고 제너레이터 객체를 리턴합니다.

앞에서 말했듯 제너레이터는 이터레이터이자 이터러블입니다.

```javascript
function* gen() {
  yield 1; // 포인트 1
  yield 2; // 포인트 2
  yield 3; // 포인트 3
}
var iter = gen();
console.log(iter.next()); // Object { value: 1, done: false }
console.log(iter.next()); // Object { value: 1, done: false }
console.log(iter.next()); // Object { value: 1, done: false }
console.log(iter.next()); // Object { value: undefined, done: true }
```

### 템플릿 리터럴의 태그 함수

템플릿 리터럴 앞에 함수 이름을 적으면 템플릿 리터럴의 내용을 인수로 받는 함수를 호출할 수 있습니다.

```javascript
func`${a} + ${b} = ${a + b}`;
```

위 코드에서 func` 부분을 **태그 함수** 라고 합니다.

https://poiemaweb.com/es6-iteration-for-of
https://poiemaweb.com/es6-generator
