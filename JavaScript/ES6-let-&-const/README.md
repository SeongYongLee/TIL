# ES6 - let & const

## var 키워드로 선언된 변수의 문제점

ES5에서 변수를 선언할 수 있는 유일한 방법은 var 키워드를 사용하는 것이다. var 키워드로 선언된 변수는 아래와 같은 특징을 갖는다. 이는 다른 C-family 언어와는 차별되는 특징(설계상 오류)으로 주의를 기울이지 않으면 심각한 문제를 발생시킨다.

1. 함수 레벨 스코프(Function-level scope)
    - 전역 변수의 남발
    - for loop 초기화식에서 사용한 변수를 for loop 외부 또는 전역에서 참조할 수 있다.
    - 변수의 유효 범위(scope)는 좁을수록 좋다.
2. var 키워드 생략 허용
    - 의도하지 않은 변수의 전역화
3. 중복 선언 허용
    - 의도하지 않은 변수값 변경
4. 변수 호이스팅
    - 변수를 선언하기 전에 참조가 가능하다.

대부분의 문제는 전역 변수로 인해 발생한다.

전역 변수는 간단한 애플리케이션의 경우, 사용이 편리한 면이 있지만 불가피한 상황을 제외하고 사용을 억제해야 한다. 전역 변수는 유효 범위(scope)가 넓어서 어디에서 어떻게 사용될 지 파악하기 힘들다. 이는 의도치 않은 변수의 변경이 발생할 수 있는 가능성이 증가한다. 또한 여러 함수와 상호 의존하는 등 부수 효과(side effect)가 있을 수 있어서 복잡성이 증가한다.

ES6는 이러한 var의 단점을 보완하기 위해 let과 const 키워드를 도입하였다. ES6에서 새로 추가된 변수(let) 및 상수(const) 선언 방식이다.

const 식별자로 선언된 배열이나 객체 같은경우, 일종의 객체타입이라는 자료형을 유지하기 위한 수단으로도 사용된다.

var를 쓰면 혼란스러운 코드가 생길 수 있다는 것을 알았지만 var에 대해서도 알고있어야 한다. 아직 var를 쓰는 코드는 많으며 ES5로 트랜스컴파일을 해야하는 경우가 있기 때문이다.

## var와 차이점

### 변수 선언 방식

var - 재할당, 재선언 가능

let - 재할당 가능, 재선언 불가

const - 재할당, 재선언 불가

```jsx
var name = 'bathingape'
console.log(name) // bathingape

var name = 'javascript'
console.log(name) // javascript

let name = 'bathingape'
console.log(name) // bathingape

let name = 'javascript'
console.log(name) 
// Uncaught SyntaxError: Identifier 'name' has already been declared

const name = 'bathingape'
console.log(name) // bathingape

const name = 'javascript'
console.log(name) 
// Uncaught SyntaxError: Identifier 'name' has already been declared

name = 'react'
console.log(name) 
//Uncaught TypeError: Assignment to constant variable.
```

### 호이스팅

모든 선언을 호이스팅 하지만 let, const로 선언된 변수는 선언문 이전에 참조하면 참조 에러(ReferenceError)가 발생한다.

스코프의 시작에서 변수의 선언까지 일시적 사각지대(Temporal Dead Zone; TDZ)에 빠지기 때문이다.

* [Hoisting](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/Hoisting)

### 스코프

var - 함수 스코프

let, const - 블록 스코프

* [Scope](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/Scope)

## 결론

우리가 작성하는 코드는 변경해서는 안 되는 변수가 많기에 const를 최대한 사용 한다. 재할당이 필요한 경우에 한정해 var 대신 let 을 사용하여 변수의 스코프는 최대한 좁게 만든다.

## Reference

- [https://velog.io/@bathingape/JavaScript-var-let-const-차이점](https://velog.io/@bathingape/JavaScript-var-let-const-%EC%B0%A8%EC%9D%B4%EC%A0%90)
- [https://poiemaweb.com/js-data-type-variable](https://poiemaweb.com/js-data-type-variable)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Vue)