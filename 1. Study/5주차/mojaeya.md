# 함수

## 함수 정의
- 호이스팅으로 호출 가능
1. 함수 선언문
```javascript
function square(x) { return x*x; }
```
---

- 함수의 참조를 변수에 할당해야 호출 가능 
2. 함수 리터럴
```javascript
var square = function(x) {return x*x; };
``` 
3. Function 생성자
```javascript
var square = new Function("x","return x*x");
  ```
4. 화살표 함수 표현식 (ES6부터 추가)
```javascript
var square = x => x*x; 
```

## 중첩 함수
- 특정 함수의 내부에 선언된 함수를 가리켜 그 함수의 중첩 함수라고 한다.   
(C나 Java에서는 중첩 함수를 사용할 수 없지만 자바스크립트에서는 가능)
- 자바스크립트에서는 외부 함수의 최상위 레벨에만 중첩 함수 작성 가능 
- 함수 안의 if문과 while 문 등의 문장 블록 안에는 중첩 함수 작성 X

```javascript
//배열 요소의 제곱합에 대한 제곱근을 구하는 함수
function norm(x) {
    var sum2 = sumSquare();
    return Math.sqrt(sum2); // Math.sqrt(x) => x의 제곱근
    function sumSquare() { // 중첩 함수
        var sum = 0;
        for(var i = 0; i<x.length; i++) {
            sum += x[i]*x[i];
        }
        return sum;
    }
}

var a = [2, 1, 3, 5, 7];
var n = norm(a);
console.log(n); // -> 9.38083151964686
```
- 중첩함수의 참조는 그 중첩 함수를 둘러싼 외부 함수의 지역 변수에 저장되므로 외부 함수의 바깥에서는 호출 불가능

✓ 자신을 둘러싼 외부 함수의 인수와 지역 변수에 접근 가능하다.
그래서 위의 코드를 보면 중첩 함수 sumSquare가 변수 x가 사용된 것을 알 수 있다.

📌 외부 함수의 변수 유효 범위가 그 함수의 중첩 함수까지 미친다는 규칙을 기억해두자. 뒤에서 배울 클로저의 핵심적인 구성요소가 된다!!!

## 즉시 실행 함수
```javascript
var f = function(){...};
f();
```

## 함수의 인수 생략
자바스크립트는 유연한 언어다.
함수를 호출할 때 인수를 생략해도 에러가 나지 않는다.
```javascript
function f(x, y) {
  console.log("x = " + x + ", y = " + y);
}
f(2); // x = 2, y = undefined
```
함수의 인자보다 적게 호출 => 생략된 인수에 undefined
함수의 인자보다 많게 호출 => 초과된 인수는 무시

## 자바스크립트에서 함수를 호출할 때 arguments 객체가 함수 내부로 전달된다.

arguments 객체 ❓
- 함수를 호출할 때 넘긴 인수들이 배열 형태로 저장된 객체를 뜻한다. 

그럼 arguments는 배열 타입 ❓ 
NO!!! 실제 배열이 아니고 배열의 형태를 띠는 '유사 배열 객체'이다!!!

🔎 유사배열에 대해 간단히 보고 오자

그러므로 arguments 객체는 
1. 매개변수 개수가 정확하게 정해지지 않은 함수를 구현하거나 (가변 인자 함수)
2. 전달된 인자의 개수에 따라 서로 다른 처리를 해줘야하는 함수를 개발하는데 유용

### 가변 인자 함수
- 매개 변수의 개수가 변할 수 있는 함수
앞에서 살펴본것처럼, 자바스크립트는 원래 인수를 생략해도 오류가 안뜨고 작동을 하기에 그냥 사용해도 괜찮지만,
여기서 말하고자 하는 가변인자 함수는 매개 변수를 선언된 형태와 다르게 사용했을 때도 매개변수를 모두 활용하는 함수이다.

# 재귀 함수 

- 재귀 호출을 수행하는 함수
재귀 호출: 함수가 자기 자신을 호출하는 행위


- 유의 사항
1. 재귀 호출은 반드시 멈춰야 한다
함수가 자신을 호출하면 무한한 연쇄 호출로 이어지므로 프로그램이 멈추지 않을 가능성이 있기 때문

2. 재귀 호출로 문제를 간단하게 해결할 수 있을 때만 사용한다 호출된 각각의 재귀 함수는 메모리의 다른 영역 사용      
-> 호출된 횟수만큼 메모리 소비량 늘어남

대부분 while문이나 for문으로 작성하는 게 이해하기 쉽고 공간도 적게 차지함

```javascript
//n의 팩토리얼을 구하는 함수
function fact(n) {
    if(n <= 1) return 1;
    return n*fact(n-1);
}

fact(5); // -> 120
```
```javascript
// arguments.callee를 사용하면 이름 없는 익명 함수도 재귀 호출 가능
var fact = function f(n) {
    if(n <= 1) return 1;
    return n*arguments.callee(n-1);
}
```
