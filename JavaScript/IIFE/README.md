# IIFE

## 즉시 호출 함수 표현식 (**Immediately Invoked Function Expressions)**

`(function() {})();`

JavaScript parser는 `function foo(){ }();`을 `function foo(){ }`와 `();`로 읽는다. 전자는 함수 선언이며 후자(한 쌍의 중괄호)는 함수를 호출하려고 시도했지만, 이름이 지정되지 않았기 때문에 `Uncaught SyntaxError : Unexpected token )`을 발생시킨다.

괄호를 추가하여 고치는 두 가지 방법으로 `(function foo(){ })()` 와 `(function foo(){ }()). function`가 있다. `function`으로 시작하는 문은 함수 선언으로 간주된다. 이 함수를 ()로 묶으면 함수 식이 되고, 이렇게하면 다음 ()로 함수를 실행할 수 있다.

## 주요 이점

### 불필요한 전역 변수와 함수를 생성하지 않는다.

IIFE 에서 생성된 변수와 함수의 이름은 전역 Scope와 충돌하지 않는다. (이를 오염시키지 않는다고도 말한다.)

프로그램 초기화 시점에 아래 init 함수를 실행한다고 가정한다.

```jsx
function init() {
  var operate = "init";
  console.log(operate);
}

init();
```

이 함수는 전역 Scope에 선언되어 name collision 이 발생할 확률을 높이며, 개발자 의도와 달리 다른 code에 의해 재호출 될 수도 있다.

따라서 외부 코드로부터 사용되지 않는 단 한번 호출하는 코드들, 이 코드에서 사용하는 변수와 함수들은 IIFE를 사용하여 전역 Scope 오염을 방지하고, 다른 개발자가 실수로 호출할 수 없도록 하는게 바람직하다.

```jsx
(function init() {
  var operate = "init";
  console.log(operate);
})();
```

이렇게 IIFE 내부에 선언된 변수와 함수는 외부에서 접근이 불가능하다. 함수 본체를 찾기 위해 다른 곳을 찾아볼 필요 없이 코드를 호출하는 코드 바로 안에 핸들러가 정의되어 있으면 코드가 보다 독립적이고 읽기 쉽게 보일 것이다.

```jsx
(function init() {
  var operate = "init";
  console.log(operate);
})();

console.log(operate); //operate is not defiend
```

### Closure

closure와 함께 private data를 사용할 수 있다. IIFE의 대표적 use case 중 하나로 Closure와 함께 priavte 변수를 생성하여 사용합니다. 아래 예제에서 count라는 private 변수를 만들어 사용하고 있다.

```jsx
const uniqueId = (function () {
  let count = 0;
  return function () {
    return ++count;
  };
})();

console.log(uniqueId()); // 1
console.log(uniqueId()); // 2
```

IIFE가 실행과 동시에 Closure 함수를 리턴하고 있으며 이때 count 변수는 private 변수로 외부에서 접근할 수 없게 된다.

그리고 클로저의 반복문에서 값의 중복 현상을 해결하기 위해서 사용한다.

- TODO : [Closure](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/Closure)

### 변수 이름 alias

jQuery와 또 다른 라이브러리를 사용하고 있는데 둘 다 $ 을 전역 변수로 사용할 때 인자를 사용하는 IIFE로 아래와 같이 사용할 수 있다.

```
window.$ = function libraryA() {
};

(function($) {
})(jQuery);
```

## 문법

일반적으로 IIFE 사용할 때 아래와 같이 두 가지 방법이 있다.

```jsx
(function () {
  console.log("I am IIFE");
})();

// Variation 1
(function () {
  console.log("I am IIFE");
})();
```

ES6 에서 도입된 Arrow function과 함께 사용할 수도 있다.

```jsx
(() => console.log("IIFE with arrow"))();

(() => {
  console.log("IIFE with arrow");
})();
```

리턴 값이 필요없을 때 문법적으로 IIFE를 아래와 같이도 사용이 가능하다. (실제로는 위 방식을 많이 쓴다.)

```jsx
!(function () {
  console.log("I am IIFE");
})();

+(function () {
  console.log("I am IIFE");
})();

-(function () {
  console.log("I am IIFE");
})();

~(function () {
  console.log("I am IIFE");
})();

void (function () {
  console.log("I am IIFE");
})();
```

자바스크립트 코드를 해석할 때 function 으로 시작하면 함수 선언식으로 인지하지만 위 코드처럼 `!,+,-,~,void` 등의 연산자와 키워드를 사용할 경우 함수 표현식으로 인지하기 때문에 위와 같은 문법으로 사용이 가능하다.

- [함수의 선언(Declaration)과 표현(Expression)](<https://github.com/SeongYongLee/TIL/tree/main/JavaScript/함수의-선언(Declaration)과-표현(Expression)>)

만약 IIFE가 return 값이 존재할 경우 위 방식을 사용하면 아래와 같이 예상치 못한 결과가 나타난다.

```jsx
var a = ~(function () {
  console.log("I am IIFE");
})();

var b = (function () {
  return 3;
})();

console.log(a); // -1
console.log(b); // 3

// Don't add JS syntax to this code block to prevent Prettier from formatting it.
const foo = void (function bar() {
  return "foo";
})();

console.log(foo); // undefined
```

연산자나 void는 보다는 `(function() {} )()` 이 널리 활용되므로 위 방법은 알고만 넘어가면 된다.

IIFE에 인자를 전달할 수 있다.

```jsx
(function (count) {
  for (let i = 0; i < count; i++) console.log("I am IIFE");
})(3);
```

또한 IIFE에 이름을 붙일 수도 있다.

```jsx
(function named(count) {
  for (let i = 0; i < count; i++) console.log("I am named IIFE");
})(3);
```

종종 아래와 같이 IIFE 앞에 semicolon이 붙는 경우를 봤을 것이다.

```
;(function() {
  console.log('semi')
})();
```

이는 IIFE 이전 코드의 semicolon이 생략된 경우 에러가 발생하기 때문에 대비한 것이다. 구체적인 예시 하나를 보면 다음과 같다.

```
var name = value

(function() {
  console.log('semi')
})();
```

위 코드는 아래와 같이 해석됩니다. IIFE 이전 코드에 semicolon이 없을 경우 함수의 인자로 전달되서 에러가 발생할 수 있다.

```
var name = value(function() {
  console.log('semi')
})();
```

## 사례

```jsx
(showName = function (name) {
  console.log(name || "No Name");
})(); // No Name
showName("Rich"); // Rich
showName(); // No Name
```

```jsx
// 즉시 호출 함수
(function () {
  var APP = APP || {};
  APP.info = {
    name: "chat app",
    version: "1.2.1",
  };
  APP.Start = function () {
    // ....
  };
  console.log(APP.info.name); // chat app
})();

console.log(APP.info.name); // APP is not defined
```

```jsx
// 로컬 네임스페이스
var obj = {
  x: "local",
  y: function () {
    alert(this.x);
  },
};
// ->
var another = function () {
  var x = "local";
  function y() {
    alert(x);
  }
  return { y: y };
};
var newScope = another();
// -> 즉시 호출 함수
var newScope = (function () {
  var x = "local";
  return {
    y: function () {
      alert(x);
    },
  };
})();
```

```jsx
// All the code is wrapped in the IIFE
(function () {
  var firstName = "Richard";
  function init() {
    doStuff(firstName);
    // code to start the application
  }
  function doStuff() {
    // Do stuff here
    console.log("doStuff");
  }
  function doMoreStuff() {
    // Do more stuff here
  }
  // Start the application
  init();
})();
```

## Reference

- [https://github.com/yangshun/front-end-interview-handbook/blob/master/contents/kr/javascript-questions.md](https://github.com/yangshun/front-end-interview-handbook/blob/master/contents/kr/javascript-questions.md)
- [https://medium.com/sjk5766/iife-immediately-invoked-function-expression-정리-53ab6543b828](https://medium.com/sjk5766/iife-immediately-invoked-function-expression-%EC%A0%95%EB%A6%AC-53ab6543b828)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/JavaScript)
