## x만큼 간격이 있는 n개의 숫자

[연습문제 > x만큼 간격이 있는 n개의 숫자](https://programmers.co.kr/learn/courses/30/lessons/12954)

```js
function solution(x, n) {
  return Array(n)
    .fill(x)
    .map((v, i) => v * (i + 1));
}

console.log(solution(2, 5));
console.log(solution(4, 3));
console.log(solution(-4, 2));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
