## 퍼즐 조각 채우기

[위클리 챌린지 > 3주차 > 퍼즐 조각 채우기](https://programmers.co.kr/learn/courses/30/lessons/84021)

```js
// 1
// function solution(game_board, table) {
//     const getBlock = (stack, array) => {
//         const blocks = [];

//         while (stack.length) {
//             const block = stack.pop();
//             array[block[0]][block[1]] = 0;
//             blocks.push([block[0], block[1]]);
//             if (array[block[0] + 1]?.[block[1]])
//                 stack.push([block[0] + 1, block[1]]);

//             if (array[block[0] - 1]?.[block[1]])
//                 stack.push([block[0] - 1, block[1]]);

//             if (array[block[0]][block[1] + 1])
//                 stack.push([block[0], block[1] + 1]);

//             if (array[block[0]][block[1] - 1])
//                 stack.push([block[0], block[1] - 1]);
//         }

//         return blocks;
//     };

//     const getBlockList = () => {
//         const tableblocks = [];

//         for (let i = 0; i < table.length; i++) {
//             for (let j = 0; j < table.length; j++) {
//                 if (table[i][j]) tableblocks.push(getBlock([[i, j]], table));
//             }
//         }

//         return tableblocks
//             .sort((a, b) => a[1] - b[1])
//             .map((block) =>
//                 block.map((b) => [b[0] - block[0][0], b[1] - block[0][1]])
//             );
//     };

//     const fillPuzzle = () => {
//         const temp = [
//             {
//                 count: 0,
//                 game_board: game_board.map((board) =>
//                     board.map((b) => (b ? 0 : 1))
//                 ),
//                 rotateCount: 0,
//                 x: 0,
//                 y: 0,
//                 blockList,
//             },
//         ];

//         const fillBlock = ({
//             count,
//             game_board,
//             rotateCount,
//             x,
//             y,
//             blockList,
//         }) => {
//             let addTemp = false;
//             const gameBoardSlice = JSON.parse(JSON.stringify(game_board));
//             const block = getBlock([[x, y]], gameBoardSlice);
//             outer: for (let i = 0; i < blockList.length; i++) {
//                 if (block.length === blockList[i].length) {
//                     // console.log(blockList[i], block, x, y);
//                     for (let j = 0; j < block.length; j++) {
//                         const blockX = block[j][0] - x;
//                         const blockY = block[j][1] - y;
//                         if (
//                             !blockList[i].filter(
//                                 (b) => b[0] === blockX && b[1] === blockY
//                             ).length
//                         )
//                             continue outer;
//                     }
//                     console.log(gameBoardSlice, blockList[i], block);
//                     const blockListSlice = blockList.slice();
//                     blockListSlice.splice(i, 1);
//                     temp.push({
//                         count: count + blockList[i].length,
//                         game_board: gameBoardSlice,
//                         rotateCount,
//                         x,
//                         y,
//                         blockList: blockListSlice,
//                     });
//                     addTemp = true;
//                 }
//             }
//             return addTemp;
//         };

//         outer: while (temp.length) {
//             const next = temp.pop();
//             console.log(next);
//             for (next.rotateCount; next.rotateCount < 4; next.rotateCount++) {
//                 for (next.x; next.x < next.game_board.length; next.x++) {
//                     for (next.y; next.y < next.game_board.length; next.y++) {
//                         if (next.game_board[next.x][next.y] && fillBlock(next))
//                             continue outer;
//                     }
//                     next.y = 0;
//                 }
//                 for (let i = 0; i < next.game_board.length / 2; i++) {
//                     for (let j = 0; j < next.game_board.length; j++) {
//                         let temp = next.game_board[i][j];
//                         next.game_board[i][j] =
//                             next.game_board[next.game_board.length - i - 1][j];
//                         next.game_board[next.game_board.length - i - 1][j] =
//                             temp;
//                     }
//                 }
//                 for (let i = 0; i < next.game_board.length; i++) {
//                     for (let j = i; j < next.game_board.length; j++) {
//                         let temp = next.game_board[i][j];
//                         next.game_board[i][j] = next.game_board[j][i];
//                         next.game_board[j][i] = temp;
//                     }
//                 }
//                 next.x = 0;
//             }
//             if (next.count > answer) answer = next.count;
//         }
//     };

//     let answer = 0;
//     const blockList = getBlockList();
//     fillPuzzle();

//     return answer;
// }

// 2 - Refactoring
function solution(game_board, table) {
  const getBlock = (stack, array) => {
    const blocks = [];

    while (stack.length) {
      const block = stack.pop();
      if (array[block[0]][block[1]]) {
        blocks.push([block[0], block[1]]);
        array[block[0]][block[1]] = 0;

        if (array[block[0] + 1] && array[block[0] + 1][block[1]])
          stack.push([block[0] + 1, block[1]]);

        if (array[block[0] - 1] && array[block[0] - 1][block[1]])
          stack.push([block[0] - 1, block[1]]);

        if (array[block[0]][block[1] + 1]) stack.push([block[0], block[1] + 1]);

        if (array[block[0]][block[1] - 1]) stack.push([block[0], block[1] - 1]);
      }
    }

    return blocks;
  };

  const getBlockList = () => {
    const tableblocks = [];

    for (let i = 0; i < table.length; i++) {
      for (let j = 0; j < table.length; j++) {
        if (table[i][j]) tableblocks.push(getBlock([[i, j]], table));
      }
    }

    return tableblocks
      .sort((a, b) => a[1] - b[1])
      .map((block) =>
        block.map((b) => [b[0] - block[0][0], b[1] - block[0][1]]),
      );
  };

  const fillPuzzle = (blockList) => {
    let answer = 0;
    let gameBoard = game_board.map((board) => board.map((b) => (b ? 0 : 1)));

    const tryFillBlock = (board, x, y) => {
      const gameBoardSlice = JSON.parse(JSON.stringify(board));
      const block = getBlock([[x, y]], gameBoardSlice);
      outer: for (let i = 0; i < blockList.length; i++) {
        if (block.length === blockList[i].length) {
          for (let j = 0; j < block.length; j++) {
            const blockX = block[j][0] - x;
            const blockY = block[j][1] - y;
            if (
              !blockList[i].filter((b) => b[0] === blockX && b[1] === blockY)
                .length
            )
              continue outer;
          }
          answer += blockList[i].length;
          blockList.splice(i, 1);
          return gameBoardSlice;
        }
      }
      return gameBoard;
    };

    for (let rotateCount = 0; rotateCount < 4; rotateCount++) {
      for (let x = 0; x < gameBoard.length; x++) {
        for (let y = 0; y < gameBoard.length; y++) {
          if (gameBoard[x][y]) {
            gameBoard = tryFillBlock(gameBoard, x, y);
          }
        }
      }
      for (let i = 0; i < gameBoard.length / 2; i++) {
        for (let j = 0; j < gameBoard.length; j++) {
          let temp = gameBoard[i][j];
          gameBoard[i][j] = gameBoard[gameBoard.length - i - 1][j];
          gameBoard[gameBoard.length - i - 1][j] = temp;
        }
      }
      for (let i = 0; i < gameBoard.length; i++) {
        for (let j = i; j < gameBoard.length; j++) {
          let temp = gameBoard[i][j];
          gameBoard[i][j] = gameBoard[j][i];
          gameBoard[j][i] = temp;
        }
      }
    }

    return answer;
  };

  return fillPuzzle(getBlockList());
}

console.log(
  solution(
    [
      [1, 1, 0, 0, 1, 0],
      [0, 0, 1, 0, 1, 0],
      [0, 1, 1, 0, 0, 1],
      [1, 1, 0, 1, 1, 1],
      [1, 0, 0, 0, 1, 0],
      [0, 1, 1, 1, 0, 0],
    ],
    [
      [1, 0, 0, 1, 1, 0],
      [1, 0, 1, 0, 1, 0],
      [0, 1, 1, 0, 1, 1],
      [0, 0, 1, 0, 0, 0],
      [1, 1, 0, 1, 1, 0],
      [0, 1, 0, 0, 0, 0],
    ],
  ),
);
console.log(
  solution(
    [
      [0, 0, 0],
      [1, 1, 0],
      [1, 1, 1],
    ],
    [
      [1, 1, 1],
      [1, 0, 0],
      [0, 0, 0],
    ],
  ),
);
console.log(
  solution(
    [
      [0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0],
      [1, 1, 1, 1, 1, 1, 0, 0, 0, 1, 0, 0],
      [0, 0, 0, 0, 0, 1, 0, 1, 0, 1, 1, 0],
      [1, 0, 1, 1, 1, 0, 1, 0, 1, 0, 0, 1],
      [0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0],
      [0, 0, 1, 1, 1, 0, 1, 0, 1, 1, 0, 1],
      [0, 1, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0],
      [0, 0, 1, 0, 1, 0, 0, 1, 1, 1, 0, 0],
      [1, 1, 0, 0, 1, 0, 0, 1, 1, 1, 1, 0],
      [0, 0, 1, 1, 0, 1, 0, 1, 1, 1, 0, 0],
      [0, 0, 1, 0, 0, 1, 0, 1, 1, 0, 1, 1],
      [0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0],
    ],
    [
      [1, 1, 1, 0, 1, 1, 1, 0, 0, 0, 1, 1],
      [1, 1, 0, 0, 0, 0, 1, 1, 1, 0, 1, 1],
      [1, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0],
      [0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 0, 0],
      [1, 1, 0, 1, 0, 0, 0, 1, 1, 1, 0, 0],
      [1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0],
      [1, 0, 0, 1, 0, 1, 1, 1, 0, 0, 0, 1],
      [1, 1, 0, 1, 0, 1, 1, 1, 0, 0, 0, 1],
      [0, 0, 0, 1, 1, 0, 0, 0, 1, 1, 0, 1],
      [1, 1, 0, 1, 1, 0, 1, 0, 0, 1, 0, 1],
      [1, 1, 1, 0, 0, 0, 1, 0, 1, 1, 0, 1],
      [1, 0, 0, 1, 1, 1, 1, 0, 0, 1, 0, 1],
    ],
  ),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
