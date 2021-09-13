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

TODO : [Closure](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/Closure)

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

TODO : [IIFE](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/IIFE)

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

- https://www.zerocho.com/category/Javascript/post/5740531574288ebc5f2ba97e

- 러닝 리액트(Learning React) 2판 | 알렉스 뱅크스 , 이브 포셀로 지음 | 오현석 옮김 | 한빛미디어

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/FrontEnd)