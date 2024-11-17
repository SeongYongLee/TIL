## 카펫

[완전탐색 > 카펫](https://programmers.co.kr/learn/courses/30/lessons/42842)

```js
function solution(brown, yellow) {
  const total = brown + yellow;
  let i = 2;

  while (i++) {
    const j = total / i;

    if (Number.isInteger(j) && (i + j - 2) * 2 === brown) {
      return i > j ? [i, j] : [j, i];
    }
  }
}

console.log(solution(10, 2));
console.log(solution(8, 1));
console.log(solution(24, 24));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
