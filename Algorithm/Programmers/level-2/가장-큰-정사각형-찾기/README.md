## 가장 큰 정사각형 찾기

[연습문제 > 가장 큰 정사각형 찾기](https://programmers.co.kr/learn/courses/30/lessons/12905)

```js
// 1 - 효율성 탈락
// function solution(board) {
//     let answer = 0;

//     for (let i = 0; i < board.length - answer; i++) {
//         for (let j = 0; j < board[i].length - answer; j++) {
//             if (board[i][j]) {
//                 let temp = isSquare(i, j, 1);
//                 answer = answer > temp ? answer : temp;
//             }
//         }
//     }

//     function isSquare(x, y, n) {
//         if (board[x + n] && board[x + n][y] && board[x][y + n]) {
//             for (let i = x; i < x + n; i++) {
//                 if (!board[i][y + n]) return n;
//             }
//             for (let i = y; i < y + n; i++) {
//                 if (!board[x + n][i]) return n;
//             }
//             if (!board[x + n][y + n]) return n;
//             return isSquare(x, y, ++n);
//         } else return n;
//     }

//     return Math.pow(answer, 2);
// }

// 2 - 효율성 탈락
// function solution(board) {
//     function isSquare(n) {
//         for (let x = 0; x <= board.length - n; x++) {
//             for (let y = 0; y <= board[0].length - n; y++) {
//                 let noZero = true;

//                 for (let z = 0; z < n; z++) {
//                     if (board[x + z].slice().splice(y, n).indexOf(0) !== -1) {
//                         noZero = false;
//                         break;
//                     }
//                 }

//                 if (noZero) return n;
//             }
//         }
//         return isSquare(n - 1);
//     }

//     return Math.pow(isSquare(board[0].length < board.length ? board[0].length : board.length), 2);
// }

// 3
function solution(board) {
  const x = board[0].length;
  const y = board.length;
  let answer = 0;

  if (x === 1) {
    for (const i of board) {
      if (i[0]) return 1;
    }
    return 0;
  }

  if (y === 1) {
    return board[0].indexOf(1) === -1 ? 0 : 1;
  }

  for (let i = 1; i < y; i++) {
    for (let j = 1; j < x; j++) {
      if (board[i][j] > 0) {
        board[i][j] =
          Math.min(board[i - 1][j - 1], board[i][j - 1], board[i - 1][j]) + 1;
      }
      if (answer < board[i][j]) {
        answer = board[i][j];
      }
    }
  }

  return Math.pow(answer, 2);
}

console.log(solution([[1], [1]]));
console.log(
  solution([
    [0, 0, 1, 1, 0],
    [1, 1, 1, 1, 1],
    [1, 1, 1, 1, 1],
    [1, 1, 1, 1, 1],
    [0, 1, 1, 1, 1],
  ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
