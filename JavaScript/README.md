# JavaScript

* [Parameter vs Arguments](#parameter-vs-arguments)
* [Evaluation Strategy](#evaluation-strategy)
* [Scope](#scope)
* TODO : [IIFE](#iife)
* [Hoisting](#hoisting)
* TODO : [Closure](#closure)
* TODO : [Immutable](#immutable)
* TODO : [함수선언문과 함수표현식](#함수선언문과-함수표현식)

* TODO : [ES6 - let & const](#es6---let--const)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main)

## Parameter vs Arguments

**parameter(매개변수)와 arguments(인자)의 차이**

parameter는 formal parameter(형식 매개변수)로 인식하면 되고, arguments는 actual parameter(실인자)로 받아들이면 된다.

parameter는 함수 선언부에 정의되고, arguments는 함수 호출부에서 사용된다.

```js
var a = 1;
var func = function(b) { // parameter, formal parameter, 매개변수, 형식 매개변수
  // code...
};

func(a); // arguments, actual parameter, 인자, 실인자
```

### Reference
- https://perfectacle.github.io/2017/10/30/js-014-call-by-value-vs-call-by-reference/

[뒤로](https://github.com/SeongYongLee/TIL/tree/main)/[위로](#javascript)

</br></br>

## Evaluation Strategy

**평가 전략**

프로그래밍 언어에서 함수 호출의 아규먼트(argument)의 순서를 언제 결정하고 함수에 어떤 종류의 값을 통과시킬지 결정하는 것

함수 실행 시 인자로 무엇을 던지느냐에 따라 함수가 어떻게 실행될지 결정하는 것을 의미한다.

Call은 함수를 호출 할 때 사용하는 동사이고 Pass는 인자를 전달한다는 의미를 나타내는 동사이다.

### call by value (O)

데이터 타입이 원시 타입인 경우 값(value)으로 전달된다. 즉, 값이 복사되어 전달된다. 이를 call-by-value(값에 의한 전달)라 한다.

원시 타입은 값이 한번 정해지면 변경할 수 없다. (Immutable)

또한 이들 값은 런타임(변수 할당 시점)에 메모리의 스택 영역(Stack Segment)에 고정된 메모리 영역을 점유하고 저장된다.

caller가 인자를 복사해서 넘겨준다. callee가 값이 변경되어도 caller는 영향을 받지 않는다.

TODO : [Immutable](#immutable)

```js
var value = 2;

var callee = (copiedValue) => {  // callee - 이 줄에서 copiedValue = 2와 동일한 동작이 수행됨
  copiedValue = copiedValue + 1;
};

callee(value); // caller
console.log(value); // 2
```

### call by reference (X)

**JS는 무조건 call by value로 작동한다.**

### call by sharing (O)

**Call By Value of Reference.**

자바스크립트에 함수의 매개변수를 설명할 때 일반적으로 얘기하는 값으로 전달(Call by Value) 또는 참조로 전달(Call by Reference) 방식으로는 이해하기 힘들다.

데이터 타입이 원시 타입이 아닌 경우 (객체 타입) caller는 변수가 가리키는 메모리 공간에 저장되어 있는 값을 복사하여 전달한다.

따라서 call by Reference와 차이점은 함수 안에서 객체의 속성 수정 시에는 같은 곳을 참조하지만 객체 자체를 수정해버리면 관계가 깨져버린다.

```js
function test(x) { // callee
  x.a = 9;
  console.log(x); // {a: 9}
}

var i = {a: 5};
test(i); // caller 
console.log(i); // {a: 9}
```

```js
function change(num, obj1, obj2) {
  num = num * 10;
  obj1.item = "changed";
  obj2 = {item: "changed"};
}

var num = 10;
var obj1 = {item: "unchanged"};
var obj2 = {item: "unchanged"};

change(num, obj1, obj2);

console.log(num); // 10
console.log(obj1.item); // changed
console.log(obj2.item); // unchanged, call by Reference라면 바뀌어야 한다.
```

### Reference

- https://perfectacle.github.io/2017/10/30/js-014-call-by-value-vs-call-by-reference

- http://milooy.github.io/TIL/JavaScript/call-by-sharing.html

- https://poiemaweb.com/js-object

- https://velog.io/@jimmyjoo/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%8F%89%EA%B0%80%EC%A0%84%EB%9E%B5-Call-By-Value-vs-Call-By-Reference-vs-Call-By-Sharing

[뒤로](https://github.com/SeongYongLee/TIL/tree/main)/[위로](#javascript)

</br></br>

## Scope

### 스코프

함수를 작성할 때 중괄호'{ }'를 이용하여 함수의 범위를 작성한다.

이 때 변수에 접근할 수 있는 범위, 변수가 영향을 미치는 범위, 변수의 유효 범위, 코드가 유효한 범위라고 할 수 있다.

스코프의 종류에 따라 변수, 함수, 코드 등의 유효 범위가 달라질수 있으며 범위 밖에 있는 변수는 이용 할 수 없다.

전역 변수와 같은 이름의 변수를 스코프 안에서 새로 생성할 수 있다.

**JS(ES6)는 함수 레벨과 블록 레벨의 정적 스코프 규칙을 따른다.**

### 스코프의 종류

#### 동작 - 정적 스코프 (렉시컬 스코프, Lexical scope)

렉시컬 스코프는 호출 스택과 관계없이 소스코드가 작성된 문맥, 소스 코드 내에 변수가 선언된 시점에서 스코프가 결정된다.

현재 대부분의 언어들은 렉시컬 스코프 규칙을 따르고 있다.

런타임에서 렉시컬 스코프를 수정할 수 있는 방법들(eval, with)이 있지만, 권장하지 않는다.


```js
var name = 'first';

function first() {
	console.log(name); // first
}

function second() {
	var name = 'second';
	first();
}

second();
```

#### 동작 - 동적 스코프 (다이나믹 스코프, Dynamic scope)

동적 스코프는 런타임 도중에 실행 콘텍스트나 호출 콘텍스트에 의해 스코프가 결정된다.

만약 JS가 동적 스코프인 경우 아래 예제와 같다.

```js
var name = 'first';

function first() {
	console.log(name); // second
}

function second() {
	var name = 'second';	
	first();
}

second();
```

#### 레벨 - 함수 스코프

함수가 유효 범위이다.

- var

```js
function hello(name){
	if(name){
		var greet = name + '님 안녕하세요';
	}
	console.log(greet); // LSY님 안녕하세요
}

hello('LSY');

var topic = "자바스크립트";
if (topic) {
	var topic = "리액트";
	console.log('블록', topic); // 블록 리액트
}
console.log('글로벌', topic); // 글로벌 리액트
// Hoisting으로 인해 두 topic은 같은 변수이다.
```

#### 레벨 - 블록 스코프

블록이 유효 범위이다.

- let, const - JS는 ES2015(ES6)부터 블록 레벨 스코프를 지원하기 시작했다.

함수 레벨 스코프가 사용하기에는 더 편리하지만 블록 레벨 스코프보다 스코프의 범위가 넓으므로 코드에 대한 복잡성을 증가하는 요인이 된다. 대표적인 예로 if/else 문이 있다.

따라서 변수의 유효 범위는 좁을수록 좋고 선택이 가능하다면 블록 레벨 스코프를 사용해야 한다.

비동기처리 반복문의 해결 방법 중 하나로 블록 레벨 스코프로 사용하는 예가 있다.

TODO : [Closure](#closure)

```js
function hello(name){
	if(name){
		let greet = name + '님 안녕하세요';
	}
	console.log(greet); // greet is not defined
}

hello('LSY');

var topic = "자바스크립트";
if (topic) {
	let topic = "리액트";
	console.log('블록', topic); // 블록 리액트
}
console.log('글로벌', topic); // 글로벌 자바스크립트
```

#### 레벨 - 전역 스코프

전체가 범위며 전역 스코프에서 변수를 선언하게 되면 어디서든지 참조할 수 있는 전역 변수가 된다.

하나의 html에서 두 개의 js파일을 로드해서 사용할 때에도 전역 변수는 사용이 가능하다.

전역 변수를 남발하게 되면 변수이나 함수의 중복이 될 가능성이 커지며 코드를 예측할 수 없어되어 조심해야 한다.

모든 스크립트는 전역 스코프에 접근할 수 있으며, 모든 사람이 전역 네임스페이스를 사용하여 변수를 정의하면 충돌이 발생할 수 있다.

이러한 충돌을 줄이기 위해 모듈 패턴(즉시 실행 함수)를 사용해서 전역 변수를 해당 파일(모듈)에서만 범위를 억제, 로컬 네임스페이스 내에 캡슐화하는 방법이 있다.

TODO : [IIFE](#iife)

#### 레벨 - 지역 스코프

함수 코드 블록이 만든 스코프로 함수 내부와 하위 함수의 변수와 함수만 참조가 가능하다.

지역에서 선언한 건 같은 지역에서만 참조가 된다

### 스코프 체인 (Scope Chain)

스코프 간에 상하 관계를 의미한다.

스코프 체인은 내부 함수에서 변수를 찾기 위해 외부 함수로 접근할 때에 탐색을 하게 되는 관계를 말한다.

스코프의 탐색은 해당 스코프 내부를 먼저 탐색하고 선언된 것이 없다면 한 단계 위의 스코프를 탐색하며 해당 변수를 찾을 때 까지 반복적으로 이루어진다.

이 과정은 해당 선언을 찾거나 null이 될 때 (더 이상의 참조가 불가능할 때) 탐색을 멈춘다.

### Reference

- https://meetup.toast.com/posts/86

- https://okayoon.tistory.com/entry/%EC%8A%A4%EC%BD%94%ED%94%84Scope%EB%9E%80

- [https://www.zerocho.com/category/Javascript/post/5740531574288ebc5f2ba97e](https://www.zerocho.com/category/Javascript/post/5740531574288ebc5f2ba97e)

- 러닝 리액트(Learning React) 2판 | 알렉스 뱅크스 , 이브 포셀로 지음 | 오현석 옮김 | 한빛미디어

[뒤로](https://github.com/SeongYongLee/TIL/tree/main)/[위로](#javascript)

</br></br>

## IIFE

TODO : 

```js
// 예시 1
// 로컬 네임스페이스
var obj = {
  x: 'local',
  y: function() {
    alert(this.x);
  }
}
// ->
var another = function () {
  var x = 'local';
  function y() {
    alert(x);
  }
  return { y: y };
}
var newScope = another();
// -> 즉시 호출 함수
var newScope = (function () {
  var x = 'local';
  return {
    y: function() {
      alert(x);
    }
  };
})();
// 예시 2
(function(){
	var APP = APP || {};
	APP.info = {
		name : 'chat app', version : '1.2.1'
	};
	APP.Start = function() {
		// ....
	};
	console.log(APP.info.name); // chat app
})();

console.log(APP.info.name); // APP is not defined
```

### Reference

[뒤로](https://github.com/SeongYongLee/TIL/tree/main)/[위로](#javascript)

</br></br>

## Hoisting

### 호이스팅

hoist 라는 단어의 사전적 정의는 끌어올리기 라는 뜻이다.

var, let, const로 정의된 변수나 함수선언문, 함수표현식들이 해당 스코프의 꼭대기(유효 범위의 최상단)에 모두 끌어올려지는것 처럼 보이는 현상

실행 컨텍스트가 활성화 되었을때 해당 영역에서 변수의 이름을 메모리에 먼저 수집하는 현상으로 인해 발생하는 현상을 말한다.

유효범위의 코드가 실행되기 전 메모리에 먼저 저장했던 선언문을 사용할 수 있다.

### 선언, 할당

#### 선언 (Declaration)

말 그대로 선언하는 것이다. 값을 할당하지 않는다.

자바스크립트 엔진은 코드를 인터프리팅 하기 전에 그 코드를 먼저 컴파일한다.

`var a = 2;`를 하나의 구문으로 생각할 수도 있지만, 자바스크립트는 다음 두 개의 구문으로 분리하여 본다.

`var a;`

`a = 2;`

변수 선언(생성) 단계와 할당(초기화) 단계를 나누고, 선언 단계에서는 그 선언이 소스코드의 어디에 위치하든 해당 스코프의 컴파일단계에서 처리해버리는 것이다.

선언 단계가 스코프의 꼭대기로 호이스팅(끌어올림)되는 작업이라고 볼 수 있다.

#### 할당 (Assignment, 초기화)

특정 변수에 값을 할당하는 과정이다. 할당 구문은 런타임 과정에서 이루어진다.

### 호이스팅 대상 - 변수

호이스팅 현상이 발생한다.

#### var

선언만 끌어 올려지며 할당은 끌어 올려지지 않는다. 

#### let & const

호이스팅은 현상은 발생하지만 할당까지는 TDZ에 빠지기 때문에 선언 전에 참조할 경우 undefined를 반환하지 않고 ReferenceError를 발생시키는 특징이 있다.

가상의 개념 '끌어올려지는 현상'의 모습을 찾아볼 수 없기 때문에 let과 const에서는 호이스팅이 발생하지 않는다고 라고 말하기도 한다.

#### TDZ (일시적 사각지대, Temporal Dead Zone)

초기화되지 않은 변수가 있는 곳을 Temporal Dead Zone이라고 한다.

변수가 초기화되는 순간 TDZ에서 나오게 되며 사용할 수 있다.

TODO : [ES6 - let & const](#es6---let--const)

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

#### 함수표현식

호이스팅은 발동하지만 변수 호이스팅이 일어난다.

함수 호출 전 함수를 선언하면 TypeError가 발생한다.

JavaScript: The Good Parts의 저자이며 자바스크립트의 권위자인 더글러스 크락포드(Douglas Crockford)는 이와 같은 문제 때문에 함수 표현식 만을 사용할 것을 권고하고 있다.

함수 호이스팅은 함수 호출 전 반드시 함수를 선언하여야 한다는 규칙을 무시하므로 코드의 구조를 엉성하게 만들 수 있다고 지적한다.

TODO : [함수선언문과 함수표현식](#함수선언문과-함수표현식)

```js
foo(); // hello
foo2(); // TypeError: foo2 is not a function

function foo() { // 함수선언문
        console.log("hello");
}

var foo2 = function() { // 함수표현식
        console.log("hello2");
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
console.log(typeof yourName); // > "functio
```

### 주의점

코드의 가독성과 유지보수를 위해 함수와 변수를 가급적 코드 상단부에서 선언하면, 호이스팅 현상 및 스코프 꼬임을 방지할 수 있다.  

호이스팅을 이해하지 못하면 의도한 결과가 나오지 않을 수도 있다.

최근에는 ES6 문법이 표준화가 되면서 크게 신경쓰지 않아도 되는 부분이 되었지만, JavaScript 라는 언어의 특성을 가장 잘 보여주는 특성 중 하나이기에 호이스팅을 이해하는 것이 중요하다.

### Reference

- https://meetup.toast.com/posts/86

- https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html

- https://okayoon.tistory.com/entry/%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85Hoisting?category=835832

- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/blob/master/JavaScript/README.md#hoisting

- https://poiemaweb.com/js-function

[뒤로](https://github.com/SeongYongLee/TIL/tree/main)/[위로](#javascript)

</br></br>

## Closure

TODO : 

### Reference

[뒤로](https://github.com/SeongYongLee/TIL/tree/main)/[위로](#javascript)

</br></br>

## Immutable

TODO : 

### Reference

[뒤로](https://github.com/SeongYongLee/TIL/tree/main)/[위로](#javascript)

</br></br>

## 함수선언문과 함수표현식

TODO : 

### Reference

[뒤로](https://github.com/SeongYongLee/TIL/tree/main)/[위로](#javascript)

</br></br>

## ES6 - let & const

TODO : 

### Reference

[뒤로](https://github.com/SeongYongLee/TIL/tree/main)/[위로](#javascript)

</br></br>