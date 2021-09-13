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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/JavaScript)