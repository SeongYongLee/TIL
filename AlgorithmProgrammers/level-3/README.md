# AlgorithmProgrammers - Level 3

* [2020 KAKAO BLIND RECRUITMENT > 자물쇠와 열쇠](#자물쇠와-열쇠)

* [2021 KAKAO BLIND RECRUITMENT > 합승 택시 요금](#합승-택시-요금)

* [이분탐색 > 입국심사](#입국심사)

* [탐욕법 > 섬 연결하기](#섬-연결하기)

* [탐욕법 > 단속카메라](#단속카메라)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)

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