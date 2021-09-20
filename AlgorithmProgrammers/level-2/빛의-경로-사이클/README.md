## 빛의 경로 사이클

[월간 코드 챌린지 시즌2 > 빛의 경로 사이클](https://programmers.co.kr/learn/courses/30/lessons/86052)

``` js
// 1 - 잘못된 풀이 접근
// function solution(grid) {
//     const answer = [];
//     const gridXLength = grid[0].length;
//     const gridYLength = grid.length;
//     const inLeft = Array(gridYLength).fill(0);
//     const inRight = Array(gridYLength).fill(0);
//     const inTop = Array(gridXLength).fill(0);
//     const inBottom = Array(gridXLength).fill(0);
//     const moveTopToBottom = (x, y) => {
//         x += 1;
//         if (x === gridYLength) {
//             x = 0;
//             inTop[y] = true;
//         }
//         return x;
//     };
//     const moveBottomToTop = (x, y) => {
//         x -= 1;
//         if (x === -1) {
//             x = gridYLength - 1;
//             inBottom[y] = true;
//         }
//         return x;
//     };
//     const moveLeftToRight = (x, y) => {
//         y += 1;
//         if (y === gridXLength) {
//             y = 0;
//             inLeft[x] = true;
//         }
//         return y;
//     };
//     const moveRightToLeft = (x, y) => {
//         y -= 1;
//         if (y === -1) {
//             y = gridXLength - 1;
//             inRight[x] = true;
//         }
//         return y;
//     };
//     const moveLight = (x, y, entry) => {
//         const first = [x, y, entry];
//         let count = 0;
//         while (1) {
//             console.log(x, y, entry);
//             console.log(inLeft, inRight, inTop, inBottom);
//             switch (grid[x][y]) {
//                 case 'S':
//                     switch (entry) {
//                         case 'left':
//                             y = moveLeftToRight(x, y);
//                             break;
//                         case 'right':
//                             y = moveRightToLeft(x, y);
//                             break;
//                         case 'top':
//                             x = moveTopToBottom(x, y);
//                             break;
//                         case 'bottom':
//                             x = moveBottomToTop(x, y);
//                             break;
//                     }
//                     break;
//                 case 'L':
//                     switch (entry) {
//                         case 'left':
//                             entry = 'bottom';
//                             x = moveBottomToTop(x, y);
//                             break;
//                         case 'right':
//                             entry = 'top';
//                             x = moveTopToBottom(x, y);
//                             break;
//                         case 'top':
//                             entry = 'left';
//                             y = moveLeftToRight(x, y);
//                             break;
//                         case 'bottom':
//                             entry = 'right';
//                             y = moveRightToLeft(x, y);
//                             break;
//                     }
//                     break;
//                 case 'R':
//                     switch (entry) {
//                         case 'left':
//                             entry = 'top';
//                             x = moveTopToBottom(x, y);
//                             break;
//                         case 'right':
//                             entry = 'bottom';
//                             x = moveBottomToTop(x, y);
//                             break;
//                         case 'top':
//                             entry = 'right';
//                             y = moveRightToLeft(x, y);
//                             break;
//                         case 'bottom':
//                             entry = 'left';
//                             y = moveLeftToRight(x, y);
//                             break;
//                     }
//                     break;
//             }
//             count++;
//             if (first[0] === x && first[1] === y && first[2] === entry)
//                 return count;
//         }
//     };

//     for (let i = 0; i < gridYLength; i++) {
//         if (inLeft[i]) continue;
//         inLeft[i] = true;
//         answer.push(moveLight(i, 0, 'left'));
//     }

//     for (let i = 0; i < gridYLength; i++) {
//         if (inRight[i]) continue;
//         inRight[i] = true;
//         answer.push(moveLight(i, 0, 'right'));
//     }

//     for (let i = 0; i < gridXLength; i++) {
//         if (inTop[i]) continue;
//         inTop[i] = true;
//         answer.push(moveLight(0, i, 'top'));
//     }

//     for (let i = 0; i < gridXLength; i++) {
//         if (inBottom[i]) continue;
//         inBottom[i] = true;
//         answer.push(moveLight(0, i, 'bottom'));
//     }

//     return answer.sort();
// }

// console.log(solution(['SL', 'LR']));
// console.log(solution(['S']));
// console.log(solution(['R', 'R']));
// console.log(solution(['RR', 'RR']));
// console.log(solution(['S', 'S', 'S', 'S']));
// console.log(solution(['SRLS']));
// console.log(solution(['R']));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)