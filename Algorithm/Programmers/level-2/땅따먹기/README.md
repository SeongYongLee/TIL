## 땅따먹기

[연습문제 > 땅따먹기](https://programmers.co.kr/learn/courses/30/lessons/12913)

```js
function solution(land) {
  const size = 4;
  const answer = land[0];

  for (let i = 1; i < land.length; i++) {
    const tempI = answer.slice();
    for (let j = 0; j < size; j++) {
      const tempJ = tempI.slice();
      tempJ.splice(j, 1);
      answer[j] = land[i][j] + Math.max(...tempJ);
    }
  }

  return Math.max(...answer);
}

console.log(
  solution([
    [1, 2, 3, 5],
    [5, 6, 7, 8],
    [4, 3, 2, 1],
  ]),
);
console.log(
  solution([
    [4, 3, 2, 1],
    [2, 2, 2, 1],
    [6, 6, 6, 4],
    [8, 7, 6, 5],
  ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
