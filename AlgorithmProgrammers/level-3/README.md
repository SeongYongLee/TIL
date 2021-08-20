# AlgorithmProgrammers - Level 3

* [위클리 챌린지 > 3주차 > 퍼즐 조각 채우기](#퍼즐-조각-채우기)

* [2020 KAKAO BLIND RECRUITMENT > 자물쇠와 열쇠](#자물쇠와-열쇠)

* [2021 KAKAO BLIND RECRUITMENT > 합승 택시 요금](#합승-택시-요금)

* [이분탐색 > 입국심사](#입국심사)

* [탐욕법 > 섬 연결하기](#섬-연결하기)

* [탐욕법 > 단속카메라](#단속카메라)

* [그래프 > 가장 먼 노드](#가장-먼-노드)

* [그래프 > 순위](#순위)

* [연습문제 > 2 x n 타일링](#2-x-n-타일링)

* [연습문제 > 멀리 뛰기](#멀리-뛰기)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)

## 퍼즐 조각 채우기

[위클리 챌린지 > 3주차 > 퍼즐 조각 채우기](https://programmers.co.kr/learn/courses/30/lessons/84021)

``` js
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

                if (array[block[0]][block[1] + 1])
                    stack.push([block[0], block[1] + 1]);

                if (array[block[0]][block[1] - 1])
                    stack.push([block[0], block[1] - 1]);
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
                block.map((b) => [b[0] - block[0][0], b[1] - block[0][1]])
            );
    };

    const fillPuzzle = (blockList) => {
        let answer = 0;
        let gameBoard = game_board.map((board) =>
            board.map((b) => (b ? 0 : 1))
        );

        const tryFillBlock = (board, x, y) => {
            const gameBoardSlice = JSON.parse(JSON.stringify(board));
            const block = getBlock([[x, y]], gameBoardSlice);
            outer: for (let i = 0; i < blockList.length; i++) {
                if (block.length === blockList[i].length) {
                    for (let j = 0; j < block.length; j++) {
                        const blockX = block[j][0] - x;
                        const blockY = block[j][1] - y;
                        if (
                            !blockList[i].filter(
                                (b) => b[0] === blockX && b[1] === blockY
                            ).length
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
        ]
    )
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
        ]
    )
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
        ]
    )
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-3)

</br></br>

## 자물쇠와 열쇠

[2020 KAKAO BLIND RECRUITMENT > 자물쇠와 열쇠](https://programmers.co.kr/learn/courses/30/lessons/60059)

``` js
function solution(key, lock) {
    const keyLength = key.length;
    const lockLength = lock.length;
    let rotateKey = key;

    function rotate(array) {
        return array.reduce((result, x) => {
            for (let i = 0; i < keyLength; i++) {
                result[keyLength - i - 1] = [
                    ...(result[keyLength - i - 1] || []),
                    x[i],
                ];
            }
            return result;
        }, []);
    }
    function isFull(li, lj, key, lock) {
        for (let ki = 0; ki < keyLength; ki++) {
            for (let kj = 0; kj < keyLength; kj++) {
                if (
                    li + ki >= 0 &&
                    lj + kj >= 0 &&
                    li + ki < lockLength &&
                    lj + kj < lockLength
                ) {
                    lock[li + ki][lj + kj] += key[ki][kj];
                    if (lock[li + ki][lj + kj] !== 1) return false;
                }
            }
        }
        for (let i = 0; i < lockLength; i++) {
            for (let j = 0; j < lockLength; j++) {
                if (lock[i][j] !== 1) return false;
            }
        }
        return true;
    }

    for (let i = 0; i < 4; i++) {
        for (let li = -keyLength + 1; li < lockLength; li++) {
            for (let lj = -keyLength + 1; lj < lockLength; lj++) {
                if (isFull(li, lj, rotateKey, JSON.parse(JSON.stringify(lock))))
                    return true;
            }
        }
        if (i === 3) return false;
        else rotateKey = rotate(rotateKey);
    }
}

console.log(
    solution(
        [
            [0, 0, 0],
            [1, 0, 0],
            [0, 1, 1],
        ],
        [
            [1, 1, 1],
            [1, 1, 0],
            [1, 0, 1],
        ]
    )
);
console.log(
    solution(
        [
            [0, 1, 0],
            [1, 1, 1],
            [0, 1, 1],
        ],
        [
            [1, 1, 1, 1, 1],
            [1, 1, 1, 1, 1],
            [1, 1, 1, 0, 0],
            [1, 1, 0, 0, 0],
            [1, 1, 1, 0, 1],
        ]
    )
);
console.log(
    solution(
        [
            [1, 1, 1],
            [0, 0, 1],
            [1, 1, 1],
        ],
        [
            [0, 1, 1, 1],
            [1, 1, 1, 1],
            [1, 1, 1, 1],
            [1, 1, 1, 1],
        ]
    )
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-3)

</br></br>

## 합승 택시 요금

[2021 KAKAO BLIND RECRUITMENT > 합승 택시 요금](https://programmers.co.kr/learn/courses/30/lessons/72413)

``` js
// Floyd–Warshall (플로이드-와샬)
function solution(n, s, a, b, fares) {
    const table = new Array(n).fill().map((_, i) => new Array(n).fill(Infinity).fill(0, i, i + 1));

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
    ])
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
    ])
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-3)

</br></br>

## 입국심사

[이분탐색 > 입국심사](https://programmers.co.kr/learn/courses/30/lessons/43238)

``` js
function solution(n, times) {
    times.sort((a, b) => a - b);

    const tLength = times.length;
    let left = 1;
    let right = n * times[tLength - 1];
    let answer = right;

    outer: while (left <= right) {
        const mid = parseInt((left + right) / 2);
        let count = 0;

        for (let i = 0; i < tLength; i++) {
            count += parseInt(mid / times[i]);
            if (count >= n) {
                answer = mid;
                right = mid - 1;
                continue outer;
            }
        }

        left = mid + 1;
    }

    return answer;
}

console.log(solution(5, [4, 7, 10, 11]));
console.log(solution(6, [7, 10, 100]));
console.log(solution(6, [7, 10, 11]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-3)

</br></br>

## 섬 연결하기

[탐욕법 > 섬 연결하기](https://programmers.co.kr/learn/courses/30/lessons/42861)

``` js
// 1 - 플로이드 와샬 (Floyd Warshall) - 시간 초과, 접근 방법이 잘못됨
// function solution(n, costs) {
//     const table = new Array(n)
//         .fill()
//         .map((_, i) => new Array(n).fill(Infinity).fill(0, i, i + 1));

//     let answer = Infinity;

//     for (let i = 0; i < costs.length; i++) {
//         if (table[costs[i][0]][costs[i][1]] > costs[i][2]) {
//             table[costs[i][0]][costs[i][1]] = costs[i][2];
//             table[costs[i][1]][costs[i][0]] = costs[i][2];
//         }
//     }

//     for (let m = 0; m < n; m++) {
//         for (let i = 0; i < n; i++) {
//             for (let j = 0; j < n; j++) {
//                 const sum = table[i][m] + table[m][j];
//                 if (table[i][j] > sum) table[i][j] = sum;
//             }
//         }
//     }

//     const sol = (sum, index, count, visited) => {
//         for (let i = 0; i < n; i++) {
//             if (visited[i]) continue;
//             const tempSum = sum + table[index][i];
//             if (tempSum >= answer) continue;
//             if (count === n - 1) {
//                 answer = tempSum;
//             } else {
//                 const tempVisited = visited.slice();
//                 tempVisited[i] = true;
//                 sol(tempSum, i, count + 1, tempVisited);
//             }
//         }
//     };

//     for (let i = 0; i < n; i++) {
//         const visited = new Array(n).fill(false);
//         visited[i] = true;
//         sol(0, i, 1, visited);
//     }

//     return answer;
// }

// 2 - MST 프림 알고리즘 (table)
// function solution(n, costs) {
//     const table = new Array(n)
//         .fill()
//         .map((_, i) => new Array(n).fill(Infinity).fill(0, i, i + 1));

//     let answer = 0;

//     for (let i = 0; i < costs.length; i++) {
//         if (table[costs[i][0]][costs[i][1]] > costs[i][2]) {
//             table[costs[i][0]][costs[i][1]] = costs[i][2];
//             table[costs[i][1]][costs[i][0]] = costs[i][2];
//         }
//     }

//     const visited = new Array(n).fill(false).fill(true, 0, 1);

//     for (let x = 0; x < n - 1; x++) {
//         let minNum = Infinity;
//         let minNumIndex = -1;

//         for (let i = 0; i < n; i++) {
//             if (!visited[i]) continue;
//             for (let j = 0; j < n; j++) {
//                 if (visited[j]) continue;

//                 if (minNum > table[i][j]) {
//                     minNum = table[i][j];
//                     minNumIndex = j;
//                 }
//             }
//         }
//         visited[minNumIndex] = true;
//         answer += minNum;
//     }

//     return answer;
// }

// 3 - MST 프림 알고리즘 (sort queue)
/* 
    프로그래머스 - 다른 사람의 풀이 참고
*/
function solution(n, costs) {
    costs.sort((a, b) => a[2] - b[2]);
    let [from, to, answer] = costs.shift();
    const connected = new Set([from, to]);

    while (connected.size < n) {
        const index = costs.findIndex(
            ([from, to]) =>
                (connected.has(from) && !connected.has(to)) ||
                (connected.has(to) && !connected.has(from))
        );
        let [[from, to, cost]] = costs.splice(index, 1);

        answer += cost;
        connected.add(from).add(to);
    }

    return answer;
}

console.log(
    solution(6, [
        [0, 1, 1],
        [0, 2, 2],
        [1, 2, 5],
        [1, 3, 1],
        [2, 3, 8],
        [3, 4, 20],
        [2, 5, 20],
        [4, 5, 20],
    ])
);

console.log(
    solution(5, [
        [0, 1, 5],
        [1, 2, 3],
        [2, 3, 3],
        [3, 1, 2],
        [3, 0, 4],
        [2, 4, 6],
        [4, 0, 7],
    ])
);

console.log(
    solution(5, [
        [0, 1, 1],
        [3, 4, 1],
        [1, 2, 2],
        [2, 3, 4],
    ])
);

console.log(
    solution(4, [
        [0, 1, 5],
        [1, 2, 3],
        [2, 3, 3],
        [1, 3, 2],
        [0, 3, 4],
    ])
);

console.log(
    solution(5, [
        [0, 1, 1],
        [3, 1, 1],
        [0, 2, 2],
        [0, 3, 2],
        [0, 4, 100],
    ])
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-3)

</br></br>

## 단속카메라

[탐욕법 > 단속카메라](https://programmers.co.kr/learn/courses/30/lessons/42884)

``` js
function solution(words) {
    words.sort((a, b) => (a[0] === b[0] ? a[1] - b[1] : a[0] - b[0]));

    let answer = 1;
    let index = words[0][1];

    for (let i = 1; i < words.length; i++) {
        if (index >= words[i][0]) {
            if (index > words[i][1]) index = words[i][1];
        } else {
            answer++;
            index = words[i][1];
        }
    }
    return answer;
}

console.log(
    solution([
        [-20, 15],
        [-14, -5],
        [-18, -14],
        [-18, -13],
        [-18, -16],
        [-5, -3],
    ])
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-3)

</br></br>

## 가장 먼 노드

[그래프 > 가장 먼 노드](https://programmers.co.kr/learn/courses/30/lessons/49189)

``` js
// 1 - 시간 초과
// function solution(n, edge) {
//     const visited = new Set([1]);
//     let tempVisited = new Set();

//     while (visited.size < n) {
//         tempVisited = new Set(visited);

//         for (let i = 0; i < edge.length; i++) {
//             if (tempVisited.has(edge[i][0]) && !tempVisited.has(edge[i][1])) {
//                 visited.add(edge[i][1]);
//                 edge.splice(i, 1);
//                 i--;
//             } else if (
//                 tempVisited.has(edge[i][1]) &&
//                 !tempVisited.has(edge[i][0])
//             ) {
//                 visited.add(edge[i][0]);
//                 edge.splice(i, 1);
//                 i--;
//             }
//         }
//     }

//     return visited.size - tempVisited.size;
// }

// 2 - Refactoring (시간 초과) - splice는 정말 시간 효율성이 떨어진다
// function solution(n, edge) {
//     const visited = new Set([1]);
//     let tempVisited = new Set();

//     while (visited.size < n) {
//         tempVisited = new Set(visited);

//         for (let i = 0; i < edge.length; i++) {
//             if (tempVisited.has(edge[i][0]) && !tempVisited.has(edge[i][1])) {
//                 visited.add(edge[i][1]);
//             } else if (
//                 tempVisited.has(edge[i][1]) &&
//                 !tempVisited.has(edge[i][0])
//             ) {
//                 visited.add(edge[i][0]);
//             }
//         }
//     }

//     return visited.size - tempVisited.size;
// }

// 3 - Refactoring
function solution(n, edge) {
    const edgeList = edge.reduce(
        (r, c) => {
            r[c[0]].push(c[1]);
            r[c[1]].push(c[0]);
            return r;
        },
        new Array(n + 1).fill().map(() => [])
    );

    const visited = new Set([1]);
    let lastVisited = new Set([1]);
    let tempLastVisited = new Set();

    while (visited.size < n) {
        tempLastVisited = new Set(lastVisited);
        lastVisited = new Set();

        for (let i of tempLastVisited) {
            for (let j = 0; j < edgeList[i].length; j++) {
                if (!visited.has(edgeList[i][j])) {
                    visited.add(edgeList[i][j]);
                    lastVisited.add(edgeList[i][j]);
                }
            }
        }
        // console.log(visited, lastVisited, tempLastVisited);
    }

    return lastVisited.size;
}

console.log(
    solution(6, [
        [3, 6],
        [4, 3],
        [3, 2],
        [1, 3],
        [1, 2],
        [2, 4],
        [5, 2],
    ])
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-3)

</br></br>

## 순위

[그래프 > 순위](https://programmers.co.kr/learn/courses/30/lessons/49191)

``` js
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
        0
    );
}

console.log(
    solution(5, [
        [4, 3],
        [4, 2],
        [3, 2],
        [1, 2],
        [2, 5],
    ])
);

console.log(
    solution(5, [
        [1, 2],
        [2, 3],
        [3, 4],
        [4, 5],
    ])
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-3)

</br></br>

## 2 x n 타일링

[연습문제 > 2 x n 타일링](https://programmers.co.kr/learn/courses/30/lessons/12900)

``` js
function solution(n) {
    let historyAnswer = 0;
    let answer = 1;

    for (let i = 1; i <= n; i++) {
        const tempAnswer = (historyAnswer + answer) % 1000000007;
        historyAnswer = answer;
        answer = tempAnswer;
    }

    return answer;
}

console.log(solution(4));

// 1 = 1
// 2 (1+1) = 2
// 3 (1+2) = 3
// 4 (1+3+1)= 5
// 5 (1+3+4) = 8
// 6 (1+5+6+1) = 13
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-3)

</br></br>

## 멀리 뛰기

[연습문제 > 멀리 뛰기](https://programmers.co.kr/learn/courses/30/lessons/12914)

``` js
function solution(n) {
    let historyAnswer = 0;
    let answer = 1;

    for (let i = 1; i <= n; i++) {
        const tempAnswer = (historyAnswer + answer) % 1234567;
        historyAnswer = answer;
        answer = tempAnswer;
    }

    return answer;
}

console.log(solution(4));
console.log(solution(3));

// 1 = 1
// 2 (1+1) = 2
// 3 (1+2) = 3
// 4 (1+3+1) = 5
// 5 (1+4+3) = 8
// 6
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-3)

</br></br>