
4주차 반복문 스터디 발표 후 호재님의 질문

do/while 문의 끝에는 세미콜론(;) 넣어야한다 고 되어있는데 빼면 어떻게 되나요?

빼보았지만 아무 문제가 없었습니다.

## ❔세미콜론을 뒤에 안넣어도 왜 오류가 나지 않을까요?

그래서 우선 JS에서의 세미콜론에 대해 알아보았습니다.

다른 프로그래밍언어들과 같이 자바스크립트에서 세미콜론(;)은 기본적으로 문장을 구분하기 위해 사용됩니다.
하지만 줄바꿈(개행) 혹은 한줄짜리 중괄호 { }를 사용한다면 세미콜론이 불필요합니다.

```
var i;                        // 변수 선언
i = 5;                        // 변수 할당
i = i + 1;                    // 변수 할당
i++;                          // 위와 같음
var x = 9;                    // 변수 선언+할당
var fun = function() {...};   // 변수 선언, 함수 선언 등
alert("hi");                  // 함수 호출
```

위 경우들은 세미콜론을 끝에 붙이지만 필수적이진 않습니다.

> 세미콜론이 필수적인 경우는 오직 2개 이상의 구문을 한 줄에 작성할 때입니다.

```java
var i = 0; i++; // <-- 세미콜론 필수


var i = 0; // <-- 세미콜론 선택적
i++; // <-- 세미콜론 선택적
```

중괄호{ } 뒤에는 세미콜론을 붙이지 않습니다. (`var obj={ };`와 같은 할당문은 예외) 붙인다고 해서 오류가 발생하진 않습니다.

```javascript
if  (...) {...} else {...}
for (...) {...}
while (...) {...}

// BUT:
do {...} while (...);

function (arg) { ... } // 세미콜론ㄴㄴ }
```

<br>


설령 뒤에 세미콜론을 붙여주지 않았더라도 ASI(자동세미콜론삽입)라는 자바스크립트엔진에 내장된 기능이 있어

```javascript
// 예시 1
var number = 100;
//예시 2
console.log(number);
```

뒤에 세미콜론을 안써도 잘 출력됩니다.

하지만 ASI가 있으니까 세미콜론 작성규칙을 꼭 지켜야하는가에 대한 의견 분분

```javascript
function test1 () {
    return {
        message : 'Hello World`
    }
}



function test2 ()
{
    return
    {
        message : 'Hello World'
    }
}

```

위의 예시에서 test1와 test2는 같은 결과를 출력할 것 같지만

```javascript
function test 2 ()
{
    return; // ASI가 return에 세미콜론 붙여버리면서
            // 아래의 코드는 무시
    {
        message : 'Hello World'
    }
}
```

return2 에서

ASI가 return 뒤에 자동으로 세미콜론을 삽입해주면서 undefined를 리턴하게 됩니다.

---

### ✔ 위와 같이 ASI와 같은 오류나 do while 구문( ) 뒤에 연달아 다른 코드가 작성될 수 있는 상황에 대비해서 세미콜론을 쓰지 않는거보단 쓰는 것이 오류를 범할 가능성이 낮기때문에 주의하라고 한 것 아닐까 하는 생각!

<br>

참고한 사이트들

https://www.codecademy.com/forum_questions/507f6dd09266b70200000d7e

https://programmingdigest.com/javascript-while-loop-and-do-while-loop-with-programming-examples/#JavaScript_do-while_loop

https://www.electroniclinic.com/javascript-while-loop-and-do-while-loop-with-programming-examples/#Differences_between_JavaScript_while_loop_and_JavaScript_do-while_loop

https://spiralmoon.tistory.com/entry/Javascript-%EC%84%B8%EB%AF%B8%EC%BD%9C%EB%A1%A0-%EC%9E%90%EB%8F%99-%EC%82%BD%EC%9E%85%EA%B3%BC-%EC%A4%91%EA%B4%84%ED%98%B8-%EC%9C%84%EC%B9%98-%EB%B2%84%EA%B7%B8
