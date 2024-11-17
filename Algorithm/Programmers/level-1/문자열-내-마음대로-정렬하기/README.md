## 문자열 내 마음대로 정렬하기

[연습문제 > 문자열 내 마음대로 정렬하기](https://programmers.co.kr/learn/courses/30/lessons/12915)

```js
function solution(strings, n) {
  return strings.sort((a, b) =>
    a[n] === b[n] ? (a > b ? 1 : -1) : a[n] > b[n] ? 1 : -1,
  );
}

console.log(solution(["sun", "bed", "car"], 1));
console.log(solution(["abce", "abcd", "cdx"], 2));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
