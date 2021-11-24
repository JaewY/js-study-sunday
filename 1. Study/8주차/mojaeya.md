# 배열

## 배열의 메서드 

**배열은 Array 타입 객체이며 Array.prototype의 프로퍼티를 상속 받는다.   
Array.prototype에는 수많은 메서드가 정의되어 있으며, 모든 배열은 이 메서드를 사용할 수 있다.**

## **수정 메서드** ( _원본 배열을 바로 수정_ )

****▶** push 메서드** : 배열 마지막에 하나 이상의 요소를 추가한 다음 그 배열의 길이를 반환

```
const fruits = ['🥝', '🍌']

fruits.push('🍎','🍉')  // 반환값 : 4
console.log(fruits)     // fruits : ['🥝', '🍌','🍎','🍉']
```

****▶** pop** **메서드** : 배열의 마지막 요소를 잘라내어 반환

```
fruits.pop()        // 반환값 : '🍉'
console.log(fruits) // fruits : ['🥝', '🍌','🍎']
```

****▶** unshift 메서드** : 배열 앞부분에 요소를 추가 후 모든 배열 요소를 오른쪽으로 이동한 다음 그 배열의 길이를 반환

```
fruits.unshift('🍋')  // 반환값 : 4
console.log(fruits)   // fruits : ['🍋','🥝', '🍌','🍎']
```

****▶** shift** **메서드** : 배열 첫번째 요소 제거 후 모든 배열 요소 왼쪽으로 이동

```
fruits.shift()       // 반환값 : '🍋'
console.log(fruits)  // fruits : ['🥝', '🍌','🍎']
```

> **note!! unshift, shift are slower than push, pop : 배열을 움직여야 되기 때문!**

****▶** splice 메서드** : 특정 인덱스의 배열 요소를 갈아 끼울 때 사용하는 메서드(요소를 끼워넣기만, 삭제만 하는것도 가능)

```
const fruits = ['🥝', '🍌','🍎','🍉']
// 첫번째 인수 : 배열을 수정하기 시작할 위치 
// 첫번째 인수만 넘기면 그 인덱스 이후에 있는 모든 배열 요소를 삭제
fruits.splice(1)     // 반환값 : '🍌','🍎','🍉'
console.log(fruits)  // fruits : ['🥝']

const fruits2 = ['🥝', '🍌','🍎','🍉']
// 두번째 인수 : 배열에서 삭제할 요소의 개수
fruits2.splice(1, 1)   // 반환값 : '🍌'
console.log(fruits2)   // fruits2 : ['🥝','🍎','🍉']

const fruits3 = ['🥝', '🍌','🍎','🍉']
// 세번째 인수 : 배열에 삽입할 요소의 값을 쉼표로 구분해서 넘김
fruits3.splice(1, 1, '🍒','🍊')   // 반환값 : '🍌'
console.log(fruits3)              // fruits3 : ['🥝','🍎','🍉','🍒','🍊']
```

****▶** sort 메서드** : 배열 안의 요소를 정렬 (인수로는 실제로 담담하는 함수의 참조를 넘기며 반환값은 정렬된 배열이다)

```
const a = [5,2,7,1,3,9,8]

a.sort(funtion(a,b) {return a-b})  // 반환값 : [1,2,3,5,7,8,9]
console.log(a)                     // a : [1,2,3,5,7,8,9]
```

비교함수는 배열안의 인접한 요소를 비교하는 역할을 한다. 비교함수는 인수를 두개 받고, 첫번째 인수는 인전합 왼쪽 요소,

두번째 인수는 인접한 오른쪽 요소이다. 비교함수를 f(a, b)라고 했을 때 비교함수는 다음 규칙을 따른다.

-   f(a, b) < 0 이면 a를 b보다 작은 인덱스로 정렬한다.
-   f(a, b) == 0 이면 a와 b의 순서를 바꾸지 않는다.
-   f(a, b) > 0 이면 b를 a보다 작은 인덱스로 정렬한다.

****▶** reverse 메서드**

```
const array = [1, 2, 3, 4, 5];

array.reverse()  // [5, 4, 3, 2, 1]
```

---

## **접근자 메서드** ( 배열을 다른 모습으로 가공한 새로운 배열 반환,  원래 배열 수정 X )

****▶** join 메서드** : 배열의 모든 요소 값을 문자열로 바꾼 후에 인수로 받은 문자로 연결해서 반환.

                     요소값이 undefined나 null일 때는 그 요소값을 빈문자로 간주.

```
const fruits = ['apple', 'banana', 'orange']

fruits.join("-")     // 'apple-banana-orange'

// 빈 문자를 지정하면 배열 요소의 모든값을 그대로 연결.
fruits.join("")    // 'applebananaorange'

// 인수를 지정하지 않으면 쉼표로 배열의 요소 값을 연결해 반환.
fruits.join()     // 'apple,banana,orange'
```

****▶** concat 메서드** : 인수로 받은 값을 그 배열의 요소로 추가해서 새로운 배열을 생성. 받은 인수가 배열이면 펼친후에 배열에 추가

```
const a = ['A', 'B', 'C']

a.concat(['D','E'])   // ['A', 'B', 'C', 'D', 'E']

// 배열은 한번만 펼처서 추가한다.(배열을 재귀적으로 펼치지 않는다)
a.concat('D', ['E',['F','G']])   // ['A', 'B', 'C', 'D', 'E', ['F','G']]
```

concat 메서드는 인수값이 객체의 참조면 그 참조값을 복사한다.

따라서 원본 객체를 수정하면 concat 메서드가 반환한 배열의 요소도 함께 바뀐다.

****▶** slice 메서드** : 배열의 일부 요소를 제거한 새로운 배열을 반환

첫번째 인수(**begin**) : 요소를 꺼낼 시작위치를 뜻하는 인덱스

두번째 인수(**end**) : 요소를 꺼낼 마지막 위치를 뜻한 인덱스 ( slice 메서드는 end가 가리키는 요소의 바로 이전 요소까지만 잘라낸다)

```
const array = [1, 2, 3, 4, 5]

array.slice(2,5)    // [3, 4, 5]

// 두번째 인수인 end를 생략하면 마지막 요소까지 잘라낸다.
array.slice(3)      // [4, 5]

array.slice()    // [1, 2, 3, 4, 5]
```

****▶** indexOf 와 lasstIndexOf 메서드** : 배열 안에서 인수로 지정한 값을 검색해서 가장 먼저 찾은 요소의 인덱스를 반환.

                                                                   (찾지 못한 경우 -1 반환)

```
let a = ['A', 'B', 'C', 'C', 'D']

// 인덱스 앞에서부터
a.indexOf('C')           // 2

// 인덱스 뒤에서부터
a.lastIndexOf('C')       // 3

// 두번째 인수 : 검색을 시작할 인덱스
a.indexOf('C', 3)        // 3

// includes 메소드 : 인수로 지정한값이 배열에 포함되어 있는지 확인, 있으면 true 없으면 false로 반환 
a.includes('F')         // false
```

****▶** toString과 toLocaleString 메서드** : 배열의 요소를 문자열로 변환하여 쉼표로 연결한 문자열을 반환

```
const date = new Date()

console.log(['A', 'B', 'C', date].toString())  // 'A, B, C, Wed Jan 03 2018...'

// toLocalString : 해당 지역에 맞는 언어로 번역한 문자열 반환
console.log(['A', 'B', 'C', date].toLocaleString())  // 'A, B, C, 2018. 1. 3. 오후 ...'
```

****▶** filter 메서드** : 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환합니다.

```
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present']

const result = words.filter(word => word.length > 6)

console.log(result) // ["exuberant", "destruction", "present"]
```

****▶** find 메서드** : 주어진 판별 함수를 만족하는 첫번째 요소의 값을 반환합니다. 그런 요소가 없다면 undefined를 반환합니다.

```
const array1 = [5, 12, 8, 130, 44]

const found = array1.find(element => element > 10)

console.log(found) // 12
```

****▶** some 메서드** : 배열 안의 어떤 요소라도 주어진 판별 함수를 통과하는지 테스트합니다**. (하나라도 통과하면 true)**

****▶** every 메서드** : 배열 안의 **모든** 요소가 주어진 판별 함수를 통과하는지 테스트합니다. Boolean 값을 반환합니다.

```
// some 메서드
const array = [1, 2, 3, 4, 5];

const even = (element) => element % 2 === 0

console.log(array.some(even)) // true

// every 메서드
const array2 = [1, 30, 39, 29, 10, 13]

const even = (element) => element < 40

console.log(array2.every(even))  // true
```

---

## **반복 메서드** : 배열의 모든 요소를 순회하며 특정한 작업을 수행하는 메소드

**forEach(반복 메서드), for..in(키값 출력 반복문) 처럼 기존 for문 반복문을 좀 더 편하게 쓰려고 시도를 했지만 효율적이지 않았다.**

**그래서 ES6부터 추가된 효율적인 반복문 for..of를 쓰는것을 권장한다.**

> let years = \[2001, 2010,2015, 2018\];

위와 같은 배열이 있을 때

****▶** forEach 메서드**

```
years.forEach((year) => {
    console.log(year);
    // 2001, 2010, 2015, 2018
})
```

\* forEach는 배열의 내용을 출력할 수 있지만 가독성이 떨어지고 내부에서 break문 등을 사용할 수 없다. (사용권장 X)

****▶** for..of 반복문**

```
for(let year of years){
  console.log(year);

  if(year == 2001){
       break; 
  }  
  // 2001
}
```

\* for..of의 경우 배열의 내용을 출력할 수 있고 내부에서 break문도 사용 가능하다. (사용 권장)

****▶** map 메서드** : 인수로 받은 함수를 배열의 요소별로 한번씩 실행하며, 마지막에는 그 함수가 반환값으로 새로운 배열을 생성

```
class Student {
  constructor(name, age, enrolled, score) {
    this.name = name;
    this.age = age;
    this.enrolled = enrolled;
    this.score = score;
  }
}
const students = [
  new Student('A', 29, true, 45),
  new Student('B', 28, false, 80),
  new Student('C', 30, true, 90),
  new Student('D', 40, false, 66),
  new Student('E', 18, true, 88),
];
```

위에 같은 클래스와 배열이 있을때,

**Quiz) student의 score만을 포함하는 배열을 만들어라 (map 메서드 활용)**

```
const result = students.map(student => student.score)

console.log(result)  // [45, 80, 90, 66, 88]
```

**▶ reduce 메서드** : 배열의 첫번째 요소부터 마지막 요소까지의 합성곱 처리를 한다.

> **합섭 곱 처리란?**  
> **배열 요소 하나를 함수로 처리한 후에 그 반환값을 다음 번 요소를 처리할 때 함수의 입력 값으로 사용하는 처리 방법  
> **

-   **initial(초기값) 지정함** : prev는 initial의 값, curr은 배열의 첫번째 요소, index는 0
-   **initial(초기값) 지정안함** : prev는 배열의 첫번째 요소 값, curr은 배열의 두번째 요소 값, index는 1

위에서 본 클래스와 배열문을 이용해 또 문제를 하나 풀자면,

**Quiz) student의 평균 점수를 계산해라. (reduce 메서드 활용)**

```
const result = students.reduce((prev, curr) => {
    //console.log(prev)     -> reduce 메소드 이해가 잘 안가면 이렇게 로그를 직접 찍어가면서 이해해보자
    //console.log(curr)
    return  prev + curr.score
  },0)  // initial 초기값을 0으로 지정

  console.log(result / students.length)  // 369 / 5 = 73.8
```

---

## 다차원 배열과 유사배열 
#### **\[JAVA\] 2차원 배열의 선언**

```
int [][] array; // 2차원 배열의 선언

array = new int[1][5];   // 2차원 배열의 초기화
```

**but** 자바스크립트의 2차원 배열이란?

-    자바스크립트는 기본적으로 2차원 배열을 지원하지 않는다
-   const arr = \[\]\[\] 이와 같은 2차원 배열 선언이 불가능하다.
-   약간의 트릭을 이용하여 2차원 배열과 비슷한 배열을 만들 뿐이다. (배열안에 배열을 넣는 방식)

#### **\[JavaScript\] 2차원 배열의 선언**

```
// arr[5][2]    // 초기값을 할당하여 배열 생성
let arr = [['a','b'], ['c', 'd'], ['e', 'f'], ['g', 'h'], ['i', 'j']]; 



// arr[5][2]    // 반복문을 사용하여 빈 배열 생성
let arr = new Array(5);

for (let i = 0; i < arr.length; i++) {
    arr[i] = new Array(2);
}
```

## **다차원 배열  ( 2차원 배열 이상 )**

다차원 배열은 배열 내부의 요소로 배열을 추가하면 된다.

\= 배열의 요소로 다른 배열이 들어가는 것

```
let num = [10,20,['가','나','다','라'],'a','b','c']
console.log(num[1])  //  20 
console.log(num[2])  //  ['가','나','다','라']
배열 num의 2번째의 인덱스는 ['가','나','다','라'] 라는 '배열'이 '값'으로 나온다. 해당 배열의 인덱스에도 접근이 가능하다.

두번째 배열의 인덱스 값은 '배열'이 아닌 '요소'가 출력된다.
console.log(num[2][0])  //  가
```

첫번째 배열 'num'의 인덱스 값 \[2\]를 넣으면 \['가','나','다','라'\] 배열이 나오고,

첫번째 배열의 인덱스 값 옆에 두번째 배열의 인덱스 값\[0\]을 넣으면,

두번째 배열 \['가','나','다','라'\]의 0번째 인덱스 값인 '가' 출력.

_\=> 이 때 출력된 인덱스 값은 배열이 아닌 '가'라는 요소로 나온다. 이를 **다차원 배열, 중첩된 배열** 이라고 한다_

---

_**유사배열을 알아보기 전에!**_

**자바스크립트에서 배열이란?**  곧 Array 타입의 객체를 말한다. Array 타입의 객체는 다음과 같은 성질이 있다. 

-   0 이상의 정수 값을 프로퍼티 이름으로 갖는다
-   length 프로퍼티가 있으며, 요소를 추가하거나 삭제하면 length 프로터티 값이 바뀐다. 또한 length 프로퍼티 값을 줄이면 그에 따라 배열 크기가 줄어든다.
-   프로토타입이 Array.prototype 이므로 Array.prototype의 메서드를 상속 받아서 사용할 수 있다. 또한 instanceof 연산자로 평가하면 Array 생성자 함수로 생성된 객체로 표시된다. 

## 유사배열

```
let array = [1, 2, 3];
array; // [1, 2, 3]

// nodes와 els는 프론트엔드 개발하면 많이 접하는 친구들이라는데 난 아직 모르겠다.
let nodes = document.querySelectorAll('div'); // NodeList [div, div, div, div, div, ...]
let els = document.body.children; // HTMLCollection [noscript, link, div, script, ...]
```

위 예제에서 array는 배열이고, nodes와 els는 유사배열이다. 다 \[\]로 감싸져 있어서 겉만 봐서는 구분하기가 힘들다 

배열인지 판단해주는 Array.isArray 메서드를 사용해보면,

Array.isArray(array)   // true    => 직접 배열 리터럴로 선언한 array만 배열이다. // 비슷한 확인 방법 : array instanceof Array Array.isArray(nodes) // false

Array.isArray(els)       // false 

**유사배열은 배열처럼 보이지만 사실 배열의 성질 중 프로퍼티 이름 즉, key가 숫자(0이상의 정수)이고 length 프로퍼티를 가지고 있는 객체를 말한다.**  

( 참고로 string도 유사배열이다. length property를 가지며, 0부터 index로 접근할 수 있기 때문이다. )

```
let ArrayLikeObject = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3
};
```

위에 코드에 나온 객체가 **유사 배열**이다. 그래서 **유사배열 객체**라고도 부른다. ( key가 숫자고, length라는 프로퍼티도 가지고 있다. )

사실 배열도 객체라는 성질을 이용한 트릭이기 때문에 배열처럼 유사배열도

ArrayLikeObject\[0\], ArrayLikeObject\[1\], ArrayLikeObject.length 같은 것을 모두 사용 가능하다.

**but** 배열과 유사배열을 구분해야 하는 이유!  => **유사배열은 배열의 메서드(Array.prototype의 메서드)를 사용 못한다.**

그런데 유사배열도 배열의 메서드를 빌려 쓰는 방법이 있긴 하다.

바로 Function.prototype.**call 메서드**로 간접 호출하면 사용 가능하다.

```
let a = {0: 'A', 1: 'B', 2: 'C', length: 3}

Array.prototype.push.call(a, 'D')
// object {0: 'A', 1: 'B', 2: 'C', 3: 'D', length: 4}

Array.prototype.slice.call(a, 0)   // 
// ['A', 'B', 'C', 'D'] => 진짜 배열로 변환해서 반환
```

#### **ES6 부터는 Array.from() 메서드로도 가능하다.**

> **Array.from() 메서드는 유사 배열 객체(array-like object)나 반복 가능한 객체(iterable object)를 얕게 복사해  
> 새로운Array 객체를 만든다.  
> **

```
let a = {0: 1, 1: 2, 2: 3, length: 3}

Array.from(a).map(function(v) { return v*v })  // [1, 4, 9]
```

## **그럼 유사배열을 사용하는 이유는?**

어떤 함수에서 실행 결과로 배열값을 돌려주고 싶을때, 원래의 배열 객체가 가지고 있는 기능(함수)를 제공하고 싶지 않거나,

원래의 배열 객체에 없는 기능을 제공하고 싶을때 유사배열을 사용한다.

즉 원래의 Array 와 다른 배열을 사용하고 싶을때 유사배열을 이용하는 것이다.  
  

_\[\]로 감싸져 있다고 다 같은 배열이 아니라는거 명심하자!_

<br>
<br>
<br>

**Reference**

\* 본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.

잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.

[https://velog.io/@takeknowledge/javscript-ES6에-추가된-기능-간단-정리](https://velog.io/@takeknowledge/javscript-ES6%EC%97%90-%EC%B6%94%EA%B0%80%EB%90%9C-%EA%B8%B0%EB%8A%A5-%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC)

[https://www.youtube.com/watch?v=yOdAVDuHUKQ&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=8](https://www.youtube.com/watch?v=yOdAVDuHUKQ&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=8)

[https://www.youtube.com/watch?v=3CUjtKJ7PJg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=9](https://www.youtube.com/watch?v=3CUjtKJ7PJg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=9)

[https://developer.mozilla.org/ko/](https://developer.mozilla.org/ko/)

[https://www.zerocho.com/category/JavaScript/post/5af6f9e707d77a001bb579d2](https://www.zerocho.com/category/JavaScript/post/5af6f9e707d77a001bb579d2)

[https://gent.tistory.com/296](https://gent.tistory.com/296)
