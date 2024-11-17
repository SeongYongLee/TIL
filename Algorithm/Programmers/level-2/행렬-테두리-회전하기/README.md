## 행렬 테두리 회전하기

[2021 Dev-Matching: 웹 백엔드 개발자(상반기) > 행렬 테두리 회전하기](https://programmers.co.kr/learn/courses/30/lessons/77485)

```js
// 1
function solution(rows, columns, queries) {
  const answer = [];
  const matrix = new Array(rows)
    .fill()
    .map((r, i) =>
      new Array(columns).fill().map((c, j) => i * columns + j + 1),
    );

  for (let i = 0; i < queries.length; i++) {
    const setNum = (tempNum) => {
      matrix[row][column] = lastNum;
      lastNum = tempNum;
      if (minNum > lastNum) minNum = lastNum;
    };

    const rowDiff = queries[i][2] - queries[i][0];
    const columnDiff = queries[i][3] - queries[i][1];
    let row = queries[i][0] - 1;
    let column = queries[i][1] - 1;
    let lastNum = matrix[row][column];
    let minNum = lastNum;

    // right
    for (let i = 0; i < columnDiff; i++) {
      setNum(matrix[row][++column]);
    }
    // down
    for (let i = 0; i < rowDiff; i++) {
      setNum(matrix[++row][column]);
    }
    // left
    for (let i = 0; i < columnDiff; i++) {
      setNum(matrix[row][--column]);
    }
    // up
    for (let i = 0; i < rowDiff; i++) {
      setNum(matrix[--row][column]);
    }

    answer.push(minNum);
  }

  return answer;
}

// 2 - Refactoring (더 느려짐)
// function solution(rows, columns, queries) {
//     const matrix = new Array(rows)
//         .fill()
//         .map((r, i) => new Array(columns).fill().map((c, j) => i * columns + j + 1));

//     return queries.map((query) => {
//         const [sr, sc, er, ec] = query.map((q) => q - 1);
//         const tempNum = matrix[sr][sc];
//         let minNum = matrix[sr][sc];

//         // down
//         for (let i = sr; i < er; i++) {
//             matrix[i][sc] = matrix[i + 1][sc];
//             if (minNum > matrix[i][sc]) minNum = matrix[i][sc];
//         }
//         // right
//         for (let i = sc; i < ec; i++) {
//             matrix[er][i] = matrix[er][i + 1];
//             if (minNum > matrix[er][i]) minNum = matrix[er][i];
//         }
//         // up
//         for (let i = er; i > sr; i--) {
//             matrix[i][ec] = matrix[i - 1][ec];
//             if (minNum > matrix[i][ec]) minNum = matrix[i][ec];
//         }
//         // left
//         for (let i = ec; i > sc; i--) {
//             matrix[sr][i] = matrix[sr][i - 1];
//             if (minNum > matrix[sr][i]) minNum = matrix[sr][i];
//         }
//         matrix[sr][sc + 1] = tempNum;

//         return minNum;
//     });
// }

console.log(
  solution(6, 6, [
    [2, 2, 5, 4],
    [3, 3, 6, 6],
    [5, 1, 6, 3],
  ]),
);
console.log(
  solution(3, 3, [
    [1, 1, 2, 2],
    [1, 2, 2, 3],
    [2, 1, 3, 2],
    [2, 2, 3, 3],
  ]),
);
console.log(solution(100, 97, [[1, 1, 100, 97]]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
