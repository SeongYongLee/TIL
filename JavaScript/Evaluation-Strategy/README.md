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

TODO : [Immutable](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/Immutable)

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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/FrontEnd)