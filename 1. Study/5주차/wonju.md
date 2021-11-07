# 8️⃣ 함수

## ✔ 함수 정의하기

### 1. 함수 정의하는 법

1. 함수 선언문

```javascript
function square(x) {
  return x * x;
}
```

2. 함수 표현문(함수 리터럴)

```javascript
var square = function (x) {
  return x * x;
};
```

3. Function 생성자

```javascript
var square = new Function("x", "return x*x");
```

4. 화살표 함수

```javascript
var square = (x) => x * x;
```

> 함수 선언문으로 정의한 함수는 변수선언문과 마찬가지로 호이스팅(끌어올림)이 가능합니다.
>
> > 그 외는 모두 변수를 할당한 후에 호출할 수 있습니다.

<br>

### 2. 중첩 함수(Nested Function)

자바스크립트에서는 함수 안쪽에 또 다른 함수를 선언하는 함수를 사용할 수 있습니다.

```javascript
function foo() {
  function bar() {
    console.log("Hello");
  }

  bar(); // 정상작동
}

bar(); // 에러발생!, bar is not defined
```

- 위의 예시를 통해 중첩함수의 참조는 그것을 둘러싼 외부 함수의 지역 변수에 저장되므로 중첩함수는 선언된 함수 내부가 아니면 호출하는 것이 불가능하다는 것을 알 수 있습니다.

> bar함수는 foo함수 내부에서만 사용될 것임을 명시적으로 나타낸다. 이는 코드를 읽어나가는데 도움이 될 수 있습니다.

- 내부함수는 자신을 둘러싼 외부함수의 인수와 지역변수에 접근할 수 있습니다.

```javascript
function outer() {
  var title = "hello";
  function inner() {
    console.log(title);
  }
  inner();
}
outer();
```

---

## ✔ 함수 호출하기

### 1. 함수 호출하기

1. 함수 호출: 함수 참조가 저장된 변수 뒤에 그룹연산자( )를 붙여서 호출

```javascript
var s = square(5);
```

2. 메서드 호출: 함수 호출과 같은 방법으로 호출

```javascript
obj.m = function(){...};
obj.m();
```

3. 생성자 호출: 함수 또는 매서드를 호출할 때 함수참조 저장한 변수 앞에 new 키워드를 추가하면 함수가 생성자로 작동.

```javascript
var obj = new Objcet();
```

4. call, apply를 사용한 간접 호출: call과 메서드를 사용해 간접호출 가능

<br>

### 2. 즉시 실행 함수

보통 익명 함수를 실행할 때는 변수에 함수의 참조를 할당한 후 ()를 붙여서 실행합니다.

```javascript
var f = function(){...};
f();
```

자바스크립트에는 익명 함수를 정의한 후 곧바로 실행할 수 있는 '즉시 실행 함수'가 있습니다.

```javascript
(function(){...})();
```

함수 정의식을 그룹연산자인 () 로 감싸줍니다. 그러면 함수정의식이 평가되고 함수 값으로 바뀝니다.

다음과 같은 방법도 사용 가능합니다.

```javascript
+function(){...}()
```

또한 즉시 실행 함수에도 인수를 넘길 수 있습니다.

```javascript
(function(a,b) {...}(1,2));
```

앞의 코드는 인수 a와 b에 각각 1과 2를 대입합니다.

즉시실행함수에도 이름을 붙일 수 있습니다. 다만 함수 내부에서만 유효합니다.

```javascript
(function fact(n) {
    if( n=<1) return 1;
    return n*fact(n-1);
})(5);      //  120 출력
```

함수의 실행결과를 변수에 할당할 수 있으며 표현식 안에서 사용가능합니다.

```javascript
var x = (function(){...})();
```

즉시 실행함수는 전역유효범위를 오염시키지않는 이름공간을 생성할때 사용됩니다(8.7절)

---

## ✔ 함수의 인수

### 1. 인수의 생략

자바스크립트에서는 함수를 호출할 때 인수를 생략할 수 있습니다.

함수 정의식에 작성된 인자의 개수보다 적은 인자를 전달해 함수를 실행하면 생략된 인자는 undefined가 됩니다.

```javascript
function f(x, y) {
  console.log("x=" + x + ", y= " + y);
}
f(2); // x = 2, y = undefined
```

이러한 성질을 활용해 인수를 생략할 수 있는 함수를 정의할 수 있습니다.
이를 위해서는 인수를 생략했을 때 사용할 초깃값을 설정합니다.

```javascript
function multiply(a, b) {
  b = b || 1; // b의 초깃값을 1로 설정
  return a * b;
}
multiply(2, 3); // 6 출력
multiply(2); // 2 출력
```

인자 b에 값이 들어오면 논리연산자(||)에 따라 true로 평가되어 값을 사용하고, b에 값이 들어오지 않으면 b값이 undefined이므로 false로 평가되어 b값이 1이 됩니다.

---

### 2. 가변 길이 인수 목록(arguments 객체)

가변인자함수 : 매개변수의 최대 갯수가 정해지지 않은 함수

```javascript
sum(10, 20, 30, ...);
```

가변인자함수를 이용해 인자의 갯수 제한이 없는 함수를 만들 수 있습니다.

- arguments 객체를 사용해 가변인자함수를 만들 수 있습니다.

- 자바스크립트 함수는 arguments 객체를 가지고 있습니다.

```javascript
function sum() {
console.log('length: ', arguments.length);
console.log('index 1: ', arguments[1]);
}
sum(10, 20);

// length:  2 출력
// index 1:  20 출력

출처: https://jungpaeng.tistory.com/80 [개발자스러운 블로그]
```

- Arguments 객체는 '유사 배열 객체'로, 10.3절을 참고합니다.

- Arguments 객체는 length와 callee 프로퍼티를 갖고 있습니다.

argument.length: 인수 개수

argument.callee: 현재 실행중인 함수의 참조

> ES5 strict 모드에서 arguments.callee()의 사용이 금지되었습니다.
> https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments/callee
>
> > JS 초기에는 함수표현식이 불가능해 재귀함수표현이 불가능해 도입되었지만 문제가 많이 발생.

---

## ✔ 재귀 함수

> 함수가 자기 자신을 호출하는 행위를 **재귀 호출** 이라고 하며, 이러한 호출을 수행하는 함수를 **재귀 함수** 라고 합니다.

### 1. 재귀 함수의 기본

재귀함수를 정의할때는 두가지를 유의해야 합니다.

```javascript
function factorial(x) {
  if (x < 0) return;
  if (x === 0) return 1;
  return x * factorial(x - 1);
}

factorial(3);
// 6
```

1. 반드시 멈춰야 한다.

함수가 자신을 호출하면 무한한 호출로 이어지기 때문에 중간에 멈출 수 있도록 만들어야 합니다.

위의 예제코드에서는 factorial(x)에서 factorial(x-1)을 호출합니다. 그때마다 인수 x값을 1씩 줄여나갑니다. 하지만 그다음 문장에서 x값이 0일 때 재귀호출을 멈춥니다.

```javascript
function factorial(x) {
  // 종료 조건
  if (x < 0) return;

  // 기반 조건
  if (x === 0) return 1;

  // 재귀
  return x * factorial(x - 1);
}

factorial(3);
// 6
```

재귀는 중첩된 함수 호출입니다. 모든 중첩된 함수에서 가장 내부에 중첩된 함수가 가장 먼저 반환됩니다.

```javascript
factorial(0) 는 1

factorial(1) 는 1 * factorial(0), 또는 1*1

factorial(2) 는 2 * factorial(1), 또는 2*1*1

factorial(3) 는 3 factorial(2), 또는 3*2*1*1

return 1 * 1 * 2 * 3
// 6
```

2. 재귀 호출로 문제를 간단히 해결할 수 있을때만 사용한다.

재귀함수는 멈출때까지 호출을 계속합니다. 각각의 호출된 재귀 함수는 메모리의 다른 영역을 사용하기 때문에 while문이나 for 문으로 대체하는 것이 이해도 쉽고 메모리 공간도 적게 차지합니다.

---

## ✔ 프로그램의 평가와 실행과정

<br>

### 실행 가능한 코드

자바스크립트 엔진은 실행 가능한 코드(전역코드, 함수코드, eval코드)를 만나면 코드를 평가하고 실행 문맥으로 만들어줍니다.

- 전역 코드: Window 아래에 정의된 함수

- 함수 코드: 문자 그대로 함수

- eval 코드: eval 함수(별도의 동적환경에서 작동하기에 설명 제외)

<br>

### 실행 문맥의 구성

```java
// 1. 실행 문맥의 구조
Execution Context = {

  // 1-1. 렉시컬 환경 컴포넌트
  Lexical Environment Component : {


    // A. 환경 레코드
    Environment Record : {
      // ㄱ. 선언적 환경 레코드
      Declarative Environment Record
      // ㄴ. 객체 환경 레코드
      Object Environment Record
    },

    // B. 외부 렉시컬 환경 참조
    Outer Lexical Environment Reference
  },


 // 1-2. 변수 환경 컴포넌트
 Variable Environment Component


 // 1-3. 디스 바인딩 컴포넌트
 This Binding Component
}
```

실행문맥은 실행가능한 코드가 실행되고 관리되는 영역으로, 컴포넌트 여러개가 정보를 나누어 관리합니다.

- 렉시컬 환경 컴포넌트 & 변수 환경 컴포넌트

  - 렉시컬환경 타입의 컴포넌트로, with문을 사용할 때를 제외하고 내부 값이 동일합니다.

- 디스 바인딩 컴포넌트

  - 함수를 호출한 객체의 참조가 저장되는 곳으로, 이것이 가리키는 값이 해당 실행 문맥의 this가 됩니다. 8.5.9절에서 설명합니다.

<br>

### 렉시컬 환경 컴포넌트의 구성

환경 레코드와 외부 렉시컬 환경 참조 컴포넌트로 구성되어 있습니다.

- 환경 레코드: 유효 범위 안의 식별자와 결과값이 묶여 기록되는 곳

- 외부 렉시컬 환경 컴포넌트: 중첩된 함수의 바깥 코드에 정의된 변수를 읽거나 쓰기 위해 저장되는 곳

### 전역 환경과 전역 객체

웹브라우저에 내장된 자바스크립트는 새로운 웹페이지를 읽어들인 후

렉시컬환경타입의 전역환경을 생성합니다. 그리고 전역객체를 생성한 후 전역환경의 환경레코드에 전역객체의 참조를 대입합니다.

### 프로그램 실행과 실행 문맥

실행문맥은 스택 이라는 구조로 관리됩니다.

![image](https://user-images.githubusercontent.com/75517083/140637442-c757362f-1409-4f8a-9a1b-4cbeeca921ff.png)

1. 실행문맥은 스택에 push되어 실행되고 그러기 위해 항상 맨아래에 위치
2. 전역코드가 실행
3. 전역코드 안의 함수가 실행되면 그러기 위한 실행문맥을 push
4. 함수작업이 끝나고나면(return) 스택에서 pop

- 중첩함수일 경우 내부함수가 새로운 실행문맥을 만들어서 스택에 push
- 재귀함수 역시 호출함수와 같음에도 전혀 다른 함수로서 스택에 push

> 자바스크립트는 싱글 스레드 방식입니다.
>
> > 호출 스택에 쌓인 실행문맥(함수 또는 코드)을 위에서부터 차례차례 실행

#### 실행순서

1. 실행 문맥 생성&호출스택에 push -> 렉시컬환경컴포넌트 생성

2. 렉시컬환경컴포넌트에서 환경레코드 생성->함수 안팎의 환경을 기록:

- 함수의 인자, 중첩함수의 참조, var로 선언한 지역변수, arguments

3. 실행문맥에 있는 디스 바인딩 컴포넌트에 그 함수를 호출한 객체의 참조를 저장하고 이것으로 this를 결정. this는 호출상황에 따라 가리키는 객체가 변화

4. 함수 안의 코드가 순서대로 실행

5. 함수가 종료되면 실행문맥과 함께 그 안의 렉시컬환경컴포넌트는 사라짐

6. but 함수의 참조가 환경 레코드에 유지되는 경우 렉시컬환경컴포넌트가 유지 => 클로저에서 확인

## ✔ 클로저

외부함수가 소멸된 이후에도 내부함수가 외부함수에 접근할 수 있습니다.

```javascript
function outer() {
  var title = "hello";
  return function () {
    console.log(title);
  };
}
inner = outer();
inner();
```

> 클로저란?
>
> > 함수와 그 함수가 선언됐을 때의 렉시컬 환경(Lexical environment)과의 조합이다.

```javascript
function outerFunc() {
  var x = 10;
  var innerFunc = function () {
    console.log(x);
  };
  innerFunc();
}

outerFunc(); // 10
```

- 함수 outerFunc 내에서 내부함수 innerFunc가 선언, 호출되었습니다.
  이때 innerFunc는 자신을 포함하고 있는 외부함수 outerFunc의 변수 x에 접근할 수 있습니다. innerFunc가 outerFunc의 내부에서 선언되었기 때문입니다.

> 스코프는 함수를 호출할 때가 아니라 함수를 어디에 선언하였는지에 따라 결정됩니다. 이를 렉시컬 스코핑(Lexical scoping)라 합니다.

> 위 예제의 함수 innerFunc는 함수 outerFunc의 내부에서 선언되었기 때문에 함수 innerFunc의 상위 스코프는 함수 outerFunc입니다.

---

1. innerFunc 함수 스코프(함수 자신의 스코프를 가리키는 활성 객체) 내에서 변수 x를 검색한다. 검색이 실패하였다.

2. innerFunc 함수를 포함하는 외부 함수 outerFunc의 스코프(함수 outerFunc의 스코프를 가리키는 함수 outerFunc의 활성 객체)에서 변수 x를 검색한다. 검색이 성공하였다.

---

```javascript
function outerFunc() {
  var x = 10;
  var innerFunc = function () {
    console.log(x);
  };
  return innerFunc;
}

//함수 outerFunc를 호출하면 내부 함수 innerFunc가 반환된다.
//그리고 함수 outerFunc의 실행 컨텍스트는 소멸한다.

var inner = outerFunc();
inner(); // 10
```

1. 함수 outerFunc는 innerFunc를 반환하고 종료되었다. 마감. 그렇기에 outerFunc의 변수 x도 유효하지 않을 것. 그런데 출력결과는 x의 값인 10.

이처럼 자신을 포함한 외부함수보다 내부함수가 더 오래 유지되는 경우, 외부 함수 밖에서 내부함수가 호출되더라도 외부함수의 지역변수에 접근할 수 있는 경우를 클로저 라고 합니다.

<br>

다시 위에서 말한 정의를 보면,

> 함수와 그 함수가 선언됐을 때의 렉시컬 환경(Lexical environment)과의 조합이다.

여기서 말하는 함수란 내부함수를 의미하며, "그 함수가 선언됐을 때의 렉시컬 환경" 이란 내부 함수가 선언됐을 때의 스코프를 의미합니다.

즉,

> ### 클로저는 반환된 내부함수가 자신이 선언됐을 때의 환경(Lexical environment)인 스코프를 기억하여 자신이 선언됐을 때의 환경(스코프) 밖에서 호출되어도 그 환경(스코프)에 접근할 수 있는 함수를 말합니다. 이를 조금 더 간단히 말하면 클로저는 자신이 생성될 때의 환경(Lexical environment)을 기억하는 함수라고 할 수 있습니다.
