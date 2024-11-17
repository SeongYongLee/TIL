## 행렬의 덧셈

[연습문제 > 행렬의 덧셈](https://programmers.co.kr/learn/courses/30/lessons/12950)

```js
function solution(arr1, arr2) {
  return arr1.map((arr, i) => arr.map((a, j) => a + arr2[i][j]));
}

console.log(
  solution(
    [
      [1, 2],
      [2, 3],
    ],
    [
      [3, 4],
      [5, 6],
    ],
  ),
);
console.log(solution([[1], [2]], [[3], [4]]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
