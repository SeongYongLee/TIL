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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)