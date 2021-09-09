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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)