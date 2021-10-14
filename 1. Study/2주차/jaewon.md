  ## 함수
    - 인수   : 함수의 입력 값
    - 반환값 : 함수의 출력 값
    
  ## return 문
   - return 문 다음에는 줄 바꿈 문자를 넣지 말 것
   - return과 값 사이에 줄 바꿈 문자를 넣으면 js 엔진이 세미콜론을 자동으로 추가해서 해석
       
       return
       x * x;
       
        ===
        
       return;
       x * x; 
       
   ## 함수 이름
    - 해당 함수의 기능을 이해하기 쉽게
    - 일반적으로 동사 또는 동사로 시작되는 어휘
    function saveImage(img) {...}
    function getMousePosition(event) {...}
    function load_file() {...}
    
   ## 함수 호출
    - 함수 이름 뒤에 소괄호로 인수를 묶어 입력
    - 인수 : 함수를 호출할 때 전달하는 
    - 인자 : 함수 정의문의 인자
      
     *함수의 실행 흐름
      1) 인수 전달
      2) 함수 처리
      3) 반환값 리턴
        
      function square(x) {
            return x * x;
      }
      
      square(3) // 9
 
 ## 인수
    - 함수는 인수를 여러 개 받을 수 있음
    - 인수가 여러 개? → 인수, 인수 (쉼표로 구분)
   
