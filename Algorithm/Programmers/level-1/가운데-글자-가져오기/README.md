## 가운데 글자 가져오기

[연습문제 > 가운데 글자 가져오기](https://programmers.co.kr/learn/courses/30/lessons/12903)

```js
function solution(s) {
  const length = s.length;
  const mid = length / 2;

  return s.slice(length % 2 === 0 ? mid - 1 : mid, mid + 1);
}

console.log(solution("abcde"));
console.log(solution("qwer"));
console.log(solution("abcdef"));
console.log(solution("a"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
