# 제어구문
- 순차적 실행
일반적으로 문장은 위에서 아래로 순서대로 실행된다. 순차적 실행 흐름을 변화시키는 문장을 제어구문이라고 한다.

오늘은 자바스크립트의 조건문, 반복문, 점프문 등의 제어구문을 공부해보자.

---

# 조건문
조건문은 조건식의 값에 따라 실행 흐름을 분기한다.

## 🔎 if 문 

if(...)문은 괄호 안의 조건식이 true면 문장을 실행한다.
```javascript
if (조건식) 문장

// 문장을 여러줄로 쓰고 싶으면 중괄호로 문장을 감싸야 한다.
if (조건식) {
    문장1
    문장2
}
```

### else 절

if 문에 else절을 붙일 수 있는데, else 뒤에 이어지는 문장은 조건이 거짓인 경우 실행된다.   
if/else => "만약 ~이라면... 그렇지 않으면...' 이런 식이다.

```javascript
if (조건식) 문장 1
else 문장 2
```

### else if 절로 복수 조건 처리

복수의 조건을 처리해야하는 경우 else if를 사용할 수 있다. (else if 더 많이 쓰는것도 가능)

```javascript
if (year < 2015) {
  alert( '숫자를 좀 더 올려보세요.' );
} else if (year > 2015) {
  alert( '숫자를 좀 더 내려보세요.' );
} else {
  alert( '정답입니다!' );
}
```

### 중첩된 if 문

if 문도 일종의 문장이므로 if 문 안에 if 문을 작성할 수 있다. 이러한 if 문을 중첩된 if 문이라고 한다.   
특히 else 절이 있는 경우 어떤 if와 호응하는지 유의해야 한다.

```javascript
if (a > b) 
    if (a > c) 
        console.log("a가 가장 크다");
else 
    console.log("a는 b 이하");

```
위의 예제는 언뜻 보면 들여쓰기 기준으로 else가 if (a > b)랑 호응 관계로 보이는데,   
else 절을 가까운 if에 호응하므로 아래 예제와 같이 if (a > c)랑 호응 관계이다.

```javascript
if (a > b) {
    if (a > c) {
        console.log("a가 가장 크다");
    } else {
        console.log("a는 b 이하")
    }
}
```
앞으로 코드를 짜다보면 실행할 문장이 하나면 길이도 길어지고 그래서 중괄호를 안하는 경우가 빈번한데,   
이러한 잘못된 해석을 피하려면 중괄호로 묶는 습관을 권장한다.

---

## 🔎 switch 문

복수의 if 조건문은 분기점을 여러 개 만들 수 있지만 코드가 복잡해진다.    
이런 경우 switch 문을 사용하면 특정 변수를 다양한 상황에서 비교하여 간결하게 표현 할 수 있다. 

- switch문은 하나 이상의 case문으로 구성된다. 대개 default 문도 있지만 default 문은 필수는 아니다.

```javascript
switch(x) {
    case 'value1':  // if (x === 'value1')
        console.log("one")
        break;
    case 'value2':  // if (x === 'value2')
        console.log("two")
        break;
    default:
        console.log("other")
}
```
- 변수 x의 값과 첫 번째 case문의 값 'value1'를 일치 비교한 후, 두 번째 case문의 값 'value2'와 비교한다. 이런 과정은 계속 이어진다.
- case문에서 변수 x의 값과 일치하는 값을 찾으면 해당 case 문의 아래의 코드가 실행된다.   
이때, break문(return문도 사용가능)을 만나거나 switch 문이 끝나면 코드의 실행은 멈춘다.
- 값과 일치하는 case문이 없다면, default문 아래의 코드가 실행됩니다(default 문이 있는 경우).

### 만약 break문이 없다면?
case문 안에 break(or return)문이 없으면 조건 부합 여부에 상관없이 이어지는 case 문을 switch 블록이 끝날 때까지 실행한다.

```javascript
let a = 2 + 2;

switch (a) {
  case 3:
    console.log( '비교하려는 값보다 작습니다.' );
  case 4:
    console.log( '비교하려는 값과 일치합니다.' );
  case 5: // 이렇게 두 case 문을 묶을 수도 있다.
  case 6:
    console.log( '비교하려는 값보다 큽니다.' );
  default:
    console.log( "어떤 값인지 파악이 되지 않습니다." );
}

// 실행
'비교하려는 값과 일치합니다.'
'비교하려는 값보다 큽니다.'
"어떤 값인지 파악이 되지 않습니다."
```

### switch/case 문의 인수엔 어떤 표현식(+a, b+1)이든 올 수 있다. 
단, 표현식을 쓰면 알고리즘을 파악하기 어려워질 수 있으므로 숫자 리터럴 또는 문자열 리터럴로 사용하는 편이 좋다.
C나 Java에는 아래와 같이 규칙이 정해져있는데 자바스크립트에서는 어떤 표현식이든 올 수 있다.

> C / Java의 switch문
>1. switch에 사용하는 식의 결과는 정수 혹은 문자(열) 이어야 한다.
>2. switch에 사용하는 식은 논리형(boolean)값을 사용할 수 없다. --> switch(true) : 에러남
>3. case에는 단일 상수, 문자(열) 값만 사용할 수 있음. --> case a > 3 : 에러남

---

# 반복문

반복문은 일정한 처리를 한 다음 원래 위치로 돌아가 똑같은 처리를 반복한다.
자바스크립트 반복문에는 while 문, do/while 문, for 문, for/in 문, for/of 문이 있다. 

## 🔎 while 문

while 문은 조건만 true면 일정한 처리를 계속 반복해서 실행한다.

```javascript
while (조건식) {
    문장
}
```
- while 문 안에서 break를 실행하면 while 문 탈출
- while 문 안에서 continue를 실행하면 while 문의 시작 부분으로 돌아간다

## 🔎 do while 문 

앞서 살펴본 while 문은 반복해서 실행할지를 시작 부분에서 판단하지만, do while 문은 마지막 부분에서 판단한다.
그래서 일단 조건 부합 여부에 상관없이 한번은 무조건 실행된다.

**do/while 문은 끝에 반드시 세미콜론이 붙는다.**
```javascript
do {
  문장
} while (조건식);
```

- while 문과 동일하게 break, continue문 사용 가능

---

## 🔎 for 문
가장 많이 쓰이는 반복문으로써, 반복 조건의 초기화, 반복문의 조건식, 반복 작업이 하나 끝났을 때 반복조건 갱신 작업을 한번에 표기한다.

```javascript
for (초기화식; 조건식; 반복식) {
    문장
}
```
그럼 for문을 구성하는 각 요소가 무엇을 의미하는지 알아보자.   
아래 반복문을 실행하면 i가 0부터 3 미만이 될 때 까지 console.log(i)가 호출된다.

```javascript
for (let i = 0; i < 3; i++) {  // 0, 1, 2가 출력
  console.log(i);
}
```
|구성요소|코드|작업|
|---|---|---|
|초기화식|i = 0|반복문에 진입할 때 단 한번 실행된다.|
|조건식|i < 3|반복마다 해당 조건이 확인되고 false일 경우 멈춘다|
|문장|console.log(i)|조건식이 true일 경우 계속해서 반복 실행|
|반복식|i++|반복 작업이 하나 끝났을 때 실행되어 갱신된다.|

### 구성요소 생략하기

초기화 식, 조건식, 반복식 모두 생략 가능하다. 단, 세미콜론 만큼은 생략할 수 없다. 하나라도 없으면 문법 오류가 발생하기 떄문이다.

아래는 모든 구성요소를 생략할 경우 무한반복문이 되는 모습이다. 
```javascript
for (;;) {
  // 끊임 없이 본문이 실행됩니다.
  // 멈추려면 break 실행
}
```

### 중첩 반복문
for 문 안에 for 문을 작성하면 중첩 반복문을 만들 수 있다.

## 🔎 for/in 문 

for/in 문은 객체 안의 프로퍼티를 순회하는 반복문이다. 
실행되면 먼저 객체표현식을 평가하는데, 객체 표현식이 null or undefined로 평가되면 for/in문을 빠져나오고.  
객체 표현식이 객체로 평가되면 객체의 프로퍼티 이름이 차례대로 변수에 할당되어서 각각의 프로퍼티에 대해서 문장이 한번씩 실행된다.

```javascript
for (변수 in 객체표현식) {
    문장
}
```

```javascript
// 프로퍼티 이름 가져오기
let obj = {a:1, b:2, c:3};
for (let p in obj) { 
    console.log("p=" + p);
}

// 실행
"p=a" "p=b" "p=c"
```

```javascript
// 프로퍼티 값 가져오기
let obj = {a:1, b:2, c:3};
for (let p in obj) { 
    console.log("obj." + p + "=" + obj[p]); 
} 

// 실행
"obj.a=1" "obj.b=2" "obj.c=3"
```

---

# 점프문

점프문은 프로그램의 다른 위치로 이동하는 제어구문이다. 자바스크립트의 점프문에는 break 문, continue 문, return 문, throw 문이 있다. 

문장에 라벨을 붙이면 해당 문장의 끝이 break, continue 문 같은 점프문을 실행 뒤 점프할 수 있는 위치가 된다.

## 🔎 라벨문

제어를 직접 지정할 때 사용한다.

자바스크립트에서는 모든 문장에 라벨을 붙일 수 있지만 라벨로 점프할 수 있는 문장은 break 문과 continue 문뿐이다.
왜냐하면 break문은 switch문과 반복문 안에서만 사용가능하고, continue문은 반복문 안에서만 사용 가능하기 떄문이다.

하지만 프로그램 처리 구조에 주의해야 함
너무 많이 사용하면 프로그램의 논리성이 약해지고, 순환 구조로 프로그래밍하면 무한 반복에 빠질 수 있기 때문이다.

사용법
``` javascript
라벨 이름 : 문장

// 라벨 이름에는 모든 식별자 사용 가능
```
라벨문은 break, continue 문에서 더 자세하게 알아보자.

---

## 🔎 break 문
break 문은 switch 문과 반복문 안에서만 사용 가능하다.
break 문을 실행하면 <u>가장 안쪽에 있는 반복문</u>이나 switch문에서 빠져나온다.

```javascript
// 사용법
break;

// 점프할 라벨 지정
break 라벨 이름;
```

break loop를 실행하면 앞뒤 코드와 상관없이 loop라는 라벨이 붙은 while 문 끝으로 점프하여 빠져나온다.
만약 break문에서 지정한 라벨이 없으면 문법 오류가 발생한다.
```javascript
loop: while(true) {
    ...
    if(confirm("종료하시겠습니까?")) break loop;
    ...
}
```

라벨을 지정한 break 문은 주로 중첩된 반복문의 안쪽 반복문 안에서 전체 반복문을 빠져나올 때 사용한다. 
```javascript
let a = [2, 4, 6, 8, 10], b = [1, 3, 5, 6, 9, 11];
loop : for(var i=0; i<a.length; i++) {
    for(var j=0; j<b.length; j++) {
        if(a[i] == b[j]) break loop;
    }
}
console.log("a[" + i + "] = b[" + j + "]")

// 실행
a[2] = b[3]
```
>break문과 라벨 이름 사이에는 줄 바꿈 문자를 넣지 않도록 주의
줄 바꿈 문자를 넣으면 자바스크립트 엔진이 내부적으로 세미콜론을 추가하므로 라벨을 지정하지 않은 break문으로 해석하기 때문이다.

---

## 🔎 continue 문 
continue문은 라벨 지정 여부와 관계없이 반복문 안에서만 사용할 수 있다는 점이 break 문과 다른점이다.
continue문을 실행하면 반복문 실행을 멈추고 반복을 새로 시작한다.

이때 동작이 반복문에 따라 달라진다.

- while문: 반복문의 처음으로 되돌아가 조건식을 다시 평가 => 조건식이 true면 반복문 처음부터 실행
- do/while문: 중간을 건너뛰고 반복문의 마지막 조건식 평가 => 조건식이 true면 반복문 처음부터 실행
- for문: 반복식을 실행한 후에 조건식 평가 => 조건식이 true면 반복문 이어서 실행
- for/in문: 반복문의 처음으로 되돌아감 => 지정한 변수에 할당되어 있는 프로퍼티의 다음 프로퍼티를 대상으로 작업 실행

```javascript
// 사용법
continue;

// 점프할 라벨 지정
continue 라벨 이름;
```

```javascript
var a = [2, 5, -1, 7, -3, 6, 9]
var sum
for(var i = 0, sum = 0; i<a.length; i++) {
    if(a[i] < 0) continue;
    sum += a[i]
}
console.log(sum)

//실행
29
```

라벨을 지정한 continue문 중첩 반복문에서 사용하는 경우
```javascript
loop : for(var i=0; i<3; i++) {
    for(var j=0; j<3; j++) {
        if(i == 1 && j == 0) continue loop;
        console.log("i = " + i + ", j = " + j )
    }
}

// 실행
i = 0, j = 0
i = 0, j = 1
i = 0, j = 2
i = 2, j = 0
i = 2, j = 1
i = 2, j = 2
```
