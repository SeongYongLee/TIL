# JavaScript

* [Parameter vs Arguments](#parameter-vs-arguments)
* [Evaluation Strategy](#evaluation-strategy)
* [Scope](#scope)

[뒤로](https://github.com/SeongYongLee/TIL)

## Parameter vs Arguments

parameter(매개변수)와 arguments(인자)의 차이

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

[뒤로](https://github.com/SeongYongLee/TIL)/[위로](#javascript)

## Evaluation Strategy

프로그래밍 언어에서 함수 호출의 아규먼트(argument)의 순서를 언제 결정하고 함수에 어떤 종류의 값을 통과시킬지 결정하는 것,

함수 실행 시 인자로 무엇을 던지느냐에 따라 함수가 어떻게 실행될지 결정하는 것을 의미한다.


### call by value (O)

arguments가 원시 값인 경우 arguments로 복사된 값이 넘어온다.

caller가 인자를 복사해서 넘겨준다. callee가 값이 변경되어도 caller는 영향을 받지 않는다.

```js
var value = 2;

var callee = (copiedValue) => {  // callee - 이 줄에서 copiedValue = 2와 동일한 동작이 수행됨
  copiedValue = copiedValue + 1;
};

callee(value); // caller
console.log(value); // 2
```

### call by Reference (X)

JS는 무조건 call by value로 작동한다.

### call by sharing (O)

자바스크립트에 함수의 매개변수를 설명할 때 일반적으로 얘기하는 값으로 전달(Call by Value) 또는 참조로 전달(Call by Reference) 방식으로는 이해하기 힘들다.

argument가 원시 값이 아닌 경우 caller가 주소 값을 복사해서 넘겨준다.

객체의 속성 수정 시에는 참조이지만 객체 자체를 수정해버리면 관계가 깨진다.

함수에 문자열, 숫자 등의 기본 형태의 인자를 넘기면 값을 복사한 지역 변수로 사용한다.

함수에 객체 형태의 인자를 넘기면 속성은 공유하지만 새로 객체를 할당할 수는 없다.

자바 진영에서는 Pass by Value, 루비 진영에서는 Pass by Reference 라고도 한다. call by Reference와 차이점은 함수 안에서 인자를 새로 할당했을 때 호출한 곳에서 접근할 수 없다는 점이다.

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

[뒤로](https://github.com/SeongYongLee/TIL)/[위로](#javascript)

## 스코프

함수를 작성할 때 중괄호'{ }'를 이용하여 함수의 범위를 작성한다.

이 때 변수에 접근할 수 있는 범위, 변수가 영향을 미치는 범위, 변수의 유효 범위, 코드가 유효한 범위라고 할 수 있다.

스코프의 종류에 따라 변수, 함수, 코드 등의 유효 범위가 달라질수 있으며 범위 밖에 있는 변수는 이용 할 수 없다.

전역 변수와 같은 이름의 변수를 스코프 안에서 새로 생성할 수 있다.

**JS(ES6)는 함수 레벨과 블록 레벨의 정적 스코프 규칙을 따른다.**

### 스코프의 종류

### 동작 - 정적 스코프 (렉시컬 스코프, Lexical scope)

렉시컬 스코프는 호출 스택과 관계없이 소스코드가 작성된 문맥, 소스 코드 내에 변수가 선언된 시점에서 스코프가 결정된다.

현재 대부분의 언어들은 렉시컬 스코프 규칙을 따르고 있다.

런타임에서 렉시컬 스코프를 수정할 수 있는 방법들(eval, with)이 있지만, 권장하지 않는다.


```jsx
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

### 동작 - 동적 스코프 (다이나믹 스코프, Dynamic scope)

동적 스코프는 런타임 도중에 실행 콘텍스트나 호출 콘텍스트에 의해 스코프가 결정된다.

만약 JS가 동적 스코프인 경우 아래 예제와 같다.

```jsx
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

## 레벨

### 레벨 - 함수 스코프

- 함수가 유효 범위이다.
- var

```jsx
function hello(name){
	if(name){
		var greet = name + '님 안녕하세요';
	}
	console.log(greet); // LSY님 안녕하세요
}

hello('LSY');
```

### 레벨 - 블록 스코프

블록이 유효 범위이다.

let, const - JS는 ES2015(ES6)부터 블록 레벨 스코프를 지원하기 시작했다.

함수 레벨 스코프가 사용하기에는 더 편리하지만 블록 레벨 스코프보다 스코프의 범위가 넓으므로 코드에 대한 복잡성을 증가하는 요인이 된다.

    따라서 변수의 유효 범위는 좁을수록 좋고 선택이 가능하다면 블록 레벨 스코프를 사용해야 한다.

    ```jsx
    function hello(name){
    	if(name){
    		let greet = name + '님 안녕하세요';
    	}
    	console.log(greet); // greet is not defined
    }

    hello('LSY');
    ```

### 전역 스코프

전체가 범위며 전역 스코프에서 변수를 선언하게 되면 어디서든지 참조할 수 있는 전역 변수가 된다.
하나의 html에서 두 개의 js파일을 로드해서 사용할 때에도 전역 변수는 사용이 가능하다.

전역 변수를 남발하게 되면 변수이나 함수의 중복이 될 가능성이 커지며 코드를 예측할 수 없어되어 조심해야 한다.

모든 스크립트는 전역 스코프에 접근할 수 있으며, 모든 사람이 전역 네임스페이스를 사용하여 변수를 정의하면 충돌이 발생할 수 있다.

이러한 충돌을 줄이기 위해 모듈 패턴(즉시 실행 함수)를 사용해서 전역 변수를 해당 파일(모듈)에서만 범위를 억제, 로컬 네임스페이스 내에 캡슐화하는 방법이 있다.

```jsx
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

### 지역 스코프

함수 코드 블록이 만든 스코프로 함수 내부와 하위 함수의 변수와 함수만 참조가 가능하다.

지역에서 선언한 건 같은 지역에서만 참조가 된다

## 스코프 체인 (Scope Chain)

스코프 간에 상하 관계를 의미한다.

스코프 체인은 내부 함수에서 변수를 찾기 위해 외부 함수로 접근할 때에 탐색을 하게 되는 관계를 말한다.

스코프의 탐색은 해당 스코프 내부를 먼저 탐색하고 선언된 것이 없다면 한 단계 위의 스코프를 탐색하며 해당 변수를 찾을 때 까지 반복적으로 이루어진다.

이 과정은 해당 선언을 찾거나 null이 될 때 (더 이상의 참조가 불가능할 때) 탐색을 멈춘다.

## Reference

- [https://meetup.toast.com/posts/86](https://meetup.toast.com/posts/86)
- [https://okayoon.tistory.com/entry/스코프Scope란](https://okayoon.tistory.com/entry/%EC%8A%A4%EC%BD%94%ED%94%84Scope%EB%9E%80)

[뒤로](https://github.com/SeongYongLee/TIL)/[위로](#javascript)