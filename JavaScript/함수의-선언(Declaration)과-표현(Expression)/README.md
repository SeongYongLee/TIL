# 함수의 선언(Declaration)과 표현(Expression)

## 함수의 선언 (Function Declarations)

일반적인 프로그래밍 언어에서의 함수 선언과 비슷한 형식이다. function 정의 부만 존재하고 별도의 할당 명령이 없다.

호이스팅에 영향을 받는다. 함수 호이스팅이 일어난다. 자바 스크립트의 실행 컨텍스트(execution context)에 로딩 되어 있으므로 언제든지 호출할 수 있다.

## 함수의 표현 (Function Expressions)

유연한 자바스크립트 언어의 특징을 활용한 선언 방식이다. 정의한 function을 별도의 변수에 할당하는 것을 말한다.

호이스팅의 영향을 받지 않는다. 정확히는 변수 호이스팅만 일어난다. 인터프리터가 해당 라인에 도달 하였을때만 실행이 된다.

## 함수 생성 방법 및 예제

### 함수의 선언

function 키워드로 시작하고, 그 뒤에 함수 이름이 온다. 함수에 속한 자바스크립트 문장은 중괄호({}) 사이에 들어간다.

### 함수의 표현

이름 없는 함수를 만들며, 변수에 값을 대입할 수 있다.

```jsx
// 함수의 선언
foo1(); // foo
function foo1() {
    alert('foo');
}
// 함수의 선언 + IIFE
foo3(); // "foo3" is not defined.
(function foo3 () {});

// 함수의 표현
foo2(); // Uncaught TypeError: foo2 is not a function
var foo2 = function() {
    alert('foo');
};
```

## Reference

- [https://okayoon.tistory.com/entry/호이스팅Hoisting?category=835832](https://okayoon.tistory.com/entry/%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85Hoisting?category=835832)
- [https://joshua1988.github.io/web-development/javascript/function-expressions-vs-declarations](https://joshua1988.github.io/web-development/javascript/function-expressions-vs-declarations/)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/FrontEnd)