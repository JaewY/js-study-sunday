## 변수 
    - 값(데이터)을 담기 위해 이름 붙인 상자
    - 변수는 어떤 정보에 이름을 붙여서 저장하고 싶을 때 사용함. 이때, 컴퓨터 메모리 공간에 일정한 크기로 생성됨

## 변수 선언
    - 선언자를 사용하여 변수 이름을 선언
    - 선언자 종류: var, let, const

   구분 | 재선언 | 재할당 | 참고 |
   ----- | ----- | ----- | -----
   var | O | O | | 
   let | X | O | let 재항당: let을 제외하고 작성 |
   const | X | X | 절대로 바뀌지 않는 상수(파이, 생일, 최댓값 등)를 선언할 때 사용 |


    *TIP: 모든 변수를 const로 선언하고 나중에 변경될 여지가 있는 변수들만 let으로 바꾸면됨
    
    *참고

    = (대입 연산자) : 오른쪽 값을 왼쪽 변수에 대입한다는 뜻

    == (일치 연산자) : 5 == '5' //true

    === (동등 연산자) :  5 === '5' //false
             
                         5 === 5 //true


## 변수 선언 생략
     - var로 선언하지 않은 변수 값을 읽으려고 시도하면 참조 오류 발생
     - var문으로 선언하지 않은 변수에 값을 대입할 때는 오류가 발생하지 않음 

        console.log(x); // ReferenceError : x is not defined
    
    
        x = 2;
        console.log(x); // 2 
 
 
    변수를 선언하지 않은 상태에서 값을 대입하면 자바스크립트 엔진이 그 변수를 자동으로 전역 변수로 선언하기 때문
    그러나 변수를 선언하지 않고 변수를 사용하는 행위는 버그의 원인 될 수 있음.
    따라서 변수는 반드시 선언하고 사용해야 한다.

## 변수 끌어올림(호이스팅, hoisting)
    - 프로그램은 작성한 순서에 따라 윗줄부터 차례대로 실행됨 but 변수 선언은 이 원칙을 따르지 않음
    - 변수 선언의 끌어올림은 다른 언어에는 없는 자바스크립트만의 고유한특징

    console.log(x); // → undefined

    var x;


    console.log(x); // → undefined

    var x = 5;

    console.log(x); // → 5


## 변수의 명명 규칙
    1. 사용 가능 문자: 유니코드 문자, 숫자(0~9), 밑줄(_), 달러 기호($)
      * 문자 중 기본적으로 영어단어 사용
      
    2. 첫 글자에 숫자 사용 X
    
    3. 예약어를 변수로 사용 X
    
    4. 가급적 상수는 대문자로 사용
    
    5. 변수가 어떤 정보를 가지고 있는지 유추하기 쉽도록
    

    + 루프 카운터 변수(7장) 이름으로는 i,j,k 등을 사용
    + 논리값(3.2.5절)을 표현하는 변수에는 이름 앞에 is를 붙임 isMouseDown
    + 생성자(4.3절) 이름을 붙일 때는 파스칼 표기법을 사용
    
    
    식별자 명명 규칙에 따라 자유롭게 지정 가능 but 협업 및 원활한 프로그래밍을 위해 
    일정한 표기법(일반적으로 세가지)에 따라 변수의 의미를 알 수 있도록 설정할 것
   - 캐멀 표기법(로어 캐멀 표기법)
    
           두 번째 이후 단어의 첫 글자를 대문자로 표기하고 나머지는 소문자로표기

           Ex) newName createLifeGame
   
   - 파스칼 표기법(어퍼 캐멀 표기법)
   
           각 단어의 첫 글자를 대문자로 표기하고 나머지는 소문자로 표기

           Ex) NewNAme  CreateLifeGame

   - 밑줄 표기법(스네이크 표기법)
   
           모든 단어를 소문자로 표기하고 단어와 단어를 밑줄(_)로 구분

           Ex) new_name  create_life_game
           
           
 ## 예약어
    - 자바스크립트 문법을 규정짓기 위해 자바스크립트 언어 사양에서 사용하는 특수한 키워드
   
   - ECMAScript 6 기준
   
   break | case | catch | class | const | continue |
   ----- | ----- | ----- | ----- | ----- | ----- |
   dubugger | default | delete | do | else | export |
   extends | false | finally | for | function | if |
   import| in | instanceof | new | null | return |
   super | switch | this | throw | true | try |
   typeof | var | void | while | with | yield |
   
  - 현재는 예약어가 아니지만 ECMAScript 확장을 위해 예약된 키워드 

   await | enum | implements | package | 
   ----- | ----- | ----- | ----- | 
   protected | interface | private | public | 

  - 미리 정의된 전역 함수

   arguments | Array | Boolean | Date | 
   ----- | ----- | ----- | ----- | 
   decodeURI | decodeURIComponent | encodeURI | encodeURIComponent | 
   Error | eval | EvalError | Function |
   Infinity | inFinite | isNaN | JSON |
   Math | NaN | Number | Object |
   parseFloat | parseInt | RangeError | RefferenceError |
   RegExp | String | SyntaxError | TypeError |
   undefined | URIError | | |


