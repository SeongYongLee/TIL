## [1차] 프렌즈4블록

- [2018 KAKAO BLIND RECRUITMENT > [1차] 프렌즈4블록](https://programmers.co.kr/learn/courses/30/lessons/17679)

```js
function solution(m, n, board) {
  board = board.map((b) => b.split(""));

  while (true) {
    let erase = [];

    for (let i = 1; i < m; i++) {
      for (let j = 1; j < n; j++) {
        if (
          board[i][j] &&
          board[i][j] === board[i][j - 1] &&
          board[i][j] === board[i - 1][j - 1] &&
          board[i][j] === board[i - 1][j]
        ) {
          erase.push([i, j]);
        }
      }
    }

    if (!erase.length) return [].concat(...board).filter((v) => !v).length;

    erase.forEach((e) => {
      board[e[0]][e[1]] = 0;
      board[e[0]][e[1] - 1] = 0;
      board[e[0] - 1][e[1] - 1] = 0;
      board[e[0] - 1][e[1]] = 0;
    });

    for (let i = m - 1; i > 0; i--) {
      if (!board[i].filter((v) => !v).length) continue;

      for (let j = 0; j < n; j++) {
        for (let k = i - 1; !board[i][j] && k >= 0; k--) {
          if (board[k][j]) {
            board[i][j] = board[k][j];
            board[k][j] = 0;
            break;
          }
        }
      }
    }
  }
}

console.log(solution(4, 5, ["CCBDE", "AAADE", "AAABF", "CCBBF"]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
