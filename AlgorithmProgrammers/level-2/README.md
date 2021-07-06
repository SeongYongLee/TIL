# AlgorithmProgrammers - Level 2

* [2019 카카오 개발자 겨울 인턴십 > 튜플](#튜플)

* [2020 KAKAO BLIND RECRUITMENT > 괄호 변환](#괄호-변환)

* [2021 KAKAO BLIND RECRUITMENT > 순위 검색](#순위-검색)

* [2021 KAKAO BLIND RECRUITMENT > 메뉴 리뉴얼](#메뉴-리뉴얼)

* [찾아라 프로그래밍 마에스터 > 게임 맵 최단거리](#게임-맵-최단거리)

* [Summer/Winter Coding(~2018) > 스킬트리](#스킬트리)

* [Summer/Winter Coding(~2018) > 방문 길이](#방문-길이)

* [Summer/Winter Coding(~2018) > 배달](#배달)

* [Summer/Winter Coding(2019) > 멀쩡한 사각형](#멀쩡한-사각형)

* [스택/큐 > 기능개발](#기능개발)

* [스택/큐 > 프린터](#프린터)

* [연습문제 > 다음 큰 숫자](#다음-큰-숫자)

* [연습문제 > 124 나라의 숫자](#124-나라의-숫자)

* [연습문제 > 올바른 괄호](#올바른-괄호)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)

## 튜플

[2019 카카오 개발자 겨울 인턴십 > 튜플](https://programmers.co.kr/learn/courses/30/lessons/64065)

``` js
// 1
// function solution(words) {
//     const answerObject = {};
//     const answer = [];
//     let num = '';

//     for (let i = 0; i < words.length; i++) {
//         if (['{', ',', '}'].includes(words[i])) {
//             if (num === '') continue;
//             if (!answerObject[num]) answerObject[num] = 0;
//             answerObject[num]++;
//             num = '';
//         } else {
//             num += words[i];
//         }
//     }

//     for (const p in answerObject) {
//         answer[answerObject[p] - 1] = +p;
//     }

//     return answer.reverse();
// }

// 2 - Refactoring
/* 
    프로그래머스 - 다른 사람의 풀이 참고
*/
function solution(words) {
    return JSON.parse(words.replace(/{/g, '[').replace(/}/g, ']'))
        .sort((a, b) => a.length - b.length)
        .reduce((r, c) => [...r, ...c.filter((f) => !r.includes(f))]);
}

console.log(solution('{{2},{2,1},{2,1,3},{2,1,3,4}}'));
console.log(solution('{{1,2,3},{2,1},{1,2,4,3},{2}}'));
console.log(solution('{{20,111},{111}}'));
console.log(solution('{{123}}'));
console.log(solution('{{4,2,3},{3},{2,3,4,1},{2,3}}'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 괄호 변환

[2020 KAKAO BLIND RECRUITMENT > 괄호 변환](https://programmers.co.kr/learn/courses/30/lessons/60058)

``` js
// 1
// function solution(words) {
//   const sol = (words) => {
//       if (!words.length) return '';

//       const u = [];
//       let wordCount = 0;
//       let isCorrect = true;

//       while (words.length) {
//           wordCount += words[0] === '(' ? 1 : -1;
//           u.push(words.shift());
//           if (wordCount < 0) isCorrect = false;
//           else if (wordCount === 0) {
//               if (!isCorrect) {
//                   let temp = '';
//                   for (let i = 1; i < u.length - 1; i++) {
//                       temp += u[i] === '(' ? ')' : '(';
//                   }
//                   return '(' + sol(words) + ')' + temp;
//               } else {
//                   return u.join('') + sol(words);
//               }
//           }
//       }
//   };

//   return sol(words.split(''));
// }

// 2 - Refactoring
function solution(words) {
    const sol = (words) => {
        if (!words.length) return '';

        const u = [];
        let wordCount = 0;

        do {
            wordCount += words[0] === '(' ? 1 : -1;
            u.push(words.shift());
        } while (wordCount !== 0);

        if (u[0] === ')') {
            let temp = '';
            for (let i = 1; i < u.length - 1; i++) {
                temp += u[i] === '(' ? ')' : '(';
            }
            return '(' + sol(words) + ')' + temp;
        } else {
            return u.join('') + sol(words);
        }
    };

    return sol(words.split(''));
}

console.log(solution('(()())()'));
console.log(solution(')('));
console.log(solution('()))((()'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 순위 검색

[2021 KAKAO BLIND RECRUITMENT > 순위 검색](https://programmers.co.kr/learn/courses/30/lessons/72412)

``` js
// 1 - 효율성 테스트 탈락
// function solution(info, query) {
//     const infoSplit = info.map((m) => m.split(' ')).sort((a, b) => b[4] - a[4]);
//     const infoLength = info.length;
//     const queryLength = query.length;
//     const answer = [];

//     for (let i = 0; i < queryLength; i++) {
//         const querySplit = query[i].split(' ');
//         let count = 0;

//         for (let j = 0; j < infoLength; j++) {
//             if (+infoSplit[j][4] < +querySplit[7]) break;
//             if (
//                 (infoSplit[j][0] === querySplit[0] || querySplit[0] === '-') &&
//                 (infoSplit[j][1] === querySplit[2] || querySplit[2] === '-') &&
//                 (infoSplit[j][2] === querySplit[4] || querySplit[4] === '-') &&
//                 (infoSplit[j][3] === querySplit[6] || querySplit[6] === '-')
//             )
//                 count++;
//         }
//         answer.push(count);
//     }
//     return answer;
// }

// 2 - 효율성 테스트 탈락
// function solution(info, query) {
//     const infoLength = info.length;
//     const infoObject = {};
//     const queryLength = query.length;
//     const answer = [];
//     const condition = 4;

//     const sets = 1 << condition;

//     for (let i = 0; i < sets; i++) {
//         for (let j = 0; j < infoLength; j++) {
//             const infoSplit = info[j].split(' ');
//             let string = '';
//             for (let col = 0; col < condition; col++) {
//                 if (i & (1 << col)) string += infoSplit[col];
//                 else string += '-';
//             }
//             infoObject[string] = infoObject[string]
//                 ? [...infoObject[string], +infoSplit[4]]
//                 : [+infoSplit[4]];
//         }
//     }

//     for (const key in infoObject) {
//         infoObject[key] = infoObject[key].sort((a, b) => b - a);
//     }

//     for (let i = 0; i < queryLength; i++) {
//         const querySplit = query[i].split(' ');
//         const queryString = `${querySplit[0]}${querySplit[2]}${querySplit[4]}${querySplit[6]}`;
//         const queryNum = +querySplit[7];
//         let count = 0;

//         if (infoObject[queryString]) {
//             count = infoObject[queryString].findIndex((j) => j < queryNum);
//             if (count === -1) count = infoObject[queryString].length;
//         }
//         answer.push(count);
//     }

//     return answer;
// }

// 3 - binary search
/* 
    카카오 문제해설 참고
    https://tech.kakao.com/2021/01/25/2021-kakao-recruitment-round-1
*/
function solution(info, query) {
    const infoLength = info.length;
    const queryLength = query.length;
    const infoObject = {};
    const answer = [];

    function getInfoObject(infoArray, infoNum, start) {
        const key = infoArray.join('');

        // 효율성 테스트 오답의 주요 원인 1
        // infoObject[key] = infoObject[key] ? [...infoObject[key], infoNum] : [infoNum];
        if (infoObject[key]) {
            infoObject[key].push(infoNum);
        } else {
            infoObject[key] = [infoNum];
        }

        for (let i = start; i < infoArray.length; i++) {
            const temp = [...infoArray];
            temp[i] = '-';
            getInfoObject(temp, infoNum, i + 1);
        }
    }

    for (let i = 0; i < infoLength; i++) {
        const infoSplit = info[i].split(' ');
        const infoNum = +infoSplit.pop();
        getInfoObject(infoSplit, infoNum, 0);
    }

    for (const key in infoObject) {
        infoObject[key].sort((a, b) => a - b);
    }

    for (let i = 0; i < queryLength; i++) {
        const querySplit = query[i].split(' ');
        const queryString = `${querySplit[0]}${querySplit[2]}${querySplit[4]}${querySplit[6]}`;
        const queryNum = +querySplit[7];
        const resultArray = infoObject[queryString];
        let count = 0;

        if (resultArray) {
            // 효율성 테스트 오답의 주요 원인 2
            // resultArray.sort((a, b) => a - b);
            let start = 0;
            let end = resultArray.length;
            while (start < end) {
                const mid = Math.floor((start + end) / 2);

                if (resultArray[mid] >= queryNum) {
                    end = mid;
                } else if (resultArray[mid] < queryNum) {
                    start = mid + 1;
                }
            }

            count = resultArray.length - start;
        }

        answer.push(count);
    }

    return answer;
}

console.log(
    solution(
        [
            'java backend junior pizza 150',
            'python frontend senior chicken 210',
            'python frontend senior chicken 150',
            'cpp backend senior pizza 260',
            'java backend junior chicken 80',
            'python backend senior chicken 50',
        ],
        [
            'java and backend and junior and pizza 100',
            'python and frontend and senior and chicken 200',
            'cpp and - and senior and pizza 250',
            '- and backend and senior and - 150',
            '- and - and - and chicken 100',
            '- and - and - and - 150',
        ]
    )
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 메뉴 리뉴얼

[2021 KAKAO BLIND RECRUITMENT > 메뉴 리뉴얼](https://programmers.co.kr/learn/courses/30/lessons/72411)

``` js
// 1
// function solution(orders, course) {
//     const answer = [];
//     const orderList = [];

//     function getOrderList(list, order, i) {
//         if (order.length > i) {
//             getOrderList(list, order, i + 1);
//             getOrderList([...list, order[i]], order, i + 1);
//         } else {
//             if (list.length > 1) orderList[orderList.length - 1].push(list.sort().join(''));
//         }
//     }

//     for (let i = 0; i < orders.length; i++) {
//         orderList.push([]);
//         getOrderList([], orders[i], 0);
//     }

//     for (let i = 0; i < course.length; i++) {
//         const tempObject = {};

//         for (let j = 0; j < orderList.length; j++) {
//             for (let k = 0; k < orderList[j].length; k++) {
//                 if (orderList[j][k].length !== course[i]) continue;

//                 if (tempObject[orderList[j][k]]) {
//                     tempObject[orderList[j][k]] += 1;
//                 } else {
//                     tempObject[orderList[j][k]] = 1;
//                 }
//             }
//         }

//         let tempArray = [];
//         let maxNum = 0;

//         for (const [key, value] of Object.entries(tempObject)) {
//             if (maxNum === value) {
//                 tempArray.push(key);
//             } else if (maxNum < value) {
//                 maxNum = value;
//                 tempArray = [key];
//             }
//         }

//         if (maxNum >= 2) answer.push(...tempArray);
//     }

//     return answer.sort();
// }

// 2 - Refactoring
// function solution(orders, course) {
//     const answer = [];
//     const orderList = [];
//     const answerObject = {};

//     function getOrderList(list, order, i) {
//         if (order.length > i) {
//             getOrderList(list, order, i + 1);
//             getOrderList([...list, order[i]], order, i + 1);
//         } else if (list.length > 1) orderList[orderList.length - 1].push(list.sort().join(''));
//     }

//     for (let i = 0; i < orders.length; i++) {
//         orderList.push([]);
//         getOrderList([], orders[i], 0);
//     }

//     for (let i = 0; i < course.length; i++) {
//         answerObject[course[i]] = {};
//     }

//     for (let j = 0; j < orderList.length; j++) {
//         for (let k = 0; k < orderList[j].length; k++) {
//             const index = orderList[j][k].length;
//             if (!answerObject[index]) continue;

//             if (answerObject[index][orderList[j][k]]) {
//                 answerObject[index][orderList[j][k]] += 1;
//             } else {
//                 answerObject[index][orderList[j][k]] = 1;
//             }
//         }
//     }

//     for (const index in answerObject) {
//         let maxNum = 0;

//         for (const [key, value] of Object.entries(answerObject[index])) {
//             if (maxNum === value) {
//                 tempArray.push(key);
//             } else if (maxNum < value) {
//                 maxNum = value;
//                 tempArray = [key];
//             }
//         }

//         if (maxNum >= 2) answer.push(...tempArray);
//     }

//     return answer.sort();
// }

// 3 - Refactoring
function solution(orders, course) {
    const answer = [];
    const orderList = [];
    const answerObject = {};
    const answerMax = {};

    function getOrderList(list, order, i) {
        if (order.length > i) {
            getOrderList(list, order, i + 1);
            getOrderList([...list, order[i]], order, i + 1);
        } else if (list.length > 1) orderList[orderList.length - 1].push(list.sort().join(''));
    }

    for (let i = 0; i < orders.length; i++) {
        orderList.push([]);
        getOrderList([], orders[i], 0);
    }

    for (let i = 0; i < course.length; i++) {
        answerObject[course[i]] = {};
        answerMax[course[i]] = { max: 1 };
    }

    for (let j = 0; j < orderList.length; j++) {
        for (let k = 0; k < orderList[j].length; k++) {
            const index = orderList[j][k].length;
            if (!answerObject[index]) continue;

            if (answerObject[index][orderList[j][k]]) {
                answerObject[index][orderList[j][k]] += 1;
                if (answerObject[index][orderList[j][k]] > answerMax[index].max) {
                    answerMax[index].max = answerObject[index][orderList[j][k]];
                    answerMax[index].list = [orderList[j][k]];
                } else if (answerObject[index][orderList[j][k]] === answerMax[index].max) {
                    answerMax[index].list.push(orderList[j][k]);
                }
            } else {
                answerObject[index][orderList[j][k]] = 1;
            }
        }
    }

    for (const index in answerMax) {
        if (answerMax[index].list) answer.push(...answerMax[index].list);
    }

    return answer.sort();
}

console.log(solution(['ABCFG', 'AC', 'CDE', 'ACDE', 'BCFG', 'ACDEH'], [2, 3, 4]));
console.log(solution(['ABCDE', 'AB', 'CD', 'ADE', 'XYZ', 'XYZ', 'ACD'], [2, 3, 5]));
console.log(solution(['XYZ', 'XWY', 'WXA'], [2, 3, 4]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 스킬트리

[Summer/Winter Coding(~2018) > 스킬트리](https://programmers.co.kr/learn/courses/30/lessons/49993)

``` js
function solution(skill, skill_trees) {
    const calc = (s) =>
        skill.indexOf(
            s
                .split('')
                .filter((x) => skill.indexOf(x) !== -1)
                .join(''),
        ) === 0;

    return skill_trees.filter((s) => calc(s)).length;
}

console.log(solution('CBD', ['BACDE', 'CBADF', 'AECB', 'BDA']));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 방문 길이

[Summer/Winter Coding(~2018) > 방문 길이](https://programmers.co.kr/learn/courses/30/lessons/49994)

``` js
function solution(dirs) {
    const answer = new Set();
    let x = 0;
    let y = 0;

    for (let i = 0; i < dirs.length; i++) {
        const first = '' + x + y;

        switch (dirs[i]) {
            case 'U':
                if (y === 5) continue;
                y++;
                break;
            case 'D':
                if (y === -5) continue;
                y--;
                break;
            case 'R':
                if (x === 5) continue;
                x++;
                break;
            case 'L':
                if (x === -5) continue;
                x--;
                break;
        }

        const second = '' + x + y;

        answer.add(first + second);
        answer.add(second + first);
    }

    return answer.size / 2;
}

console.log(solution('ULURRDLLU'));
console.log(solution('LULLLLLLU'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 방문 길이

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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 멀쩡한 사각형

[Summer/Winter Coding(2019) > 멀쩡한 사각형](https://programmers.co.kr/learn/courses/30/lessons/62048)

``` js
// 1
// const gcd = (a, b) => {
//     return b ? gcd(b, a % b) : Math.abs(a);
// };

// function solution(w, h) {
//     const temp = gcd(w, h);

//     return w * h - (w / temp + h / temp - 1) * temp;
// }

// 2 - Refactoring
const gcd = (a, b) => {
    return b ? gcd(b, a % b) : Math.abs(a);
};

function solution(w, h) {
    return w * h - (w + h - gcd(w, h));
}

console.log(solution(8, 12));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 기능개발

[스택/큐 > 기능개발](https://programmers.co.kr/learn/courses/30/lessons/42586)

``` js
// 1
// function solution(progresses, speeds) {
//     const answer = [];
    
//     while (speeds.length) {
//         let count = 0;
//         progresses = progresses.map((x, i) => x + speeds[i]);
//         while (speeds.length) {
//             if (progresses[0] >= 100) {
//                 progresses.shift();
//                 speeds.shift();
//                 count++;
//             } else break;
//         }
//         if (count) answer.push(count);
//     }
    
//     return answer;
// }

// 2 - Refactoring
// function solution(board, moves) {
//     let answer = 0;
//     const result = [];

//     let fitstFilter = board.reduce((result, x, i) => x.map((i, y) => [...(result[y] || []), i]), []);
//     let secondFilter = fitstFilter.map((x, i) => x.filter((x) => x !== 0).reverse());

//     for (let x = 0; x < moves.length; x++) {
//         const temp = secondFilter[moves[x] - 1].pop();
//         if (!temp) continue;
//         if (temp === result[result.length - 1]) {
//             result.pop();
//             answer += 2;
//             continue;
//         }
//         result.push(temp);
//     }
//     return answer;
// }

// 3 - Change Approach
/* 
    프로그래머스 - 다른 사람의 풀이 참고
*/
function solution(progresses, speeds) {
    const answer = [0];
    const days = progresses.map((p, i) => Math.ceil((100 - p) / speeds[i]));
    const dlength = days.length;
    let maxDay = days[0];

    for (let i = 0, j = 0; i < dlength; i++) {
        if (days[i] <= maxDay) {
            answer[j] += 1;
        } else {
            maxDay = days[i];
            answer[++j] = 1;
        }
    }

    return answer;
}

console.log(solution([93, 30, 55], [1, 30, 5]));
console.log(solution([95, 90, 99, 99, 80, 99], [1, 1, 1, 1, 1, 1]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 프린터

[스택/큐 > 프린터](https://programmers.co.kr/learn/courses/30/lessons/42587)

``` js
function solution(priorities, location) {
    let p = priorities.map((a, b) => [a, b]);
    let answer = 1;

    do {
        const temp = [p.shift()];

        while (p.length) {
            if (p[0][0] > temp[0][0]) p.push(...temp.splice(0, temp.length));
            temp.push(p.shift());
        }

        if (location === temp.shift()[1]) return answer;
        else p = temp.slice();
    } while (answer++);
}

console.log(solution([2, 1, 3, 2], 2));
console.log(solution([1, 1, 9, 1, 1, 1], 0));
console.log(solution([1], 0));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 다음 큰 숫자

[연습문제 > 다음 큰 숫자](https://programmers.co.kr/learn/courses/30/lessons/12911)

``` js
function solution(n) {
  const count = (n) =>
    n
      .toString(2)
      .split('')
      .filter((x) => x === '1').length;

  const nLength = count(n);

  while (n++) if (nLength === count(n)) return n;
}

console.log(solution(78));
console.log(solution(15));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 123 나라의 숫자

[연습문제 > 124 나라의 숫자](https://programmers.co.kr/learn/courses/30/lessons/12899)

``` js
// 1
// function solution(n) {
//     const temp = n.toString(3).split('');

//     for (let x = temp.length - 1; x >= 0; x--) {
//         switch (+temp[x]) {
//             case 0:
//                 if (x !== 0) {
//                     temp[x - 1] = +temp[x - 1] - 1;
//                     temp[x] = 4;
//                 } else temp.shift();
//                 break;
//             case -1:
//                 temp[x - 1] = +temp[x - 1] - 1;
//                 temp[x] = 2;
//                 break;
//         }
//     }

//     return temp.join('');
// }
// /*
// 1   1   1
// 2   2   2
// 3   10  4   !
// 4   11  11
// 5   12  12
// 6   20  14  !
// 7   21  21
// 8   22  22
// 9   100 24  !
// 10  101 41  !
// 11  102 42  !
// 12  110 44  !
// 13  111 111
// 14  112 112
// 15  120 114 !
// 16  121 121
// */

// 2 - Refactoring
/* 
    프로그래머스 - 다른 사람의 풀이 참고
*/
function solution(n) {
    return n ? solution(parseInt((n - 1) / 3)) + [1, 2, 4][(n - 1) % 3] : '';
}
// /*
// 1   1           1
// 2   1*2         2
// 3   1*3         4
// 4   3*1+1*1     11
// 5   3*1+1*2     12
// 6   3*1+1*3     14
// 7   3*2+1*1     21
// */

console.log(solution(1));
console.log(solution(2));
console.log(solution(3));
console.log(solution(4));
console.log(solution(13));
console.log(solution(10));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 올바른 괄호

[연습문제 > 올바른 괄호](https://programmers.co.kr/learn/courses/30/lessons/12909)

``` js
// 1
function solution(s) {
    let answer = 0;
    const sLength = s.length;

    for (let i = 0; i < sLength; i++) {
        answer += s[i] === '(' ? 1 : -1;
        if (answer < 0) return false;
    }

    return answer === 0 ? true : false;
}

// 2 - Refactoring (1이 더 빠름)
// function solution(s) {
//     let answer = 0;
//     const sLength = s.length;

//     for (let i = 0; i < sLength; i++) {
//         answer += s[i] === '(' ? 1 : -1;
//         if (answer < 0 || answer > sLength - i - 1) return false;
//     }

//     return answer === 0 ? true : false;
// }

// console.log(solution('()()'));
// console.log(solution('(())()'));
// console.log(solution(')()('));
// console.log(solution('(()('));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>