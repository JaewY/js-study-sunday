## 함수 정의하기
  
  #### 함수 정의 방법
  * 함수 선언문
      ```javascript
      function square(x) { return x*x; }
      ```
  * 함수 리터럴
     ```javascript
     var square = function(x) {return x*x; };
      ``` 
 * Function 생성자
   ```javascript
   var square = new Function("x","return x*X");
      ```
  * 화살표 함수 표현식 
     ```javascript
     var square =x => x*x; 
     ```
  #### 중첩 함수
    중첩 함수란? 특정 함수의 내부에 선언된 함수
    (== 지역 함수, 내부 함수 but 중첩 함수가 올바른 표현)
   * C나 Java 등에서는 사용 불가! Javascript에서 사용 가능
   * 함수 안의 if 문과 while 문 등의 문장 블록 안에는 중첩 함수 작성할 수 없다. 
   * 중요 성질 : 자신을 둘러싼 외부 함수의 인수와 지역 변수에 접근할 수 있다. 
예를 드렁,

 ```javascript
    function norm(x) {
      var sum2 = sumSquare();
      return Math.sqrt(sum2);
      function sumSquare() {
          sum = 0;
          for(var i=0; i<x.length; i++) sum += x[i]*x[i];
          return sum;
        }
 ```
 중첩함수인 sumSquare는 변수 x를 사용하지만 변수 x는 외부 함수인 norm의 인수!!
## 함수 호출하기
#### 함수 호출 방법
 * 함수 호출
  ```javascript
  var s = square(5);
  ```
 * 메서드 호출
  ```javascript
  obj.m = function() { ...};
  obj.m();
  ```
 * 생성자 호출
  ```javascript
  var obj = new Object();
  ```
 * call, apply를 사용한 간접 호출

 #### 즉시 실행 함수
    즉시 실행 함수란? 말그대로 함수를 정의하고 곧바로 실행하는 함수
  ```javascript
  var f = function() { ... };
  f();
  ```
  이 함수를 아래와 같이 수정하면 **정의하는 동시에 실행할 수 있음**
  ```javascript
  (function() { ... })();
  (function() { ... }());
  ```

## 함수의 인수
  #### 인수의 생략
    함수 정의식에서 작성된 인자 개수보다 인수를 적게 전달해서 함수를 실행하면 인수에서 생략된 인자는 undefined
 ```javascript
  function f(x,y) {
   console.log("x = " + x + ", y = " + y);
  }
  f(2);    // x = 2, y = undefined  
 ```
  
  #### 가변 길이 인수 목록(Arguments 객체)

## 재귀 함수
  * 재귀 호출 : 함수가 자기 자신을 호출하는 행위
  * 재귀 함수 : 이러한 재귀 호출을 수행하는 함수
     → 재귀 함수를 사용하면 특정 부류의 문제를 간단히 해결할 수 있음
  * 유의 사항
    - **재귀 호출은 반드시 멈춰야 한다**
    
         : 함수가 자신을 호출하면 무한한 연쇄 호출로 이어짐 따라서 조건을 붙이는 등 함수를 멈춰!
    - **재귀 호출로 문제를 간단하게 해결할 수 있을 때만 사용한다**
    
         : 호출된 각각의 재귀 함수는 메모리의 다른 영역 사용
         
         : 호출된 횟수만큼 메모리 소비량 증가 → 좋지 않아! 프로그램 무거워 느려져
         
예를 들어, 하노이의 탑(A에 있는 원반 n개를 막대기 B를 경유하여 막대기 C로 이동시키는 방법) 
   ```javascript
   function hanoi(n, a, b, c) {
    if( n<1 ) { retrun; }
    hanoi(n-1, a, c, b);
    console.log(n + " 번째 원반: " + a + " → " + c);
    hanoi(n-1, b, a, c);
  }
  hamoi(4, "A", "B", "C");
   ```

## 프로그램의 평가와 실행 과정 🆘🥕
    * 스택 : 바구니! 실행컨텍스트를 담는 바구니
    * 실행컨텍스트 스택 : 스택은 스택인데 자바스크립트에서 쓰는 스택
    * 스코프 : 실행컨텍스트는 스코프 단위로 이루어져 있음
    * 렉시컬 : 보이는 순서대로 읽음
    * push : 평가하고 실행할 때 스택에 넣어
    * pop : 끝나면 스택에서 빼!! 없어져(근데 여기에 얘 있었다고 mark정도는 해줌)
    * last in first out : 스택에 제일 나중에 들어온 실행컨텍스트가 제일 먼저 나간다. 왜냐하면 먼저 할 일을 끝냈거든. 자기할일 다 하면 그냥 나감
    
   https://www.youtube.com/watch?v=pfQfEwnJHRs&t=932s
   
## 클로저 🆘🥕
