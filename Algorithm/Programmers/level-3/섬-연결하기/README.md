## 섬 연결하기

[탐욕법 > 섬 연결하기](https://programmers.co.kr/learn/courses/30/lessons/42861)

```js
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
        (connected.has(to) && !connected.has(from)),
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
  ]),
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
  ]),
);

console.log(
  solution(5, [
    [0, 1, 1],
    [3, 4, 1],
    [1, 2, 2],
    [2, 3, 4],
  ]),
);

console.log(
  solution(4, [
    [0, 1, 5],
    [1, 2, 3],
    [2, 3, 3],
    [1, 3, 2],
    [0, 3, 4],
  ]),
);

console.log(
  solution(5, [
    [0, 1, 1],
    [3, 1, 1],
    [0, 2, 2],
    [0, 3, 2],
    [0, 4, 100],
  ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
