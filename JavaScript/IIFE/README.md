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

TODO : 

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/FrontEnd)