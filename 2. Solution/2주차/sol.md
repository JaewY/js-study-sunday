🤷‍♂️ 
앞서 함수 안에서 변수의 블록 유효범위를 공부하다가 아래 let 문의 경우,   
var 문으로 선언한 변수를 읽으려고 시도할때 오류가 발생하지 않는것과 대조적인것을 보고 의문점이 들었다.
```javascript
console.log(x) // ReferenceError: x is not defined
let x = 5
```
모던자바스크립트입문 교재에서 TDZ 때문이라고 나와있는데, 이해가 잘 가지 않았다. 일단 TDZ 정의를 보고 포스팅을 내려가면서 TDZ에 대해 이해해보자.
# TDZ(Temporal Dead Zone) ?
- 스코프의 시작 지점부터 초기화 시작 지점까지의 구간을 TDZ(Temporal Dead Zone) = 일시적인 사각지대라고 한다.
> 스코프(Scope) : '변수에 접근할 수 있는 범위' ; global(전역) local(지역)

<br>

## 변수 선언의 3단계
<p align="center"><img width="30%" src="https://user-images.githubusercontent.com/76654131/138394994-39408b4b-068d-4532-9f68-7f5995aecb35.png"></p>

- 선언 단계(Declaration phase) : 변수를 실행 컨텍스트의 변수 객체에 등록하는 단계를 의미한다. 이 변수 객체는 스코프가 참조하는 대상이 된다.
- 초기화 단계(Initialization phase) : 실행 컨텍스트에 존재 하는 변수 객체에 선언 단계의 변수를 위한 메모리를 만드는 단계. 이 단계에서 할당된 메모리에는 undefined로 초기화 된다.
- 할당 단계(Assignment phase) : 사용자가 undefined로 초기화된 메모리의 다른 값을 할당하는 단계.

> 실행 컨텍스트(Execution Context)는 scope, hoisting, this, function, closure 등의 동작원리를 담고 있는 자바스크립트의 핵심원리이다.   
좀 더 쉽게 말하자면 실행 컨텍스트는 실행 가능한 코드가 실행되기 위해 필요한 환경... 이라는데 솔직히 이해가 잘 안가서 나중에 따로 정리!  [참고](https://poiemaweb.com/js-execution-context)

🔎 지금까지 아무 생각없이 var let const를 사용했는데, 위처럼 3가지 단계를 거쳐서 생성되는 것을 알았다.

## var 변수 lifecycle
<p align="center"><img width="50%" src="https://user-images.githubusercontent.com/76654131/138396433-1c4dac06-0098-451e-8b03-19baf5d2f4e9.png">
</p>

- var 같은 경우 선언과 동시에 undefined라는 값으로 초기화가 된다. 즉, 선언 단계와 초기화 단계를 동시에 진행
- 그렇기 때문에 변수를 선언하기 전에 호출을 해도 undefined로 호출이 되는 호이스팅이 발생!

```javascript
console.log(x) // undefined
var x = 5
```

## let(const) 변수 lifecycle
<p align="center"><img width="50%" src="https://user-images.githubusercontent.com/76654131/138398124-93fd95dc-fb4c-4315-bff8-e7ba22661832.png"></p>

- let , const 변수들도 실행컨텍스트 생성단계에서 메모리에 매핑이 일어나면서 호이스팅이 일어나지만 var 변수와 달리 초기화단계가 일어나지 않는다.
- 그래서 실행 컨텍스트에 변수를 등록했지만, 메모리가 할당이 되질 않아 접근할 수 없어 참조 에러(ReferenceError)가 발생하는 것이었다.   
나는 지금까지 이런것을 모르고, 그냥 호이스팅이 되지 않는구나라고 오해를 했던것이다.

🔥 즉, let const 또한 선언단계에서 실행 컨텍스트 변수 객체에 등록이 되어 호이스팅이 되지만,   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TDZ 구간에 의해 메모리가 할당이 되질 않아 참조 에러(ReferenceError) 발생하는 것이다.
   
<br>
<br>

**Reference**   
본 포스팅은 아래 사이트를 참조 및 인용하여 개인공부 용도로 작성되었습니다.   
잘못된 내용 피드백 주시면 반영하겠습니다. 감사합니다.   
[https://noogoonaa.tistory.com/78](https://noogoonaa.tistory.com/78)   
[https://caferion.netlify.app/JavaScript/variable/](https://caferion.netlify.app/JavaScript/variable/)
