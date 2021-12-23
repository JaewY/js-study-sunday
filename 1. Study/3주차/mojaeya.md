# 표현식과 연산자
- 여기서 표현식이란?   
결과적으로 어떤 값으로 평가되는것

- 표현식을 평가한다?   
표현식의 값과 변수, 함수 등의 값을 바탕으로 식의 값을 계산하는 행위를 뜻함

- 가장 간단한 표현식은 숫자, 문자열, 논리값 등의 원시값이다.   
  >3.14, "hello", true, false, null 

- 그 외에 변수, 프로퍼티, 배열요소, 함수 호출, 메서드 호출도 표현식이다.   
  >sum, circle.radius, a[3], square(5), card.getSum()
 
- 연산자는 일반적으로 피연산자 개수에 따라 단항, 이항, 삼항연산자로 분류된다.   
  >-x, a+b, a ? x : y
  
- 조건 선택 연산자 : (조건식) ? A : B  (삼항 연산자)
  조건식이 참이면 A 거짓이면 B
 
# 산술 연산

- 산술 연산자란?   
피연산자가 숫자인 연산자

> 피연산자가 숫자가 아닐 때는 연산자가 피연산자 타입을 숫자 타입으로 바꾸어 연산한다.   
피연산자가 숫자로 바꿀 수 없거나, 계산할 수 없을때는 NaN이 나온다.   
모든 산술 연산은 64비트 부동소수점 연산으로 이루어진다.

### 산술 이항 연산자
```
+, - : 수학에서 사용하는 기호와 같다.
* : 곱하기
/ : 나누기
% : 나눈 나머지
```
1. 정수끼리 나누어도 결과가 부동소수점이 된다.
다른 프로그래밍 언어에서는 정수/정수의 결과값이 정수지만,   
자바스크립트에서는 모두 부동소수점이 된다!
```
7 / 2   //   3.5
```

2. 나머지 연산자 %의 피연산자는 부동소수점도 가능하다.
일부 프로그래밍 언어에서는 정수만 나머지 연산자 %로 구할 수 있는데,   
자바스크립트에서는 모두 부동소수점으로 계산 가능하다!
```
15 % 4   //  3
5 % 1.5  // 0.5
```
3. 숫자와 문자열의 덧셈을 제외한 사칙연산.  

'+' 연산자는 피연산자 중 하나가 문자열이면 나머지 피연산자를 문자열로 만든다.
```
1 + "2month"  //  "12month"
```
나머지 연산자에서는 문자열을 숫자로 바꾸어서 연산을 한 결과가 출력
```
1 * "2month" // NaN  => 문자열이 숫자가 아닐 경우는 형변환을 해서 연산을 하지 못하고 NaN를 반환
'24' / 2 // 12
'24' - 2 // 22
```

4. 기타
```
0 / 0 //  NaN : 계산 불가
"one" * 1 //  NaN : 계산 불가

true + true  //  2    => true는 1, false는 0
1 + null  //  1  => null은 0
1 + undefined // -> NaN
```

### 산술 단항 연산자
```
증감연산자 : ++  --  * 1씩 증가, 1씩 감소
* 전위형 : ++변수, --변수 : 증가/감소하고 동작 
* 후위형 : 변수++, 변수-- : 동작하고  증가/감소

+ : 아무것도 처리하지 않음
- : 부호 반전
```

### 산술 대입 연산자
```
a += b : a = a + b
a -= b : a = a - b
a *= b : a = a * b
a /= b : a = a / b
a %= b : a = a % b
```

### 비교연산자 
```
>, <, >=, <=, ==, ===(같다), !=, !==(같지 않다)

* 비교연산자는 결과가 true / false 로 나옴. 
 ```

**==, ===, !=, !== 의 차이가 뭐지?**
- 결론부터 말하면 형변환을 하냐 안하냐 차이다.
- 동일 비교 연산자(==, !=) : 형변환을 해 두 피연산자의 자료형을 일치시킨 뒤, 서로 같은지 비교를 진행한다. 
- 일치 비교 연산자(===, !==) : 형변환을 하지 않은 상태에서 두 피연산자가 서로 같은지 비교를 진행한다. (값하고 자료형까지 같아야 일치)


### 논리연산자
```
&&, ||, !  = [ and, or, not ] 

* A && B : A가 참이고, B도 참. 둘다 참이어야 함.  => 하나라도 거짓이면 거짓 
* A || B : A 또는 B 중 하나만 참이여도 참  => 둘다 거짓일 경우만 거짓 
* !A : A가 참이면 거짓, 거짓이면 참
```

### 비트연산자 : 변수 값을 비트로 나열한 후 연산
- 비트 연산자는 32 비트 숫자 작업
- 작동에 있는 숫자 피연산자는 32비트 값으로 변환된다.
- 결과는 자바스크립트 번호로 다시 변환

<img width="80%" alt="스크린샷 2021-10-24 오후 8 52 38" src="https://user-images.githubusercontent.com/76654131/138592875-40370241-97b8-4992-b24e-262a461355f0.png">


### Math 객체
- 수학에서 자주 사용하는 상수와 함수들을 미리 구현해 놓은 자바스크립트 표준 내장 객체이다.
- Math 객체는 다른 전역 객체와는 달리 생성자(constructor)가 존재하지 않는다.   
따라서 따로 인스턴스를 생성하지 않아도 Math 객체의 모든 메소드나 프로퍼티를 바로 사용할 수 있다.

### Math 메소드
자바스크립트는 웹 페이지에서 수학적 작업을 손쉽게 할 수 있도록 다양한 Math 메소드를 제공하고 있다.   
가장 많이 사용되는 대표적인 Math 메소드는 아래와 같다.
```
1. Math.min() // 인수로 전달받은 값 중에서 가장 작은 수를 반환
2. Math.max() //  인수로 전달받은 값 중에서 가장 큰 수를 반환
3. Math.random() // 0보다 크거나 같고 1보다 작은 무작위 숫자(random number)를 반환
4. Math.round() //  인수로 전달받은 값을 소수점 첫 번째 자리에서 반올림하여 그 결괏값을 반환
5. Math.floor() // 인수로 전달받은 값과 같거나 작은 수 중에서 가장 큰 정수를 반환
6. Math.ceil() // 인수로 전달받은 값과 같거나 큰 수 중에서 가장 작은 정수를 반환
```

# 문자열 제어하기
- 문자열을 처리하기 위한 객체로 String 객체가 마련되어 있음.
- 문자열을 String 객체로 변환 하려면 String 생성자를 사용함.

```
var msgObj = new String("Everything is practice.");
// 원시 값을 객체로 변환하는 행위를 원시값을 객체로 래핑(wrapping)한다고 함.

var msg = "Everything is practice.";
console.log(msg.length); // -> 23
onsole.log(msg.charAt(3)); // -> r (문자열의 n번째 문자를 구할 수 있음)
// String 객체의 프로퍼티와 메서드는 문자열에서도 사용할 수 있음.
// 래퍼 객체(wrapper object)로 자동 변환되기 때문
```

- 문자열 메서드 사용 예
```
var msg = "Everything is practice.";
msg.substring(7, 10) // -> "ing" : 7번째 문자열부터 10번째 이전의 문자열
msg.slice(7, 10) // 위 코드와 같음
msg.slice(-3) // "ce." : 마지막 문자 세 개
msg.indexOf("t") // -> 5 : 문자 t가 처음 나오는 위치
msg.indexOf("i", 10) // -> 11 : 10번째 이후 문자에서 "i"가 처음 나오는 위치
msg.lastIndexOf("t") // -> 18 :  문자 "t"가 마지막으로 나오는 위치
msg.split(" ") // -> ["Everything", "is", "practice."] : " "로 문자열을 나눔
msg.replace("p","P") // -> 'Everything is Practice.' : "p" -> "P"
msg.toUpperCase() // -> 'EVERYTHING IS PRACTICE.'
msg.endsWith(".") // -> true
msg.includes("thing") // -> true
```

- JS에서 string replaceAll
```
var msg = "Everything is practice.";
msg.replace('i','I');
'EverythIng is practice.' // 앞에 한 글자만 바뀐다.

// 1. 정규식을 이용한 replace> msg.replace(/i/gi,'I');
'EverythIng Is practIce.'// gi는 정규식 옵션
// g: global
// i: ignor case
// m: multiline

// 2. replaceAll 함수 사용
const replaceAll = (str, searchStr, replaceStr) => str.split(searchStr).join(replaceStr);
replaceAll("Everything is practice.", "i", "I");
> 'EverythIng Is practIce.'
```

- 문자열을 배열로 읽고 쓰기
```
// 문자열을 읽을 때는 charAt 메서드 대신 대괄호 연산자를 사용할 수 있음.
var msg = "Everything is practice.";
msg[3] // -> r
// 그러나 배열처럼 값을 대입해서 수정할 수 없음. 대입해도 무시됨.
msg[3] = "R";
```

# 명시적 타입 변환 

- 숫자 + 문자열
```
10 + "little indians" // "10 little indians"
```

- Number 객체의 메서드 활용
```
var n = 26;
n.toString() // -> "26" : 인수를 지정하지 않으면 10진수 문자열로 변환
n.toString(2) // -> "11010" : 2진수 문자열로 변환

var x = 1234.567;
x.toFixed(0) // -> "12345" : 숫자의 소수점 아래 자릿수를 지정한 문자열로 변환
```

- String 함수 활용
```
// String 생성자 앞에 new 연산자를 붙이면 String 객체를 생성하는 함수로 사용할 수 있지만,
// new 연산자를 붙이지 않으면 일반적인 함수로 활용 가능. 반환값은 문자열.

String(26) // -> "26"
String(1234.567) // -> "1234.567"

// String 함수에는 모든 데이터 타입을 문자열 타입으로 바꾸는 기능이 있음.

String(true) // -> "true"
String(NaN) // -> "NaN"
String(null) // -> "null"
```

### 문자열을 숫자로 변환하기

- 수식 안에서 묵시적으로 변환
```
var s = "2";
s - 0 // -> 2
+s    // -> 2
```

- parseInt, parseFloat 함수 사용
```
// 문자열의 첫 번째 문자를 숫자로 바꾼 값을 반환하고, 이후에 등장하는 문자열은 무시.
// 첫 번째 문자를 숫자로 해석할 수 없을 때는 NaN을 반환.
// 문자열 앞 부분의 공백 문자는 무시
```

- Number 함수 활용
```
// Number 생성자 앞에 new 연산자를 붙이면 Number 객체를 생성하는 함수로 사용할 수 있지만,
// new 연산자를 붙이지 않으면 일반적인 함수로 활용 가능. 반환값은 숫자.

Number("2.71828") // -> 2.71828

Number(true) // -> 1
Number(NaN) // -> NaN
```

- 논리값으로 변환하기 = Boolean() 의한 자료형 변환
```
x = 1

!x // -> false : !연산자는 논리 타입이 아닌 값의 타입을 논리 타입으로 바꿈.
!!x // -> true

Boolean(x) // -> true
```

**자바스크립트에서 Boolean() 결과가 false로 판명되는 것들은 다음과 같다.**

- undefined, null
- NaN
- 0 (숫자 리터럴) , -0
- “” (빈 문자열)
- false

#### 다른 유형의 데이터를 비교하는 것은 예상치 못한 결과를 얻을 수 있다. 위에 내용을 숙지한 뒤 아래 내용으로 점검해보자.

<img width="50%" src="https://user-images.githubusercontent.com/76654131/138594485-daf0efde-73a1-4fb7-9a7b-6b028330a414.png">

참조 및 인용
[https://velog.io/@k904808/표현식과-연산자](https://velog.io/@k904808/표현식과-연산자)
[http://www.w3bai.com/ko/js/js_comparisons.html](http://www.w3bai.com/ko/js/js_comparisons.html)
