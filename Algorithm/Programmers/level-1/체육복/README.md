## 체육복

[탐욕법(Greedy) > 체육복](https://programmers.co.kr/learn/courses/30/lessons/42862)

```js
function solution(n, lost, reserve) {
  return lost.reduce((r, c) => {
    let a = reserve.indexOf(c);
    if (a !== -1) {
      reserve.splice(a, 1);
      return r;
    }
    a = reserve.indexOf(c - 1);
    if (a !== -1) {
      reserve.splice(a, 1);
      return r;
    }
    a = reserve.indexOf(c + 1);
    if (a !== -1 && lost.indexOf(c + 1) === -1) {
      reserve.splice(a, 1);
      return r;
    }
    return --r;
  }, n);
}

console.log(solution(5, [2, 4], [1, 3, 5]));
console.log(solution(5, [2, 4], [3]));
console.log(solution(3, [3], [1]));
console.log(solution(4, [4, 2], [1, 3]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
