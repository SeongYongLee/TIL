## 배달

[Summer/Winter Coding(~2018) > 배달](https://programmers.co.kr/learn/courses/30/lessons/12978)

``` js
// 1 - 플로이드 와샬 (Floyd Warshall)
// function solution(N, road, K) {
//     const table = new Array(N)
//         .fill()
//         .map((_, i) => new Array(N).fill(Infinity).fill(0, i, i + 1));

//     for (let i = 0; i < road.length; i++) {
//         if (table[road[i][0] - 1][road[i][1] - 1] > road[i][2]) {
//             table[road[i][0] - 1][road[i][1] - 1] = road[i][2];
//             table[road[i][1] - 1][road[i][0] - 1] = road[i][2];
//         }
//     }

//     for (let m = 0; m < N; m++) {
//         for (let i = 0; i < N; i++) {
//             for (let j = 0; j < N; j++) {
//                 const sum = table[i][m] + table[m][j];
//                 if (table[i][j] > sum) table[i][j] = sum;
//             }
//         }
//     }

//     return table[0].filter((t) => K >= t).length;
// }

// 2 - 다익스트라 (Dijkstra)
function solution(N, road, K) {
    const table = new Array(N)
        .fill()
        .map((_, i) => new Array(N).fill(Infinity).fill(0, i, i + 1));

    for (let i = 0; i < road.length; i++) {
        if (table[road[i][0] - 1][road[i][1] - 1] > road[i][2]) {
            table[road[i][0] - 1][road[i][1] - 1] = road[i][2];
            table[road[i][1] - 1][road[i][0] - 1] = road[i][2];
        }
    }

    const answer = [...table[0]];
    const visited = new Array(N).fill(false).fill(true, 0, 1);

    for (let i = 1; i < N; i++) {
        const tempArray = answer.map((a, i) => (visited[i] ? Infinity : a));
        const index = tempArray.indexOf(Math.min(...tempArray));
        visited[index] = true;
        for (let j = 0; j < N; j++) {
            if (answer[j] > answer[index] + table[index][j])
                answer[j] = answer[index] + table[index][j];
        }
    }

    return answer.filter((t) => K >= t).length;
}

console.log(
    solution(
        5,
        [
            [1, 2, 1],
            [2, 3, 3],
            [5, 2, 2],
            [1, 4, 2],
            [5, 3, 1],
            [5, 4, 2],
        ],
        3
    )
);
console.log(
    solution(
        6,
        [
            [1, 2, 1],
            [1, 3, 2],
            [2, 3, 2],
            [3, 4, 3],
            [3, 5, 2],
            [3, 5, 3],
            [5, 6, 1],
        ],
        4,
    ),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)