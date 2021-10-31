# 제어구문

순차적 실행 흐름을 변화시키는 문장을 **제어구문** 이라고 합니다.

|  분류  |                     제어 구문                      |               설명               |
| :----: | :------------------------------------------------: | :------------------------------: |
| 조건문 |    **if/else문, switch문**, try/catch/finally문    |         조건에 따라 처리         |
| 반복문 | **while문, do/while문, for문, for/in문**, for/of문 | 조건을 만족하면 처리를 반복 실행 |
| 점프문 |     **break문, continue문**, return문, throw문     |   프로그램의 다른 위치로 이동    |

- 7장에서는 볼드 처리된 구문만 알아보겠습니다.

---

<br>
<br>

# 7.2 조건문

조건문은 조건식의 값에 따라 실행 흐름을 분기합니다.

> 분기란?
>
> > 프로그램의 실행 순서를 변경하여 다른 명령을 실행할 수 있게 하다.

<br>

## if/else 문

if/else 문은 '만약 ~이라면 ..., 그렇지 않으면...' 이라는 식의 흐름을 표현합니다.

즉 조건의 만족 여부에 따라 처리할 작업을 선택합니다.
크게 두가지 사용법이 있습니다.

<br>

> if (...) 문장: "~~하다면 ~~를 해라"

if(...) 문은 괄호 안의 표현식을 평가하고 그 표현식이 true로 평가되면 '문장'을 실행합니다.

```javascript
const a = 1;
if (a + 1 === 2) {
  console.log("a + 1 은 2 입니다.");
}
```

위 조건문은 true이기 때문에 "a + 1 은 2 입니다." 가 실행될 것입니다.

하지만 a를 0으로 바꾼다면 아무것도 출력되지 않습니다.

이렇듯 if문을 사용하면, 특정 조건이 만족 될 때에만 특정 코드를 실행 시킬 수 있습니다.

<br>

> if (...) 어쩌구 else {저쩌구}}: "~~하다면 ~~하고, 그렇지 않다면 ~~해라."

if(...) 어쩌구 else {저쩌구} 에서는 괄호 안의 표현식이 true로 평가되면 '어쩌구'를 실행하고, false로 표현되면 '저쩌구'를 실행합니다.

예제입니다.

```javascript
if (x >= 0) console.log("Positive or Zero");
else console.log("Negative");
```

특정 조건이 만족할 때와 만족하지 않을 때 각각 다른 코드를 실행해야 된다면 if-else 구문을 사용 할 수 있습니다.

> else if 문
>
> > 만약 ~ 면 .. 하고, 아니면 ... 하고, 그것도 아니면 ...해라

여러 조건에 따라 다른 작업을 해야 할 때 사용합니다.

```javascript
const a = 10;

if (a === 5) {
  console.log("5입니다!");
} else if (a === 10) {
  console.log("10입니다!");
} else {
  console.log("5도 아니고 10도 아닙니다.");
}
```

---

---

<br>

# switch 문

### switch문은 else if문으로 복잡해질 수 있는 코드를 간결하게 표현할 수 있습니다. 뿐만 아니라 switch문을 사용한 비교법은 특정 변수를 각각 다른 조건에서 사용할 수 있다는 특징이 있습니다.

<br>

switch문은 아래와 같은 문법으로 작동합니다.

```javascript

let x = '어쩌구저쩌구';

switch(x) {
  case 'value1':  // if (x === 'value1') 즉, true일 경우
    ...
    [break]

  case 'value2':  // if (x === 'value2') 즉, true일 경우
    ...
    [break]

  default:
    ...
    [break]
}
```

- 변수 x의 값이 첫번째 case 문의 값 'value1'과 일치하는지 비교한 후, 두번째 case 문의 값 'value2'와 비교합니다. 이 과정은 계속 이어집니다.

- x값과 일치하는 값을 찾을 때 해당 case문의 값을 실행합니다.

- 이때 break문을 만나거나 switch문이 끝나면 코드의 실행도 멈춥니다.

- 변수 값과 일치하는 case 문의 값을 찾지 못한다면 default 안의 문장을 실행합니다. 만약 case 문과 default 모두에서 일치하는 값을 찾지 못한다면 아무것도 발생하지 않습니다.

### 예시

```javascript
let a = 어떤 숫자;

switch (a) {
  case 3:
    console.log("비교하려는 값보다 작습니다.");
    break;
  case 4:
    console.log("비교하려는 값과 일치합니다.");
    break;
  case 5:
    console.log("비교하려는 값보다 큽니다.");
    break;
  default:
    console.log("어떤 값인지 파악이 되지 않습니다.");
}
```

- case문 안에 break문이 없으면 조건에 부합하는지 여부를 따지지 않고 이어지는 case문을 실행합니다.

  만약 break를 모두 없애고 실행하면

```javascript
//"비교하려는 값과 일치합니다."
//"비교하려는 값보다 큽니다."
//"어떤 값인지 파악이 되지 않습니다."
```

모든 케이스가 실행됩니다.

이것을 폴 스루(fall through)라고 합니다. 이 기법은 가능하면 쓰지 않는 편이 좋습니다.

- C나 Java에서는 case 뒤에 상수를 써야하지만 자바스크립트에서는 모든 형태의 표현식을 그대로 쓸 수 있습니다.

---

<br>
<br>

# 반복문

> 반복문은 특정 작업을 반복적으로 할 때 사용할 수 있는 구문입니다.

<br>

## while 문

- 조건이 맞다면 일정한 처리를 계속 반복해서 실행합니다.

```javascript
while (조건식) 문장;
```

```javascript
let i = 0;
while (i < 3) {
  console.log(i);
  i++;
}
// 0, 1, 2가 출력됩니다.
```

만약에 while문이 false 로 전환이 되지 않는다면 반복문이 끝나지 않고 영원히 반복됩니다.

---

<br>

## do/while 문

do/while문은 반복해서 실행할지를 **마지막 부분** 에서 판단합니다.

```javascript
let i = 0;
do {
  //실행할 코드
  i++;
} while (i < 10);
```

- while 반복문은 조건식을 먼저 평가하기 때문에 문장이 실행되지 않을 수 있지만 (선평가 후실행)

- do while 반복문은 문장을 먼저 실행하고 조건식을 평가하기 때문에 문장이 적어도 한번은 실행됩니다. (선실행 후평가)

<br>
while 문을 사용할 경우 조건 부분이 먼저 실행되기 때문에

```javascript
let i = 5;
while (i < 3) {
  console.log(i);
  i++;
}
//아무것도 실행되지 않습니다.
```

do/while문을 사용할 경우 조건과 상관없이 무조건 한 번은 실행됩니다.

```javascript
let i = 5;
do {
  console.log(i);
  i++;
} while (i < 3);
//최초값인 5가 실행된 후  반복문이 종료됩니다.
```

> ### while문과 달리 적어도 한 번은 실행한다는 점이 가장 큰 차이.

---

<br>

# for 문

for 문은 가장 많이 쓰이는 반복문으로, 세 부분으로 나뉘며 세미콜론(;)으로 구분합니다.

반복문의 세가지 작업(초기값 설정 / 조건 / 코드 실행 후 작업)을 한 곳에 모아 표기합니다.

```javascript
for (let i = 0; i < 10; i++) {
  //반복할 코드
}
```

<br>

```javascript
for문 예시


for (let i = 0; i < 4; i++) {
  console.log(i);

// 0, 1, 2, 3 출력
```

> > > ## 변수 선언 시, const를 쓰면 값 변경이 불가하여 에러가 발생하니 주의!

 <br>

| 구성요소  |                |                                           |
| :-------: | :------------: | :---------------------------------------: |
|   begin   |     i = 0      |       반복문에 진입할 때 한 번 실행       |
| condition |     i < 4      | 반복될때마다 조건 확인. false면 반복 멈춤 |
|   body    | console.log(i) |     condition이 true인 동안 계속 실행     |
|   step    |      i++       |      각 반복 body가 실행된 이후 실행      |

```javascript
- 쉼표 연산자를 사용해 초기화식 입력 부분에 여러 표현식을 사용할 수 있습니다.

for(var i = 1, sum = 0; i <= 10; i++) {
    sum += i;
}
```

### 구성 요소 생략하기

> 초기화식, 조건식, 반복식 모두 생략할 수 있다. but 세미콜론은 필수! (;;)

조건식을 생략하면 무한반복이 발생합니다. 때문에 break 문을 사용해
반복을 막아주어야 합니다.

```javascript
var i = 0;

for (;;) {
  if (i > 3) break;
  console.log(i);
  i++;
}

//break 문을 사용하지 않으면 무한실행됨
```

- continue 문을 통해 다음 반복문을 넘어가기

continue 는 전체 반복문을 멈추지 않습니다. 대신 조건을 통과할 때 실행중인 반복을 중단하고 다음 반복으로 넘어가게 해줍니다.

```javascript
for (let i = 0; i < 10; i++) {
  // 조건이 참이라면 남아있는 본문은 실행되지 않습니다.
  if (i % 2 == 0) continue;

  console.log(i);
}
// 1, 3, 5, 7, 9가 차례대로 출력됨
```

---

<br>

# 중첩 반복문

  <br>

> for문 안에 for 문을 작성하는 중첩 반복문

구구단이 가장 대표적인 중첩for 문 예제입니다.

```javascript
1부터 9까지 각각 9번을 반복해야 합니다.


for (var i = 2; i <= 9; i++) {
  for (var j = 1; j <= 9; j++) {
    console.log(i + "x" + j + "=" + i * j);
  }
}
/* 2x1=2
   2x2=4
   ...
   3x1=3
   3x2=6
   ...
   9x8=72
   9x9=81
```

> > 바깥 for 문의 i가 실행되고 (i=2부터 시작) 안쪽 for문의 j가 9까지 실행이 완료되고 나면 for문 종료 후 다시 바깥 for문 i가 실행됩니다.(i는 ++증감식으로 인해 3으로 시작)

<br>

---

<br>

# for/in 문 😱

> 객체에 포함된 모든 속성에 대해 반복을 실행하는 반복문

- 객체가 지니고 있는 값에 대해 반복하고 싶을 때 사용합니다.

`for (변수 in 객체 표현식) 문장`

```javascript
예시;

let Wonju = {
  job: "student",
  age: 27,
};

for (a in Wonju) {
  console.log(a);
}
//job, age 출력
//a는 Wonju가 가진 프로퍼티를 의미(a 말고 아무거나 넣어도 ㄱㅊ)

for (a in Wonju) {
  console.log(Wonju[a]); // Wonju['job'], Wonju['age']와 같음
}
//student, 27 출력
```

---

<br>
<br>

# 점프문

점프문은 프로그램의 다른 위치로 이동하는 제어 구문입니다.

자바스크립트에서 라벨로 점프할 수 있는 문장은 break 문과 continue 문입니다.

<br>

- 라벨문: 자바스크립트에서 모든 문장에 라벨을 붙일 수 있으며,

> 라벨 이름: 문장

break와 continue를 통해 반복문의 어느 위치에서 멈추고 어느 위치에서 다시 실행할지를 알려줄 수 있습니다.

## break 문

> break;

break 문은 break; 를 만나는 즉시 코드 실행을 멈추고 **반복문 자체** 를 탈출합니다. 원하는 값을 찾으면 쓸데없이 끝까지 반복문을 돌릴 필요가 없습니다.

```javascript
loop: while (true) {
  if (confirm("종료?")) break loop;
}
```

## continue 문

> continue;

continue 문은 코드 실행은 멈추지만 반복문을 탈출하지 않고 다음 반복을 수행합니다.

```javascript
for (let i = 0; i < 10; i++) {
  if (i === 2) continue; // 다음 루프를 실행
  console.log(i);
  if (i === 5) break; // 반복문을 끝내기
}
// 0, 1, 3, 4, 5 출력
```

---

앞서 설명한 구구단에서 5단을 건너뛰고 싶다면?

> ## continue를 사용하기

```javascript
for (var i = 2; i <= 9; i++) {
    if(i === 5) continue;
    for (var j = 1; j <=9; j++){
        console.log(i + "x" + j + "=" + i * j);
    }
}

/* if(i === 5) continue; 라는 조건문을 걸고 continue를 넣었습니다.
변수 i 가 5일 때는 건너뛰고 6부터 실행하라 는 의미입니다.

```

구구단 출처: https://velog.io/@khd/%EC%A4%91%EC%B2%A9-for%EB%AC%B8
