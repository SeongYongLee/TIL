## 게임 맵 최단거리

[찾아라 프로그래밍 마에스터 > 게임 맵 최단거리](https://programmers.co.kr/learn/courses/30/lessons/1844)

``` js
// 1 - DFS (효율성 테스트 탈락)
// function solution(maps) {
//     let answer = Infinity;
//     const sol = (x, y, pastMaps, count) => {
//         if (x === maps.length - 1 && y === maps[0].length - 1) {
//             answer = answer < count ? answer : count;
//             return;
//         }

//         pastMaps[x][y] = 0;

//         if (pastMaps[x + 1] && pastMaps[x + 1][y]) {
//             sol(x + 1, y, JSON.parse(JSON.stringify(pastMaps)), count + 1);
//         }
//         if (pastMaps[x] && pastMaps[x][y + 1]) {
//             sol(x, y + 1, JSON.parse(JSON.stringify(pastMaps)), count + 1);
//         }
//         if (pastMaps[x - 1] && pastMaps[x - 1][y]) {
//             sol(x - 1, y, JSON.parse(JSON.stringify(pastMaps)), count + 1);
//         }
//         if (pastMaps[x] && pastMaps[x][y - 1]) {
//             sol(x, y - 1, JSON.parse(JSON.stringify(pastMaps)), count + 1);
//         }
//     };

//     sol(0, 0, JSON.parse(JSON.stringify(maps)), 1);

//     return answer === Infinity ? -1 : answer;
// }

// 2 - BFS (효율성 테스트 탈락)
// function solution(maps) {
//     let answer = 1;
//     let locaQueue = [[0, 0, JSON.parse(JSON.stringify(maps))]];

//     while (locaQueue.length) {
//         const next = [];

//         for (let i = 0; i < locaQueue.length; i++) {
//             const x = locaQueue[i][0];
//             const y = locaQueue[i][1];
//             const map = locaQueue[i][2];

//             if (x === maps.length - 1 && y === maps[0].length - 1) return answer;

//             map[x][y] = 0;

//             if (map[x + 1] && map[x + 1][y]) {
//                 next.push([x + 1, y, JSON.parse(JSON.stringify(map))]);
//             }
//             if (map[x] && map[x][y + 1]) {
//                 next.push([x, y + 1, JSON.parse(JSON.stringify(map))]);
//             }
//             if (map[x - 1] && map[x - 1][y]) {
//                 next.push([x - 1, y, JSON.parse(JSON.stringify(map))]);
//             }
//             if (map[x] && map[x][y - 1]) {
//                 next.push([x, y - 1, JSON.parse(JSON.stringify(map))]);
//             }
//         }

//         answer++;
//         locaQueue = next;
//     }

//     return -1;
// }

// 3 - BFS Refactoring
function solution(maps) {
    let answer = 2;
    let locaQueue = [[0, 0]];
    const rows = maps.length - 1;
    const cols = maps[0].length - 1;
    const mapsCount = maps.map((row) => row.map((_) => 0));
    mapsCount[0][0] = 1;

    while (locaQueue.length) {
        const next = [];

        for (let i = 0; i < locaQueue.length; i++) {
            const row = locaQueue[i][0];
            const col = locaQueue[i][1];
            const map = [
                [row + 1, col],
                [row, col + 1],
                [row - 1, col],
                [row, col - 1],
            ];

            for (let j = 0; j < 4; j++) {
                const row = map[j][0];
                const col = map[j][1];

                if (maps[row] && maps[row][col] && !mapsCount[row][col]) {
                    if (row === rows && col === cols) return answer;
                    mapsCount[row][col] = 1;
                    next.push([row, col]);
                }
            }
        }

        answer++;
        locaQueue = next;
    }

    return -1;
}

console.log(
    solution([
        [1, 0, 1, 1, 1],
        [1, 0, 1, 0, 1],
        [1, 0, 1, 1, 1],
        [1, 1, 1, 0, 1],
        [0, 0, 0, 0, 1],
    ])
);
console.log(
    solution([
        [1, 0, 1, 1, 1],
        [1, 0, 1, 0, 1],
        [1, 0, 1, 1, 1],
        [1, 1, 1, 0, 0],
        [0, 0, 0, 0, 1],
    ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)