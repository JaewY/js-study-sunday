# 제어구문
- 순차적 실행
일반적으로 문장은 위에서 아래로 순서대로 실행된다. 순차적 실행 흐름을 변화시키는 문장을 제어구문이라고 한다.

오늘은 자바스크립트의 조건문, 반복문, 점프문 등의 제어구문을 공부해보자.

# 조건문
조건문은 조건식의 값에 따라 실행 흐름을 분기한다.

- if 문 

if(...)문은 괄호 안의 조건식이 true면 문장을 실행한다.
```javascript
if (조건식) 문장

// 문장을 여러줄로 쓰고 싶으면 중괄호로 문장을 감싸야 한다.
if (조건식) {
    문장1
    문장2
}
```
- else 절

if 문에 else절을 붙일 수 있는데, else 뒤에 이어지는 문장은 조건이 거짓인 경우 실행된다.   
if/else => "만약 ~이라면... 그렇지 않으면...' 이런 식이다.

```javascript
if (조건식) 문장 1
else 문장 2
```

- else if 절로 복수 조건 처리

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

- 중첩된 if 문

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

# switch 문

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

## 만약 break문이 없다면?
- case문 안에 break(or return)문이 없으면 조건 부합 여부에 상관없이 이어지는 case 문을 switch 블록이 끝날 때까지 실행한다.

```javascript
let a = 2 + 2;

switch (a) {
  case 3:
    alert( '비교하려는 값보다 작습니다.' );
  case 4:
    alert( '비교하려는 값과 일치합니다.' );
  case 5: // 이렇게 두 case 문을 묶을 수도 있다.
  case 6:
    alert( '비교하려는 값보다 큽니다.' );
  default:
    alert( "어떤 값인지 파악이 되지 않습니다." );
}

// 실행 
alert( '비교하려는 값과 일치합니다.' );
alert( '비교하려는 값보다 큽니다.' );
alert( "어떤 값인지 파악이 되지 않습니다." );
```

## switch/case 문의 인수엔 어떤 표현식(+a, b+1)이든 올 수 있다. 
단, 표현식을 쓰면 알고리즘을 파악하기 어려워질 수 있으므로 숫자 리터럴 또는 문자열 리터럴로 사용하는 편이 좋다.
C나 Java에는 아래와 같이 규칙이 정해져있는데 자바스크립트에서는 어떤 표현식이든 올 수 있다.

> C / Java의 switch문
>1. switch에 사용하는 식의 결과는 정수 혹은 문자(열) 이어야 한다.
>2. switch에 사용하는 식은 논리형(boolean)값을 사용할 수 없다. --> switch(true) : 에러남
>3. case에는 단일 상수, 문자(열) 값만 사용할 수 있음. --> case a > 3 : 에러남


# 반복문


