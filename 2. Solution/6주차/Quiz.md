Q. 화살표 함수로 코드를 최대한 간결하게 만들어보자.

```javascript
function outer(x) {
    return function inner(){
        return x*x;
    }
}

const innerFuc = outer(10);
const result = innerFuc();
console.log(result);

