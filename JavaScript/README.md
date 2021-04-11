# JavaScript

* [Parameter vs Arguments](#parameter-vs-arguments)
* [Evaluation Strategy](#evaluation-strategy)
* [Cross Browsing](#cross-browsing)

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

프로그래밍 언어에서 함수 호출의 아규먼트(argument)의 순서를 언제 결정하고 함수에 어떤 종류의 값을 통과시킬지 결정하는 것

함수 실행 시 인자로 무엇을 던지느냐에 따라 함수가 어떻게 실행될지 결정하는 것


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