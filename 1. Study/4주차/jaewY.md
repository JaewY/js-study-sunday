## 제어 구문
- 자바스크립트는 순차적 실행(위에서부터 아래 방향으로 작성한 순서)함
- 이러한 순차적 실행 흐름을 변화시키는 문장을 제어 구문이라고 함
- 제어 구문 종류 : 조건문(if/else문, switch문, try/catch/finally문)/ 반복문(while문, do/while문, for문, for/in문, for/of문)/ 점프문(break문, continue문, return문, throw문)

### 조건문
1. if/else문 📑
    - if 다음에 오는 조건식이 true로 평가되면 문장을 실행
    - 중첩된 if문일 때 else 절은 가장 가까운 if에 호응
    - 실행할 문장이 단 하나더라도 문장을 {중괄호}로 묶어서 블록 문장으로 만들기를 권장 
```javascript
if( num == 1 ) {
    console.log("One");
  } else if( num == 2) {
    console.log("Two");
  } else {
     console.log("Other");
  }
```

3. switch문 📑
   - switch문을 사용하면 분기점 여러 개를 더욱 간결하게 표현 가능/ 즉, case가 여러 개 일 때 사용하면 좋음
   - break문이 실행되면 블록 문장에서 빠져나와 다음 작업을 시작
   - 함수 끝에 switch문을 사용하면 break문 대신 return 문을 사용해도 똑같은 다중 분기 표현 가능 
   - 다만, default가 switch블록 중간에 있으면 프로그램을 이해하기 어려워지므로 피하는 편이 좋음
```javascript
switch(n) {
     case 1:
         console.log("One");
         break;
     case 2:
         console.log("Two");
         break;
     case 3:
         console.log("Three");
         break;
     default:
         console.log("Other");
  }
```
      
### 반복문
  - 일정한  처리를 한 다음 원래 위치로 돌아가 똑같은 처리를 반복하는 처리(like 도돌이표)
1. while문 📑
   - 조건식 평가 
       → 결과가 false면 while 문을 빠져나와 다음 처리로 이동

       → 결과가 true면 문장 실행 
                 
       → 다시 한번 while문의 시작 부분으로 돌아가서 조건식 평가
                 
   - while 문 안에서는 break 문과 continue 문 사용 가능
     
      → while 문 안에서 break를 실행하면 while 문에서 빠져나옵니다.
     
      → while 문 안에서 continue를 실행하면 while 문의 시작 부분으로 되돌아갑니다.
    
```javascript
functionn fact(n) {
  var k = 1, i = 1;
  while( i < n ) {
     k *= (++i);
  }
  return k;
}
fact(5);   // → 120
```
2. do/while문 📑
    - while문과의 차이는 반복 실행 여부를 어느 부분에서 판단하느냐~
    - while 문은 반복 실행 여부를 시작 부분에서 판단 
    - do/while 문은 반복 실행 여부를 마지막 부분에서 판단
    - do/while 문 끝에 반드시 세미콜론 붙이기;
    - while 문 안에 있는 문장은 한 번도 실행되지 않을 수 있지만 do/while 문 안에 있는 문장은 반드시 한 번 이상 실행됨
```javascript
functionn fact(n) {
  var k = 1, i = n;
  do {
     k *= i --;
   } while( i>0 );
    return k;
 }
 fact(5); // → 120
```

3. for문 📑
   - 반복문은 세 가지 공통점이 있는데, 그 모든걸 한곳에 모아서 표기하는 for 문
     1) 반복 조건의 초기화 작업 
     2) 반복문의 조건식 
     3) 반복 작업이 하나 끝났을 때 반복 조건을 갱신하는 작업
   - for( 초기화 식; 조건식; 반복식) 문장
   - 장점: 어떤 반복 처리를 하는지 이해하기 쉽고, 반복 조건의 초기화 작업과 갱신 작업을 빠뜨리는 등의 실수를 사전 방지 가능
           
           
  - 중첩 반복문: for 문 안에 for 문 작성
```javascript
var n = 20;
for(var a = 1; a <=n; a++) {
  for(var b = 1; b <= n; b++) {
    for(var c = 1; c <= n; c++) {
      if( a*a + b*b == c*c ) {
        console.log(a + "^2 + " + b + "^2 = " + c + "^2");
      }
    }
  }
}
```
4. for/in문 📑
 - for/in 문은 객체 안의 프로퍼티를 순회하는 반복문
 
       for (변수 in 객체 표현식) 문장
       
 - 먼저 객체 표현식을 평가 
 
    → 객체 표현식이 null 또는 undefined로 평가되면 for/in 문을 빠져나와 다음 작업으로 이동

    →객체 표현식이 객체로 평가되면 객체의 프로퍼티 이름이 차례대로 변수에 할당되고 각각의 프로퍼티에 대해서 문장이 한 번씩 실행
    
```javascript
var obj = {a:1, b:2, c:3};
for(var p in obj) {
    console.log("p = " + p);
} 
```
출력 결과
p = a
p = b
p = c

### 점프문
  - 점프문은 프로그램의 다른 위치로 이동하는 제어 구문
1. 라벨문 📑
   - js에서는 모든 문장에 라벨을 붙일 수 있음
           
         라벨 이름 : 문장
   - js에서 라벨로 점프할 수 있는 문장은 break 문과 continue 문뿐
   - break 문 : switch 문, 반복문 안에서만 사용 가능
   - continue 문 : 반복문 안에서만 사용 가능
      즉, 실제로 라벨을 붙여서 사용가능한 문장은 switch 문과 반복문뿐
      
2. break문 📑
       
       break;
  - break 문은 switch 문과 반복문 안에서만 사용 가능
  - break 문을 실행하면 가장 안쪽에 있는 반복문이나 switch 문에서 빠져나옴
  - break 문에는 점프할 라벨을 지정할 수 있음
   
        break 라벨 이름;
  - 라벨을 지정한 break 문을 실행하면 라벨일 붙은 문장 끝으로 점프(break 문에서 지정한 라벨 X? 문법 오류 발생)
  *주의 : break 문과 라벨 이름 사이에는 줄 바꿈 문자를 넣지 않도록 !!!! ( 줄 바꿈 문자를 넣으면 js 엔진이 내부적으로 세미콜론을 추가함. 즉, 라벨을 지정하지 않은 break문으로 해석)
  
3. continue문 📑
     
       continue; 
  - continue 문에도 점프할 라벨 지정할 수 있음
       
        continue 라벨 이름;
  - break 문과의 차이 : continue 문은 라벨 지정 여부와 관계없이 반복문 안에서만 사용할 수 있다!
