# 생성자와 클래스 구문
### 생성자 정의 방법 (4가지)
1. 함수 선언문
2. 함수 리터럴
4. 클래스 선언문
5. 클래스 표현식
<br>

### 생성자(constructor)란?
- 객체를 생성하는 함수를 뜻함
```javascript
 function Person(){}; //undefined
 var p0 = Person(); //undefined
 
 p0 // undefined
 ```
 비어있는 함수를 호출하면 그대로 비어있음
 ```javascript
 function Person(){}; //undefined
 var p = new Person(); //undefined
 
 p // Person {}
 ```
 그런데 비어있는 함수를 new 연산자로 호출하면 빈 객체가 생성됨
 
 <br>
 
 
 ### 생성자를 쓰는 이유는?
 - 중복을 없애기 위해! 비슷한 객체를 여러개 만들 때(ex.회원,상품정보)
 ```javascript
  function User(name, age){
    //this = {}
    this.name = name;
    this.age= age;
    //retrun this;
  }

  const User1 = new User(재원, 20);
  const User2 = new User(호재, 21);
  const User3 = new User(원주, 21);
 ```
 <br>
 
 
### 생성자의 특징은?
- 객체리터럴을 이용하는 것보다 훨씬 일관성있게 객체를 만들 수 있고 만들 수 있음
- 객체 프로퍼티 수정이 쉬움
- 어떤 함수든 new 연산자를 사용하면 생성자함수가 되기 때문에, 첫 글자는 대문자로 써서 구분함
```javascript
 function User(name){
    this.name = name;
    tihs.introduce = function() {
        return `My name is ` +this.name;
       }
  }     
 
 let User1 = new Person('재원'); // My name is 재원
 let User2 = new Person('지원'); // My name is 지원
 ```
 <br>
 
 ### 참고자료
 - https://youtu.be/qnOX3M7VpQ8
 - https://youtu.be/VLhA3haEfIk
 - https://youtu.be/VnqC_EmnU9g
 - https://youtu.be/8hrSkOihmBI
 - https://youtu.be/dHrI-_xq1Vo
