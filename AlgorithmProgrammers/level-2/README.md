# AlgorithmProgrammers - Level 2

* [스택/큐 > 기능개발](#기능개발)

* [2021 KAKAO BLIND RECRUITMENT > 순위 검색](#순위-검색)

* [2021 KAKAO BLIND RECRUITMENT > 메뉴 리뉴얼](#메뉴-리뉴얼)

* [연습문제 > 다음 큰 숫자](#다음-큰-숫자)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)

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

## 메뉴 리뉴얼

[2021 KAKAO BLIND RECRUITMENT > 메뉴 리뉴얼](https://programmers.co.kr/learn/courses/30/lessons/72411)

``` js
function solution(orders, course) {
    const answer = [];
    const orderList = [];

    function getOrderList(list, order, i) {
        if (order.length > i) {
            getOrderList(list, order, i + 1);
            getOrderList([...list, order[i]], order, i + 1);
        } else {
            if (list.length > 1) orderList[orderList.length - 1].push(list.sort().join(''));
        }
    }

    for (let i = 0; i < orders.length; i++) {
        orderList.push([]);
        getOrderList([], orders[i], 0);
    }

    for (let i = 0; i < course.length; i++) {
        const tempObject = {};

        for (let j = 0; j < orderList.length; j++) {
            for (let k = 0; k < orderList[j].length; k++) {
                if (orderList[j][k].length !== course[i]) continue;

                if (tempObject[orderList[j][k]]) {
                    tempObject[orderList[j][k]] += 1;
                } else {
                    tempObject[orderList[j][k]] = 1;
                }
            }
        }

        let tempArray = [];
        let maxNum = 0;

        for (const [key, value] of Object.entries(tempObject)) {
            if (maxNum === value) {
                tempArray.push(key);
            } else if (maxNum < value) {
                maxNum = value;
                tempArray = [key];
            }
        }

        if (maxNum >= 2) answer.push(...tempArray);
    }

    return answer.sort();
}

console.log(solution(['ABCFG', 'AC', 'CDE', 'ACDE', 'BCFG', 'ACDEH'], [2, 3, 4]));
console.log(solution(['ABCDE', 'AB', 'CD', 'ADE', 'XYZ', 'XYZ', 'ACD'], [2, 3, 5]));
console.log(solution(['XYZ', 'XWY', 'WXA'], [2, 3, 4]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>