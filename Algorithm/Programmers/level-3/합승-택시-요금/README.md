## 합승 택시 요금

[2021 KAKAO BLIND RECRUITMENT > 합승 택시 요금](https://programmers.co.kr/learn/courses/30/lessons/72413)

```js
// Floyd–Warshall (플로이드-와샬)
function solution(n, s, a, b, fares) {
  const table = new Array(n)
    .fill()
    .map((_, i) => new Array(n).fill(Infinity).fill(0, i, i + 1));

  for (let i = 0; i < fares.length; i++) {
    table[fares[i][0] - 1][fares[i][1] - 1] = fares[i][2];
    table[fares[i][1] - 1][fares[i][0] - 1] = fares[i][2];
  }

  for (let m = 0; m < n; m++) {
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < n; j++) {
        const sum = table[i][m] + table[m][j];
        if (table[i][j] > sum) table[i][j] = sum;
      }
    }
  }

  let answer = table[s - 1][a - 1] + table[s - 1][b - 1];

  for (let i = 1; i < n; i++) {
    const sum = table[s - 1][i] + table[i][a - 1] + table[i][b - 1];
    if (answer > sum) answer = sum;
  }

  return answer;
}

console.log(
  solution(6, 4, 6, 2, [
    [4, 1, 10],
    [3, 5, 24],
    [5, 6, 2],
    [3, 1, 41],
    [5, 1, 24],
    [4, 6, 50],
    [2, 4, 66],
    [2, 3, 22],
    [1, 6, 25],
  ]),
);
console.log(
  solution(7, 3, 4, 1, [
    [5, 7, 9],
    [4, 6, 4],
    [3, 6, 1],
    [3, 2, 3],
    [2, 1, 6],
  ]),
);
console.log(
  solution(6, 4, 5, 6, [
    [2, 6, 6],
    [6, 3, 7],
    [4, 6, 7],
    [6, 5, 11],
    [2, 5, 12],
    [5, 3, 20],
    [2, 4, 8],
    [4, 3, 9],
  ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
