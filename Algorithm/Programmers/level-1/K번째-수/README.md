## K번째 수

[정렬 > K번째 수](https://programmers.co.kr/learn/courses/30/lessons/42748)

```js
function solution(array, commands) {
  return commands.reduce(
    (answer, c) => [
      ...answer,
      array.slice(c[0] - 1, c[1]).sort((x, y) => x - y)[c[2] - 1],
    ],
    [],
  );
}

console.log(
  solution(
    [1, 5, 2, 6, 3, 7, 4],
    [
      [2, 5, 3],
      [4, 4, 1],
      [1, 7, 3],
    ],
  ),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
