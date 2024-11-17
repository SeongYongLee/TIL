## 순위

[그래프 > 순위](https://programmers.co.kr/learn/courses/30/lessons/49191)

```js
function solution(n, results) {
  const loseList = new Array(n + 1).fill().map(() => new Set());
  const winList = new Array(n + 1).fill().map(() => new Set());

  for (let i = 0; i < results.length; i++) {
    winList[results[i][0]].add(results[i][1]);
    loseList[results[i][1]].add(results[i][0]);
  }

  for (let i = 0; i < n + 1; i++) {
    for (const first of loseList[i]) {
      for (const j of loseList[first]) {
        if (i !== j) loseList[i].add(j);
      }
    }
    for (const first of winList[i]) {
      for (const j of winList[first]) {
        if (i !== j) winList[i].add(j);
      }
    }
  }

  return winList.reduce(
    (r, _, i) => (winList[i].size + loseList[i].size === n - 1 ? r + 1 : r),
    0,
  );
}

console.log(
  solution(5, [
    [4, 3],
    [4, 2],
    [3, 2],
    [1, 2],
    [2, 5],
  ]),
);

console.log(
  solution(5, [
    [1, 2],
    [2, 3],
    [3, 4],
    [4, 5],
  ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
