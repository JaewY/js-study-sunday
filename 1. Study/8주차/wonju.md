# 배열의 다양한 기능

## ✔ 배열의 메서드

배열은 Array 타입 객체이며, Array.prototype의 프로퍼티를 상속받습니다. 수많은 메서드들이 정의되어 있으며, 모든 배열은 이 메서드를 사용할 수 있습니다. 이 메서드를 통해 다양한 배열을 처리할 수 있습니다.

### Array.prototype의 메서드 목록

- 수정 메서드: 원본 배열을 바로 수정합니다.

- 접근자 메서드: 배열을 다른 형태로 가공한 새로운 배열을 반환하며, 원본 배열은 수정하지 않습니다.

- 반복 메서드: 원본 배열의 모든 요소를 순회하며 특정 작업을 수행합니다.

---

### 수정 메서드

**push**

push 메서드는 배열 마지막에 하나 이상의 요소를 추가한 후 배열의 길이를 반환합니다.

요소를 두 개 이상 추가하려면 쉼표로 구분해줍니다.

```javascript
var a = ["A", "B", "C"];
a.push("D"); // ["A", "B", "C", "D"] : 4 출력(배열의 길이)

a.push("E", "F"); // a = ["A", "B", "C", "D", "E", "F"]
```

**pop**

pop 메서드는 배열의 마지막 요소를 잘라내 반환합니다.

```javascript
var a = ["A", "B", "C"];
a.pop(); // a = ["A", "B"] : "C" 출력
```

**shift**

shift 메서드는 배열의 첫 번째 요소를 제거한 후, 삭제된 요소의 값을 반환합니다.

```javascript
var a = ["A", "B", "C"];
a.shift(); // a = ["B", "C"] : "A" 출력
```

**unshift**

unshift 메서드는 배열의 앞부분에 한 개 이상의 요소를 추가합니다(shift메서드와 반대). 배열의 길이를 반환합니다.

```javascript
var a = ["A", "B", "C"];
a.unshift("X"); // a = ["X", "A", "B", "C"] : 4 출력
```

**splice**

splice 메서드는 특정 요소를 갈아 끼울 때(끼워넣기나 삭제) 사용합니다. 삭제된 요소는 배열로 만들어 반환합니다. splice에는 '이어붙이기' 라는 뜻이 있습니다.

첫번째 인수(index):

배열을 수정하기 시작할 위치 가리키는 인덱스. 값이 배열 길이보다 클 경우 배열 마지막을 시작으로, 값이 음수면 이 값에 배열 길이를 더한 값을 시작 위치로 본다.

두번째 인수(howmany):

삭제할 요소의 개수. 0을 넘기면 어떤 요소도 삭제하지 않는다. 이때는 인수로 새로운 요소를 최소 1개를 넘겨야 한다. 아무값도 넘기지 않으면 index 이후 모든 요소를 삭제한다.

세번째 인수:

배열에 삽입할 요소를 쉼표로 구분해 넘긴다. 값이 없으면 단순히 배열에서 요소를 삭제한다.

- 첫번째 인수만 넘기면 그 인덱스 이후 모든 배열 요소를 삭제합니다.

```javascript
var a = ["A", "B", "C", "D"];
a.splice(2); // a = ["A", "B"] : ["C", "D"] 출력
```

- 첫번째 인수가 음수면 그 값에 배열 길이를 더한 값을 시작 위치로 간주합니다.

```javascript
var a = ["A", "B", "C", "D"];
a.splice(-1); // a = ["A", "B", "C"] : ["D"] 출력
```

- 두번째 인수가 0이면 index가 가리키는 요소 바로 앞에 세번 째 이후 요소를 끼워 넣습니다.

```javascript
var a = ["A", "B", "C", "D"];
a.splice(1, 0, "X", "Y"); // a = ["A", "X", "Y", "B", "C", "D"] : [] 출력
```

**sort**

sort 메서드는 배열 안 요소를 정렬합니다. 반환값은 정렬된 배열입니다.

```javascript
var a = [5, 2, 7, 1, 3, 9, 8];
a.sort(function (a, b) {
  return a - b;
});
//  a = [1, 2, 3, 5, 7, 8, 9]
```

비교함수는 배열 안의 인접한 요소를 비교하는 역할을 합니다. 인수를 두 개 받으며,
f(a, b) 로 가정할 때 비교함수는 다음과 같은 규칙을 따라야 합니다.

    - f(a, b) < 0 이면 a를 b보다 작은 인덱스로 정렬한다.
    - f(a, b) == 0 이면 a와 b의 순서를 바꾸지 않는다.
    - f(a, b) > 0 이면 b를 a보다 작은 인덱스로 정렬한다.

비교함수를 지정하지 않으면 배열의 요소를 문자열로 변환해 사전순으로 정렬합니다. 값이 undefined인 요소가 있다면 배열의 마지막에 위치합니다.

---

### 접근자 메서드

**join**

join 메서드는 배열의 모든 값을 문자열로 바꾼 후 인수로 받은 문자로 연결해 반환합니다. 요소값이 undefined이거나 null일 때는 요소값을 빈 문자로 간주하며, 인수를 지정하지 않으면 쉼표로 연결해 반환합니다.

```javascript
var a = ["A", "B", "C"];
a.join("-"); // "A-B-C"

a.join(""); // "ABC"
```

**concat**

concat 메서드는 인수로 받은 값을 배열의 요소로 추가해 새로운 배열을 만듭니다. 받은 인수가 배열일 경우 펼친후에 배열에 추가합니다. concat은 concatenate의 줄임말(사슬로 만들다, 연결하다)

값을 여러개 추가하면 쉼표로 구분해 입력하며,

원시값도 배열에 추가할 수 있습니다.

배열은 한 번만 펼쳐 추가합니다.

concat 메서드는 얕은 복사를 합니다. 즉, 인수 값이 객체의 참조면 그 참조값을 복사합니다. 따라서 원본 객체를 수정하면, concat메서드가 반환한 배열의 요소도 함께 바뀝니다.

```javascript
var a = ["A", "B", "C"];
a.concat(["D", "E"]); // ["A", "B", "C", "D", "E"]

a.concat("D", ["E", ["F", "G"]]); //["A", "B", "C", "D", "E", ["F", "G"]]
```

**slice**

slice메서드는 배열 요소 일부를 제거한 새로운 배열을 반환합니다.

첫번째 인수(begin): 요소 꺼낼 위치를 뜻하는 인덱스. 값이 음수면 이 값에 배열길이를 더한 값을 시작위치로 간주하며, 생략하면 0으로 간주한다.

두번째 인수(end): 요소 꺼낼 마지막 위치를 뜻하는 인덱스. end가 가리키는 요소의 바로 이전요소까지 잘라낸다. 값이 음수면 이 값에 배열길이를 더한 값을 마지막위치로 간주하며, 생략하면 배열의 끝으로 간주한다.

```javascript
var a = ["A", "B", "C", "D", "E"];
a.slice(1, 3); // ["B", "C"] 출력
```

두번째 인수인 end를 생략하면 마지막 요소까지 잘라냅니다.

```javascript
a.slice(3); // ["D", "E"]
```

음수는 끝에서 n번째 라는 뜻입니다.

```javascript
a.slice(1, -1); // ["B", "C", "D"]
a.slice(-3, -2); // ["C"]
```

**indexOf와 lastIndexOf**

두 메서드는 배열 안에서 인수로 지정한 값을 검색해 가장 먼저 찾은 요소의 인덱스를 반환하며, 못찾았을 경우 -1 을 반환합니다.

indexOf메서드는 인덱스가 작은 쪽부터, lastIndextOf메서드는 인덱스가 큰쪽부터 검색합니다.

첫번째 인수: 검색할 값

두번째 인수: 검색 시작할 인덱스. 생략하면 0으로 간주. 배열길이를 넘는 값을 입력하면 검색X. 값이 음수면 배열길이를 더한 값을 시작위치로 간주.

```javascript
"C"를 작은, 큰 인덱스부터 검색하는 예

var a =  ["A", "B", "C", "C", "D"];
a.indexOf("C")  //  2
a.lastIndexOf("C")  // 3
```

**toString과 toLocaleString**

두 메서드는 배열의 요소를 문자열로 변환해 쉼표로 연결한 문자열을 반환합니다.

이 메서드는 Object.prototype에 있는 같은 이름의 메서드를 다시 정의한 것입니다.

toLocalString 메서드는 해당 지역에 맞는 언어로 번역한 문자열로 변환합니다.

```javascript
["A", "B", "C", date].toString(); // "A, B, C"
[1, 2, 3, date].toString(); // "1, 2, 3"
[1, [2, 3], date].toString(); // "1, 2, 3"

var date = new Date();
console.log(["A", "B", "C", date].toString()); // "A, B, C, Wed Jan 03 2018 22:56:54 GMT+0900 (KST)"

console.log(["A", "B", "C", date].toLocalString()); // "A, B, C, 2018. 1. 3. 오후 10:56:54"
```

---

### 반복 메서드

반복메서드가 지닌 공통적인 성질:

1. 인수로 전달한 함수는 배열의 요소마다 호출됩니다.

2. 대부분은 첫번째 인수로 함수를 받으며, 이 함수에는 인수 세개가 전달됩니다. 보통은 첫번째 인수만 사용하는 경우가 많으며, 두번째/세번째 인수는 생략할 수 있습니다.

   - 첫번째 인수(value): 현재 처리하고 있는 배열 요소의 값
   - 두번째 인수(index): 현재 처리하고 있는 배열 요소의 인덱스
   - 세번째 인수(array): 메서드가 적용되는 배열의 참조

3. reduce와 reduceRight을 제외한 나머지 반복메서드에는 두번째 인수를 지정할 수 있습니다. 두번째 인수는 첫번째 인수로 받은 함수 안의 this값이며 생략가능합니다.

**forEach**

인수로 받은 함수를 배열의 요소별로 한번씩 실행합니다. 함수에는 인수 세개가 전달됩니다.

forEach 메서드를 for문 대신 사용할 수 있습니다.

```javascript
var a = [1, 2, 3, 4, 5];
// 배열 합 구한다.
var sum = 0;
a.forEach(function (value) {
  sum += value;
});
console.log(sum); // 15
// 각 배열 요소의 제곱을 구한다.
a.forEach(function (v, i, a) {
  a[i] = v * v;
});
console.log(a); // [1, 4, 9, 16, 25];
```

**map**

인수로 받은 함수를 배열의 요소로 한번씩 실행하며, 마지막엔 그 함수가 반환한 값으로 새로운 배열을 생성합니다. 인수로 넘긴 함수에는 인수 세개가 전달되며, 인수로 넘긴 함수는 반드시 값을 반환해야 합니다.

```javascript
배열의 각 요소를 두 배 곱한 배열로 생성하기

var a = [1, 2, 3, 4, 5];
var b = a.map(function (x) {
  return 2 * x;
});
// b = [2, 4, 6, 8, 10]

배열의 요소들을 제곱근한 배열로 생성하기

var a = [1, 4, 9, 16, 25];
var b = a.map(Math.sqrt);
// b = [1, 2, 3, 4, 5]
```

다음 코드는 객체 배열의 요소를 순회합니다. 이때 각 객체가 가진 특정한 프로퍼티 값을 꺼내 배열로 만듭니다.(화살표함수 사용)

```javascript
var persons = [
  { name: "Tom", age: 17 },
  { name: "Huck", age: 18 },
  { name: "Becky", age: 16 },
];
var names = persons.map((person) => person.name);
var ages = persons.map((person) => person.age);
console.log(names); // ["Tom", "Huck", "Becky"]
console.log(ages); // [17, 18, 16]
```

map메서드 의 반환값은 원본배열과 같은 개수의 원소가 들어있는 배열입니다. 따라서 map메서드 의 반환값에 Array.prototype의 메서드를 메서드체인으로 연결해 처리할 수 있습니다.

예를 들어 앞의 persons 객체 배열을 대상으로 '이름을 배열로 만든 후 이름 별로 문자의 개수를 구하라'는 요구사항을 다음과 같이 구현할 수 있습니다.

```javascript
persons.map((person) => person.name).map((name) => name.length);
// [3, 4, 5]
```

**reduce**

배열의 첫번째 요소부터 마지막 요소까지의 합성 곱(convolution)처리합니다.

합성곱 처리란 배열 요소 하나를 함수로 처리한 후 그 반환값을 다음번 요소를 처리할 때 함수의 입력값으로 사용하는 처리방법을 말합니다.

reduce메서드는 마지막 요소를 처리한 함수가 값을 반환합니다.

reduce메서드의 인수는 다음과 같습니다.

- callback: 합성곱을 하는 함수
- initial: callback이 처음 호출되었을 때 첫번째 인수의 값(생략가능)

callback함수는 다음과 같은 인수를 받습니다.

- prev: 이전 요소를 처리한 함수의 반환값 또는 initial 또는 첫번째 요소의 값
- value: 현재 처리하는 배열 요소의 값
- index: 현재 처리하는 배열 요소의 인덱스
- array: 메서드를 적용 중인 배열의 참조

초깃값 initial 지정여부에 따라 callback이 처음 호출될때 인수로 들어오는 세 값이 다음과 같이 바뀝니다.

- initial 지정함: prev는 initial값, value는 배열의 첫번째요소, index는 0
- initial 지정안함: prev는 배열의 첫번째 요소값, value는 배열의 두번째요소값, index는 1

다음 코드는 reduce메서드로 배열요소의 합을 구하는 예입니다.

```javascript
var a = [1, 2, 3, 4, 5];
a.reduce(function(prev. value){
    return prev + value;}, 0);
    // 15

a.reduce(function(prev, value){
    return prev + value
});
    // 15

첫번째 reduce메서드 통한 코드는 인수 initial을 지정했고,
두번째 reduce메서드 통한 코드는 initial 지정하지 않았습니다.
```

> reduce() 는 배열을 순회하며 인덱스 데이터를 줄여가며 어떠한 기능을 수행 할 수 있는 함수

```javascript
let arr = [1, 2, 3, 4, 5]

// prev: 이전값. 즉 현재까지 누적된 값(누산값)
// cur : 현재값

const result = arr.reduce((prev, cur)=>{
  return prev + cur;
	}, 0) //초기값을 0으로 설정한 것. 선택사항임. 안쓰면 첫번째요소가 들어가게됨.


처음: return prev:0 cur:1 // 한바퀴 돌아서
두번째: return prev:1 cur: 2
세번째: return prev:3(이전 누산값 1에서 2 더했으니까) cur:3
네번째: return prev:6 cur:4
다섯번째: return prev:10 cur:5
여섯번째: return prev:15
-----
  만약 초기값을 100으로 한다면? 100부터 시작해 다 더하니까 115가 될 것.

```

reduce()의 실용 예제:

```javascript
let userList: [
  { name: "Mike", age: 30 },
  { name: "Tom", age: 10 },
  { name: "Jane", age: 27 },
  { name: "Sue", age: 26 },
  { name: "Harry", age: 42 },
  { name: "Steve", age: 60 }
]; // 여기서 성인만 배열로 골라내기

let result = userList.reduce((prev, cur) => {
  if (cur.age > 19) {
    prev.push(cur.name);
  }
  return prev;
}, []);

// 1. 초기값은 빈 배열 [] 로 만들어준다.
// 2. 현재값의 나이가 19세보다 많을 경우
// 3. 현재값의 이름을 push, 즉 배열에 추가 해주고 리턴한다.
// 4. 그렇다면 19세 미만은 if문을 만족하지 못해 걸러질 것이다.

console.log(result);
// ["Mike", "Jane", "Sue", "Harry", "Steve"]
```

만약 나이를 다 더하려면?

```javascript
let result = userList.reduce((prev, cur) => {
  return (prev += cur.age);
}, 0);
```

## ✔ 다차원 배열

자바스크립트는 다차원 배열을 정의하기 위한 문법은 제공하지 않지만, 배열에 배열을 중첩해 다차원 배열과 비슷한 기능을 구현할 수 있습니다.

## ✔ 유사 배열 객체

자바스크립트에서는 배열은 아니지만 배열로 처리할 수 있는 객체를 사용하며, 이를 '유사 배열 객체' 라고 합니다.

자바스크립트에서 배열이란 Array타입의 객체입니다. Array 타입의 객체는 다음과 같은 성질이 있습니다.

1. 0 이상의 정수 값을 프로퍼티 이름으로 갖는다.
2. length 프로퍼티가 있으며, 요소를 추가/삭제하면 length프로퍼티 값이 바뀐다. 또한 length 프로퍼티 값을 줄이면 그에 따라 배열 크기가 줄어든다.
3. 프로토타입이 Array.prototype 이므로 Array.prototype의 메서드를 상속받아 사용할 수 있다. 또한 instanceOf 연산자로 평가하면 Array 생성자 함수로 생성된 객체로 표시된다.

이러한 성질 중 프로퍼티 이름이 0 이상의 정수이며, length 프로퍼티가 있는 객체는 대부분 배열로 다룰 수 있고 이러한 객체를 '유사 배열 객체' 라고 합니다.

유사배열객체는 다음과 같은 방법으로 직접 생성할 수 있습니다.

```javascript
//  유사 배열 객체를 생성해서 값을 대입한다.
var a = {};
for (var i = 0; i < 10; i++) {
  a[i] = i;
}
a.length = 10;
//  유사 배열 객체의 요소 합을 구한다.
for (var i = 0, sum = 0; i < a.length; i++) sum += a[i];
console.log(sum); // 45
```

유사배열객체는 Array.prototype의 메서드를 사용할 수 없습니다. 그러나 배열로 참조/대입할 수 있으며, for문이나 for/in 문으로 반복 처리할 수 있습니다. 그러나 요소의 추가/삭제 또는 length 프로퍼티값을 요수의 개수와 연계하는 등의 처리는 배열처럼 동작하지 않습니다.

### Array.prototype의 메서드를 유사 배열 객체에서 사용하기

Function.prototype.call 메서드로 간접 호출하면 Array.prototype의 메서드를 사용할 수 있습니다.

```javascript
var a = { 0: "A", 1: "B", 2: "C", length: 3 };
Array.prototype.join.call(a, ","); // "A, B, C"
Array.prototype.push.call(a, "D");
//  Object {0: "A", 1: "B", 2: "C", 3: "D", length: 4}
Array.prototype.slice.call(a, 0); //  ["A", "B", "C", "D"] : 진짜 배열로 변환
var a = { 0: 1, 1: 2, 2: 3, length: 3 };
Array.prototype.map.call(a, function (v) {
  return v * v;
});
//  [1, 4, 9]
```

이처럼 Array.prototype의 메서드를 유사배열객체에 적용할 수는 있지만, concat메서드를 제외한 나머지 배열 메서드는 배열처럼 작동하지 않습니다.

```javascript
var a = { 0: "A", 1: "B", 2: "C", length: 3 };
Array.prototype.concat.call(a, ["D", "E"]);
//  [{ 0: "A", 1: "B", 2: "C", length: 3 }, "D", "E"]
```

## ✔ ECMAScript 6 의 배열과 새롭게 추가된 기능

### 비구조화 할당

비구조화 할당은 배열, 객체, 반복가능객체 에서 값을 꺼내 그 값을 별도의 변수에 대입하는 문장입니다.

- 배열의 비구조화 할당

1. 기본 사용법

```javascript
var [a, b] = [1, 2]; // var a = 1, b = 2 와 같음
```

이 문장을 실행하면

변수 a와 b를 선언한 후 우변의 배열에서 요소를 하나씩 꺼내 인덱스 순서대로 a, b에 대입합니다. 우변의 배열을 분할해 좌변의 변수에 할당하므로 '분할 할당' 이라고도 합니다.

배열 리터럴과 비슷합니다. 즉, 변수를 쉼표로 구분하고 대괄호로 묶습니다.

다음 코드는 이미 선언된 변수를 비구조화 할당하는 예입니다.

```javascript
[a, b] = [2 * a, 3 * b]; // a = 2*a, b = 3*b 와 같음
[a, b] = [b, a]; // a 값과 b 값을 교환함
```

이때 우변값의 개수와 좌변 변수의 개수가 같을 필요는 없습니다.

좌변 변수 개수가 우변값의 개수보다 많으면 undefined가, 반대의 경우 남은 값은 무시됩니다. 또한 변수가 없는 인덱스 값도 무시됩니다.

```javascript
[a, b, c] = [1, 2]; // a = 1, b = 2, c = undefined와 같음
[a, b] = [1, 2, 3]; // a= 1, b = 2와 같음. 3은 무시됨
[, a, , b] = [1, 2, 3, 4]; // a = 2, b = 4 와 같음
```

배열 비구조화 할당 표현식의 값은 우변 값이 됩니다.

```javascript
var array, first, second;
array = [first, second] = [1, 2, 3, 4];
// first = 1, second = 2, array = [1, 2, 3, 4] 와 같음
```

2. 나머지 요소

베열의 비구조화 할당을 할 때는 함수의 나머지 매개변수(함수, 319쪽)와 마찬가지로 전개연산자인 ... 을 사용해 나머지요소를 이용할 수 있습니다.

```javascript
[a, b, ...rest] = [1, 2, 3, 4]; // a = 2, b = 2, rest = [3, 4] 와 같음
```

좌변의 ...rest 부분이 나머지 요소이며, 변수 rest에는 할당되지 않은 우변의 남은 요소들이 배열로 할당됩니다.

3. 요소의 기본값

배열의 비구조화 할당을 할 때는 함수의 인수와 마찬가지로 기본값을 설정할 수 있습니다. 비구조화 할당하는 좌변의 변수에 undefined가 할당되면 undefined 대신 기본값을 할당합니다.

```javascript
[a = 0, b = 1, c = 2] = [1, 2]; // a = 1, b = 2, c = 2와 같음
```

4. 함수가 배열로 반환한 값을 비구조화 할당받기

함수가 값을 여러개 반환해야 하면 그 값을 배열로 반환하도록 만들 수 있다. 비구조화 할당으로 더 간결하게 표현할 수 있다.

---

- 객체의 비구조화 할당

1. 기본적인 사용법

객체도 비구조화 할당을 할 수 있습니다. 좌변은 객체 리터럴과 비슷한 문법을 사용합니다.

프로퍼티를 쉼표로 구분, 중괄호로 묶어줍니다. 이 프로퍼티 이름은 우변의 프로퍼티 이름이며 프로퍼티 값으로는 임의의 변수를 사용할 수 있습니다.

```javascript
var { a: x, b: y } = { a: 1, b: 2 }; // x = 1, y = 2와 같음
```

이렇게 하면 좌변에 변수 x와 y가 선언되며, 각각 우변의 a 프로퍼티 값과 b 프로퍼티 값이 할당됩니다. 다음 코드는 이미 선언된 변수를 비구조화할당하는 예입니다.

```javascript
{a: x, b: y} = {a: y, b: x};  // x 값과 y 값을 교환한다.
```

좌변의 변수에 호응하는 프로퍼티 이름이 오른쪽에 없으면 그 변수엔 undefined가 할당됩니다.

```javascript
{a: x, b: y} = {a: 1, c: 2};  // x = 1, y = undefined와 같음
```

우변에 값이 있지만 그에 대응하는 이름의 변수가 좌변에 없으면 무시됩니다.

```javascript
{a: x, b: y} = {a: 1, b:2, c: 3}; // x = 1, y = 2 와 같음. 3은 무시됨
```

2. 프로퍼티의 기본값

배열의 비구조화 할당을 할 땐 함수의 인수와 마찬가지로 기본값을 설정할 수 있습니다. 좌변의 변수에 undefined가 할당되면 그 대신 기본값을 할당합니다.

```javascript
{a: x=1, b: y=2, c: z=3} = {a: 2, b: 4};  // x = 2, y = 4, z = 3 과 같음
```

3. 프로퍼티 이름 생략하기

좌변에는 변수 이름만 쉼표로 구분해 작성할 수 있습니다. 이때는 프로퍼티 이름이 변수의 이름이 됩니다.

```javascript
{a, b} = {a: 1, b: 2};  // {a: a, b: b} = {a: 1, b: 2}와 같음

var {sin, cos, tan, PI} = Math;
// var sin = Math.sin, cos = Math.cos, tan = Math.tan, PI = Math.PI 와 같음
```

프로퍼티 이름을 생략한 상태에서도 기본값을 지정할 수 있습니다.

```javascript
{a=1, b=2, c=3} = {a: 2, b: 4}; // a = 2, b = 4, c = 3과 같음
```

---

- 반복 가능한 객체의 비구조화 할당

우변에 반복가능한(이터러블한) 객체가 있을 때도 비구조화 할당을 할 수 있습니다. 좌변에는 배열 리터럴과 비슷한 문법을 사용합니다.

```javascript
var [a, b, c] = "ABC"; // var a ="A", b = "B", c = "C" 와 같음
function* createNumbers(from, to) {
  while (from <= to) yield from++;
}
var [a, b, c, d, e] = createNumbers(10, 15);
// a = 10, b = 11, c = 12, d = 13, e = 14 와 같음
```

---

- 중첩된 자료 구조의 비구조화 할당

중첩된 객체나 배열에도 비구조화 할당을 적용할 수 있습니다.

```javascript
var [a, [b, c]] = [1, [2, 3]]; // var a = 1, b = 2, c = 3 과 같음
var {
  a: x,
  b: { c: y, d: z },
} = { a: 1, b: { c: 2, d: 3 } };
// var x = 1, y = 2, z = 3 과 같음
var person = { name: "Tom", age: 17, hobby: ["Tennis", "Music"] };
var {
  name,
  age,
  hobby: [hobby1],
} = person;
// var name = "Tom", age = 17, hobby1 = "Tennis" 와 같음
```

---

### 전개 연산자

...은 전개 연산자라고 합니다. 반복가능한(이터러블한)객체(322쪽)를 반환하는 표현식 앞에 표기하며, 이를 통해 반복 가능한 객체를 배열 리터럴 또는 함수의 인수 목록으로 펼칠 수 있습니다.

```javascript
[... "ABC"]   // ["A", "B", "C"]

[1, ... [2, 3, 4], 5]   // [1, 2, 3, 4, 5]

f(...[1, 2, 3])   // f(1, 2, 3) 과 같음
```

다음 코드는 제너레이터가 만든 이터레이터를 배열 리터럴 안에 펼치는 예입니다.

```javascript
function* createNumbers(from, to) {
  while (from <= to) yield from++;
}
var iter = createNumbers(10, 15);
[...iter]; // [10, 11, 12, 13, 14, 15]
```

배열 두개를 연결할 때는 보통 Array.prototype.concat 메서드를 사용하지만 전개 연산자를 사용하면 Array.prototype.push 메서드로도 연결할 수 있습니다.

```javascript
var a = ["A", "B", "C"];
a.push(...["D", "E"]); // ["A", "B", "C", "D", "E"]
```

다음 코드는 배열 안의 최댓값을 Math.max 로 구합니다.

```javascript
var a = [5, 2, 3, 7, 1];
Math.max(...a); // 7
```

---

### ArrayBuffer와 형식화 배열

ArrayBuffer, DataView, 형식화 배열(TypedArray)은 연속된 데이터 영역(버퍼)을 조작하기 위한 객체입니다. 배열과 이미지 데이터를 빠르게 읽고 쓸 수 있습니다.
ArrayBuffer는 버퍼를 확보하며, 형식화 배열은 버퍼에 뷰(읽고 쓰기)를 제공합니다.

---

### Map

Map 객체는 데이터를 수집하여 활용하기 위한 객체이며, '키'와 값을 한 쌍으로 객체 안에 저장해서 사용합니다.

Map 객체는 외부에서 키를 사용해 원하는 값을 추가/삭제/검색할 수 있으며, 키와 값의 데이터 타입은 제한이 없습니다.

Object 객체도 프로퍼티가 모여 만들어졌기 때문에 Map 객체와 비슷해보이지만 다음과 같은 차이점이 있습니다.

- Map 객체에는 데이터 수집 위한 다양한 메서드 존재
- Map 객체는 Object객체와 달리 키 타입에 제한이 없음(Object객체는 문자열만 사용 가능)
- Map 객체는 반복가능(이터러블)하며 for/of문으로 순회하면 키와 값으로 구성된 배열 반환
- Map 객체는 데이터 개수를 size 프로퍼티로 구할 수 있다(Object객체는 수동으로 계산해야함)

Map 객체는 생성자 함수로 만들며, 인수를 지정하지 않으면 데이터 없는 빈 Map객체가 생성됩니다.

```javascript
var map = new Map();
console.log(map); // Map{}
```

Map 객체는 Map.prototype의 프로퍼티와 메서드를 상속받습니다.(423쪽 참고)

Map 객체에 데이터를 추가할 땐 set(key, value)메서드를 사용합니다. 이미 키 값이 가리키는 데이터가 있다면 덮어씁니다.

---

### Set

Set 객체는 중복되지 않는 유일한 데이터를 수집해 활용하기 위한 객체입니다. Set 객체는 데이터 값의 단순집합으로 간주하며, 외부에서 키를 사용해 데이터값을 추가/삭제/검색할 수 있습니다. Map 객체와 마찬가지로 데이터 타입에는 제한이 없습니다.

Set 객체의 생성은 Map객체와 같은 방식을 가집니다.

```javascript
var set = new Set();
console.log(set); // Set {}
```

Set객체에서의 값 동일성은 일치연산자(===)가 정의하는 동일성과 약간 다릅니다. 다시 말해, Set 객체에서는 NaN과 NaN이 같으며, +0과 -0이 같습니다.

Set 객체는 Set.prototype의 프로퍼티와 메서드를 상속받습니다(429쪽 참고)

Set객체에 데이터를 추가할 땐 add(value)메서드를 사용합니다.
