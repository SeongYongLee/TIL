# 변수의 선언과 할당

## 변수

변수(Variable)는 프로그램에서 사용되는 데이터를 일정 기간 동안 기억하여 필요한 때에 다시 사용하기 위해 데이터에 고유의 이름인 식별자(identifier)를 명시한 것이다. 변수에 명시한 고유한 식별자를 변수명이라 하고 변수로 참조할 수 있는 데이터를 변수값이라 한다.

식별자는 어떤 대상을 유일하게 식별할 수 있는 이름을 말한다. 식별자에는 변수명, 함수명, 프로퍼티명, 클래스명 등이 있다.

### 변수의 선언

예를 들어 반지름의 길이가 2인 원의 넓이를 구해보자. 이때 원주율은 3.141592653589793라고 하자.

```
3.141592653589793 * 2 * 2; // 12.566370614359172
```

원의 넓이를 구하였으나 그 결과를 기억할 수 없다. 만약에 원의 넓이를 다시 사용해야 한다면 다시 구해야 한다. 변수를 사용하여 원의 넓이를 기억(캐싱)하고 기억된 원의 넓이를 재사용하여 높이가 5인 원기둥의 부피를 구해보자.

```
var circleArea = 3.141592653589793 * 2 * 2;
var cylinderVolume = circleArea * 5;
```

원주율 3.141592653589793은 재사용할 가능성이 크므로 변수에 저장하도록 하자.

원주율은 변하지 않는 상수이지만 자바스크립트는 상수를 별도 지원하지 않으므로 변수 이름을 대문자로 하여 상수임을 암시하도록 하자.
`원주율은 자바스크립트 빌트인 상수인 Math.PI을 통해 참조할 수 있다. 상수는 ES6의 const 키워드를 사용해 표현할 수 있다.`

* TODO : [ES6 - let & const](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/ES6-let-&-const)

그리고 반지름과 원기둥의 높이도 값의 의미를 명확히하고 변화에 대처하기 쉽도록 변수에 저장하도록 하자.

```
var PI = 3.141592653589793; // 상수
var radius = 2; // 변수
var circleArea = PI * radius * radius;
var cylinderHeight = 5;
var cylinderVolume = circleArea * cylinderHeight;
```

이처럼 변수는 애플리케이션에서 한번 쓰고 버리는 값이 아닌 값이 아닌 일정 기간 유지할 필요가 있는 값에 사용한다. 또한 변수를 사용하면 값의 의미가 명확해져서 코드의 가독성이 좋아진다.

변수의 존재 목적을 쉽게 이해할 수 있도록 의미있는 변수명을 지정하여야한다.

```
var x = 3;        // NG
var score = 100;  // OK
```

변수명은 식별자(identifier)로 불리기도 하며 명명 규칙이 존재한다.

- 반드시 영문자(특수문자 제외), underscore ( _ ), 또는 달러 기호($)로 시작하여야 한다. 이어지는 문자에는 숫자(0~9)도 사용할 수 있다.
- 자바스크립트는 대/소문자를 구별하므로 사용할 수 있는 문자는 “A” ~ “Z” (대문자)와 “a” ~ “z” (소문자)이다.

### 변수의 선언과 할당

```
var score;  // 변수의 선언
score = 80; // 값의 할당
score = 90; // 값의 재할당
score;      // 변수의 참조

// 변수의 선언과 할당
var average = (50 + 100) / 2;
var age = 30;

var person = 'Lee',
    address = 'Seoul',
    price = 200;

var price = 10;
var tax   = 1;
var total = price + tax;

// 할당하지 않은 변수
var x;
console.log(x); // undefined
console.log(y); // ReferenceError
```

**선언 (Declaration)**

변수는 `var`, `let`, `const` 키워드를 사용하여 **선언**한다. 값을 할당하기 전이다.

자바스크립트 엔진은 코드를 인터프리팅 하기 전에 그 코드를 먼저 컴파일한다.

`var a = 2;`를 하나의 구문으로 생각할 수도 있지만, 자바스크립트는 `var a;` `a = 2;` 두 개의 구문으로 분리하여 본다.

변수 선언(생성) 단계와 초기화 및 할당 단계로 나누고, 선언 단계에서는 그 선언이 소스코드의 어디에 위치하든 해당 스코프의 컴파일단계에서 처리한다. 선언 단계가 스코프의 꼭대기로 호이스팅 되는 작업이라고 볼 수 있다.

* [Hoisting](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/Hoisting)

**초기화 (Initialization)**

변수 객체(Variable Object)에 등록된 변수를 메모리에 할당한다. 이 단계에서 변수는 undefined로 **초기화**된다.

**할당 (Assignment)**

할당 연산자(등호, =, equal sign)을 사용해 특정 변수에 값을 **할당**한다. 할당 구문은 런타임 과정에서 이루어진다.

* TODO : [JS Runtime, Event Loop](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/JS-Runtime-Event-Loop)

값을 할당하지 않은 변수 즉 선언만 되어 있는 변수는 `undefined`로 초기값을 갖는다. 선언하지 않은 변수에 접근하면 `ReferenceError`가 발생한다.

**참조**

사람을 고유한 이름으로 구별하듯이 변수도 사람이 이해할 수 있는 언어로 지정한 고유한 식별자(변수명)에 의해 구별하여 **참조**할 수 있다.

데이터는 메모리에 저장되어 있고 데이터를 참조하려면 데이터가 저장된 메모리 상의 주소(address)를 알아야 한다.

식별자는 데이터가 저장된 메모리 상의 주소를 기억한다. 따라서 식별자를 통해 메모리에 저장된 값을 참조할 수 있다. 또한 변수명을 통해 데이터의 의미를 명확히 할 수 있어 코드의 가독성이 좋아지는 효과도 있다.

### 변수의 중복 선언

var 키워드로 선언한 변수는 중복 선언이 가능하다. 다시 말해 변수명이 같은 변수를 중복해 선언해도 에러가 발생하지 않는다.

```
var x = 1;
console.log(x); // 1

// 변수의 중복 선언
var x = 100;
console.log(x); // 100

```

위 예제의 변수 x는 중복 선언되었다. 이처럼 변수를 중복 선언하면 에러없이 이전 변수의 값을 덮어쓴다. 만약 동일한 변수명이 선언되어 있는 것을 모르고 변수를 중복 선언했다면 의도치 않게 변수의 값을 변경하는 부작용을 발생시킨다. 따라서 변수의 중복 선언은 문법적으로 허용되지만 사용하지 않는 것이 좋다.
`ES6의 let, const 키워드는 재선언이 불가능하다.`

* TODO : [ES6 - let & const](https://github.com/SeongYongLee/TIL/tree/main/JavaScript/ES6-let-&-const)

## Reference

- [https://poiemaweb.com/js-data-type-variable](https://poiemaweb.com/js-data-type-variable)
- [https://meetup.toast.com/posts/86](https://meetup.toast.com/posts/86)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/FrontEnd)