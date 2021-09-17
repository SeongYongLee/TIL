## Hoisting

### 호이스팅

hoist 라는 단어의 사전적 정의는 끌어올리기 라는 뜻이다.

실행 컨텍스트가 활성화 되었을때 해당 영역에서 변수의 이름을 메모리에 먼저 수집하는 현상으로 인해 발생하는 현상, 해당 스코프의 꼭대기(유효 범위의 최상단)에 모두 끌어올려지는것 처럼 보이는 현상을 말한다.

자바스크립트는 모든 선언(var, let, const, function, function*, class)을 호이스팅한다.

유효범위의 코드가 실행되기 전 메모리에 먼저 저장했던 선언문을 사용할 수 있다.

### 호이스팅 대상 - 변수

호이스팅 현상이 발생한다.

#### var (Variable Hositing)

선언만 끌어 올려지며 할당은 끌어 올려지지 않는다. 

var 키워드로 선언된 변수는 선언 단계와 초기화 단계가 한번에 이루어진다.

즉, 스코프에 변수가 등록되고 변수는 메모리에 공간을 확보한 후 undefined로 초기화된다.

따라서 변수 선언문 이전에 변수에 접근하여도 Variable Object에 변수가 존재하기 때문에 에러가 발생하지 않는다. 다만 undefined를 반환한다. 이러한 현상을 변수 호이스팅(Variable Hoisting)이라한다.

이후 변수 할당문에 도달하면 비로소 값의 할당이 이루어진다.

#### let & const

호이스팅은 현상은 발생하지만 할당까지는 TDZ에 빠지기 때문에 선언 전에 참조할 경우 undefined를 반환하지 않고 ReferenceError를 발생시키는 특징이 있다.

가상의 개념 '끌어올려지는 현상'의 모습을 찾아볼 수 없기 때문에 let과 const에서는 호이스팅이 발생하지 않는다고 라고 말하기도 한다.

#### TDZ (일시적 사각지대, Temporal Dead Zone)

초기화되지 않은 변수가 있는 곳을 Temporal Dead Zone이라고 한다.

변수가 초기화되는 순간 TDZ에서 나오게 되며 사용할 수 있다.

* TODO : [ES6 - let & const](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/ES6-let-&-const)

```js
console.log(i); // undefined
console.log(j); // Uncaught ReferenceError
var i = "var"; // var 변수 
let j = "let"; // let 변수

var a = '외부 a';
const b = '외부 b';
(function() {
	console.log(a); // undefined
	var a = '내부 a';
}());
(function() {
	console.log(b); // ReferenceError
	const b = '내부 b';
}());
```

### 호이스팅 대상 - 함수

#### 함수선언문

함수 선언문의 경우 함수 자체를 끌어올리는 함수 호이스팅이 일어난다.

함수 선언, 초기화, 할당이 한번에 이루어진다.

따라서 함수가 정의되기 이전에 함수 호출이 가능하며 함수 선언의 위치와는 상관없이 코드 내 어느 곳에서든지 호출이 가능하다.

함수 호이스팅은 함수 호출 전 반드시 함수를 선언하여야 한다는 규칙을 무시하므로 코드의 구조를 엉성하게 만들 수 있다고 지적한다.

JavaScript: The Good Parts의 저자이며 자바스크립트의 권위자인 더글러스 크락포드(Douglas Crockford)는 이와 같은 문제 때문에 함수 표현식 만을 사용할 것을 권고하고 있다.

#### 함수표현식

호이스팅은 발동하지만 변수 호이스팅이 일어난다.

함수 호출 전 함수를 선언하면 TypeError가 발생한다.

* TODO : [함수의 선언(Declaration)과 표현(Expression)](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/함수의-선언(Declaration)과-표현(Expression))

```js
foo(); // hello
foo2(); // TypeError: foo2 is not a function

function foo() { // 함수선언문
    console.log("hello");
}

var foo2 = function() { // 함수표현식 + var
    console.log("hello2");
}

foo3(); // ReferenceError: foo3 is not defined

const foo3 = function() { // 함수표현식 + const
    console.log("hello3");
}
```

### 호이스팅 순서

같은 이름의 var 변수 선언과 함수 선언에서의 호이스팅의 경우 변수 선언이 함수 선언보다 위로 끌어올려진다.

```js
console.log(typeof myName);
console.log(typeof yourName);

var myName = "hi";

function myName() {
    console.log("yuddomack");
}
function yourName() {
    console.log("everyone");
}

var yourName = "bye";

console.log(typeof myName);
console.log(typeof yourName);

/** --- JS Parser 내부의 호이스팅(Hoisting)의 결과 --- */

// 1. [Hoisting] 변수값 선언 
var myName; 
var yourName; 

// 2. [Hoisting] 함수선언문
function myName() {
    console.log("yuddomack");
}
function yourName() {
    console.log("everyone");
}

// 3. 변수값 할당 전

console.log(typeof myName);  // > "function"
console.log(typeof yourName); // > "function"

// 4. 변수값 할당 후

myName = "hi";
yourName = "bye";

console.log(typeof myName); // > "string"
console.log(typeof yourName); // > "string"
```

따라서 값이 할당되어 있지 않은 변수의 경우는 다음과 같다.

```js
var myName = "Heee"; // 값 할당 
var yourName; // 값 할당 X

function myName() { // 같은 이름의 함수 선언
    console.log("myName Function");
}
function yourName() { // 같은 이름의 함수 선언
    console.log("yourName Function");
}

console.log(typeof myName); // > "string"
console.log(typeof yourName); // > "function"
```

### 주의점

코드의 가독성과 유지보수를 위해 함수와 변수를 가급적 코드 상단부에서 선언하면, 호이스팅 현상 및 스코프 꼬임을 방지할 수 있다.  

호이스팅을 이해하지 못하면 의도한 결과가 나오지 않을 수도 있고, JavaScript 라는 언어의 특성을 가장 잘 보여주는 특성 중 하나이기에 호이스팅을 이해하는 것이 중요하다.

### Reference

- https://meetup.toast.com/posts/86

- https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html

- https://okayoon.tistory.com/entry/%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85Hoisting?category=835832

- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/blob/master/JavaScript/README.md#hoisting

- https://poiemaweb.com/js-function

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/FrontEnd)