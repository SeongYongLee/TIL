# AlgorithmProgrammers - Level 2

* [2017 팁스타운 > 예상 대진표](#예상-대진표)

* [2017 팁스타운 > 짝지어 제거하기](#짝지어-제거하기)

* [2019 카카오 개발자 겨울 인턴십 > 튜플](#튜플)

* [2020 카카오 인턴십 > 수식 최대화](#수식-최대화)

* [2021 카카오 채용연계형 인턴십 > 거리두기 확인하기](#거리두기-확인하기)

* [2020 KAKAO BLIND RECRUITMENT > 괄호 변환](#괄호-변환)

* [2021 KAKAO BLIND RECRUITMENT > 순위 검색](#순위-검색)

* [2021 KAKAO BLIND RECRUITMENT > 메뉴 리뉴얼](#메뉴-리뉴얼)

* [2021 Dev-Matching: 웹 백엔드 개발자(상반기) > 행렬 테두리 회전하기](#행렬-테두리-회전하기)

* [월간 코드 챌린지 시즌1 > 쿼드 압축 후 개수 세기](#쿼드-압축-후-개수-세기)

* [월간 코드 챌린지 시즌1 > 삼각 달팽이](#삼각-달팽이)

* [월간 코드 챌린지 시즌2 > 괄호 회전하기](#괄호-회전하기)

* [월간 코드 챌린지 시즌2 > 2개 이하로 다른 비트](#2개-이하로-다른-비트)

* [찾아라 프로그래밍 마에스터 > 게임 맵 최단거리](#게임-맵-최단거리)

* [Summer/Winter Coding(~2018) > 스킬트리](#스킬트리)

* [Summer/Winter Coding(~2018) > 방문 길이](#방문-길이)

* [Summer/Winter Coding(~2018) > 배달](#배달)

* [Summer/Winter Coding(~2018) > 영어 끝말잇기](#영어-끝말잇기)

* [Summer/Winter Coding(~2018) > 점프와 순간 이동](#점프와-순간-이동)

* [Summer/Winter Coding(2019) > 멀쩡한 사각형](#멀쩡한-사각형)

* [스택/큐 > 기능개발](#기능개발)

* [스택/큐 > 프린터](#프린터)

* [연습문제 > 다음 큰 숫자](#다음-큰-숫자)

* [연습문제 > 124 나라의 숫자](#124-나라의-숫자)

* [연습문제 > 올바른 괄호](#올바른-괄호)

* [연습문제 > 가장 큰 정사각형 찾기](#가장-큰-정사각형-찾기)

* [연습문제 > N개의 최소공배수](#N개의-최소공배수)

* [연습문제 > JadenCase 문자열 만들기](#JadenCase-문자열-만들기)

* [연습문제 > 행렬의 곱셈](#행렬의-곱셈)

* [연습문제 > 피보나치 수](#피보나치-수)

* [연습문제 > 최솟값 만들기](#최솟값-만들기)

* [연습문제 > 숫자의 표현](#숫자의-표현)

* [연습문제 > 땅따먹기](#땅따먹기)

* [사라진문제 > 스택/큐 > 탑](#탑)

* [사라진문제 > 스택/큐 > 쇠막대기](#쇠막대기)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)

## 예상 대진표

[2017 팁스타운 > 예상 대진표](https://programmers.co.kr/learn/courses/30/lessons/12985)

``` js
function solution(n, a, b) {
    let answer = 0;

    while (a !== b) {
        a = Math.ceil(a / 2);
        b = Math.ceil(b / 2);
        answer++;
    }

    return answer;
}

console.log(solution(8, 4, 7));
console.log(solution(8, 1, 2));
console.log(solution(8, 4, 8));
console.log(solution(16, 4, 9));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 짝지어 제거하기

[2017 팁스타운 > 짝지어 제거하기](https://programmers.co.kr/learn/courses/30/lessons/12973)

``` js
function solution(s) {
    const temp = [];

    for (let i = 0; i < s.length; i++) {
        if (temp[temp.length - 1] === s[i]) temp.pop();
        else temp.push(s[i]);
    }

    return temp.length ? 0 : 1;
}

console.log(solution('baabaa'));
console.log(solution('baabaa'));
console.log(solution('cdcd'));

```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

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

## 튜플

[2020 카카오 인턴십 > 수식 최대화](https://programmers.co.kr/learn/courses/30/lessons/67257)

``` js
function solution(expression) {
    let answer = 0;
    let numTemp = '';
    const numArr = [];
    const expArr = [];
    const expList = ['+', '-', '*'];

    const sol = (expList, expArr, numArr) => {
        for (let i = 0; i < expList.length; i++) {
            const sliceExpList = expList.slice();
            const sliceExpArr = expArr.slice();
            const sliceNumArr = numArr.slice();
            const nextExp = sliceExpList.splice(i, 1)[0];

            for (let j = 0; j < sliceExpArr.length; j++) {
                if (sliceExpArr[j] === nextExp) {
                    let resultNum = 0;
                    switch (nextExp) {
                        case '+':
                            resultNum = +sliceNumArr[j] + +sliceNumArr[j + 1];
                            break;
                        case '-':
                            resultNum = +sliceNumArr[j] - +sliceNumArr[j + 1];
                            break;
                        case '*':
                            resultNum = +sliceNumArr[j] * +sliceNumArr[j + 1];
                            break;
                    }
                    sliceNumArr.splice(j, 2, resultNum);
                    sliceExpArr.splice(j, 1);
                    j--;
                }
            }
            
            if (sliceExpList.length) {
                sol(sliceExpList, sliceExpArr, sliceNumArr);
            } else {
                const result = Math.abs(...sliceNumArr);
                if (result > answer) answer = result;
            }
        }
    };

    for (let i = 0; i < expression.length; i++) {
        if (expList.includes(expression[i])) {
            numArr.push(numTemp);
            expArr.push(expression[i]);
            numTemp = '';
        } else numTemp += expression[i];
    }
    numArr.push(numTemp);

    sol(expList, expArr, numArr);

    return answer;
}

console.log(solution('100-200*300-500+20'));
console.log(solution('50*6-3*2'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 거리두기 확인하기

[2021 카카오 채용연계형 인턴십 > 거리두기 확인하기](https://programmers.co.kr/learn/courses/30/lessons/81302)

``` js
function solution(places) {
    const pLength = places[0].length;
    const nearP = (place, x, y) => {
        for (let i = x - 2 > 0 ? x - 2 : 0; i < (x + 3 < pLength ? x + 3 : pLength); i++) {
            const xAbs = Math.abs(x - i);
            for (
                let j = y - 2 + xAbs > 0 ? y - 2 + xAbs : 0;
                j < (y + 3 - xAbs < pLength ? y + 3 - xAbs : pLength);
                j++
            ) {
                if (place[i][j] === 'P' && !(x === i && y === j)) {
                    switch (xAbs) {
                        case 0:
                            if (Math.abs(y - j) === 1 || place[i][(y + j) / 2] !== 'X') return 1;
                            break;
                        case 2:
                            if (place[(x + i) / 2][j] !== 'X') return 1;
                            break;
                        case 1:
                            if (place[x][j] !== 'X' || place[i][y] !== 'X') return 1;
                            break;
                    }
                }
            }
        }
        return 0;
    };

    return places.map((place) => {
        for (let x = 0; x < pLength; x++) {
            const placeSplit = place[x].split('');
            for (let y = 0; y < pLength; y++) {
                if (placeSplit[y] === 'P') {
                    if (nearP(place, x, y)) return 0;
                    placeSplit[y] = 'O';
                    place[x] = placeSplit.join('');
                }
            }
        }
        return 1;
    });
}

console.log(
    solution([
        ['POOOP', 'OXXOX', 'OPXPX', 'OOXOX', 'POXXP'],
        ['POOPX', 'OXPXP', 'PXXXO', 'OXXXO', 'OOOPP'],
        ['PXOPX', 'OXOXP', 'OXPOX', 'OXXOP', 'PXPOX'],
        ['OOOXX', 'XOOOX', 'OOOXX', 'OXOOX', 'OOOOO'],
        ['PXPXP', 'XPXPX', 'PXPXP', 'XPXPX', 'PXPXP'],
    ])
);
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

## 행렬 테두리 회전하기

[2021 Dev-Matching: 웹 백엔드 개발자(상반기) > 행렬 테두리 회전하기](https://programmers.co.kr/learn/courses/30/lessons/77485)

``` js
// 1
function solution(rows, columns, queries) {
    const answer = [];
    const matrix = new Array(rows)
        .fill()
        .map((r, i) => new Array(columns).fill().map((c, j) => i * columns + j + 1));

    for (let i = 0; i < queries.length; i++) {
        const setNum = (tempNum) => {
            matrix[row][column] = lastNum;
            lastNum = tempNum;
            if (minNum > lastNum) minNum = lastNum;
        };

        const rowDiff = queries[i][2] - queries[i][0];
        const columnDiff = queries[i][3] - queries[i][1];
        let row = queries[i][0] - 1;
        let column = queries[i][1] - 1;
        let lastNum = matrix[row][column];
        let minNum = lastNum;

        // right
        for (let i = 0; i < columnDiff; i++) {
            setNum(matrix[row][++column]);
        }
        // down
        for (let i = 0; i < rowDiff; i++) {
            setNum(matrix[++row][column]);
        }
        // left
        for (let i = 0; i < columnDiff; i++) {
            setNum(matrix[row][--column]);
        }
        // up
        for (let i = 0; i < rowDiff; i++) {
            setNum(matrix[--row][column]);
        }

        answer.push(minNum);
    }

    return answer;
}

// 2 - Refactoring (더 느려짐)
// function solution(rows, columns, queries) {
//     const matrix = new Array(rows)
//         .fill()
//         .map((r, i) => new Array(columns).fill().map((c, j) => i * columns + j + 1));

//     return queries.map((query) => {
//         const [sr, sc, er, ec] = query.map((q) => q - 1);
//         const tempNum = matrix[sr][sc];
//         let minNum = matrix[sr][sc];

//         // down
//         for (let i = sr; i < er; i++) {
//             matrix[i][sc] = matrix[i + 1][sc];
//             if (minNum > matrix[i][sc]) minNum = matrix[i][sc];
//         }
//         // right
//         for (let i = sc; i < ec; i++) {
//             matrix[er][i] = matrix[er][i + 1];
//             if (minNum > matrix[er][i]) minNum = matrix[er][i];
//         }
//         // up
//         for (let i = er; i > sr; i--) {
//             matrix[i][ec] = matrix[i - 1][ec];
//             if (minNum > matrix[i][ec]) minNum = matrix[i][ec];
//         }
//         // left
//         for (let i = ec; i > sc; i--) {
//             matrix[sr][i] = matrix[sr][i - 1];
//             if (minNum > matrix[sr][i]) minNum = matrix[sr][i];
//         }
//         matrix[sr][sc + 1] = tempNum;

//         return minNum;
//     });
// }

console.log(
    solution(6, 6, [
        [2, 2, 5, 4],
        [3, 3, 6, 6],
        [5, 1, 6, 3],
    ]),
);
console.log(
    solution(3, 3, [
        [1, 1, 2, 2],
        [1, 2, 2, 3],
        [2, 1, 3, 2],
        [2, 2, 3, 3],
    ]),
);
console.log(solution(100, 97, [[1, 1, 100, 97]]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 쿼드 압축 후 개수 세기

[월간 코드 챌린지 시즌1 > 쿼드 압축 후 개수 세기](https://programmers.co.kr/learn/courses/30/lessons/68936)

``` js
function solution(arr) {
    const answer = arr.reduce(
        (r, a) => {
            a.map((b) => r[b]++);
            return r;
        },
        [0, 0],
    );
    const isCompress = (num, i, j, k) => {
        for (let a = j; a < j + i; a++) {
            for (let b = k; b < k + i; b++) {
                if (num !== arr[a][b]) return false;
            }
        }
        return true;
    };
    const compress = (i, j, k) => {
        for (let a = j; a < j + i; a++) {
            for (let b = k; b < k + i; b++) {
                arr[a][b] = -1;
            }
        }
    };

    const aLength = arr.length;

    for (let i = aLength; i > 1; i /= 2) {
        for (let j = 0; j < aLength; j += i) {
            for (let k = 0; k < aLength; k += i) {
                const num = arr[j][k];
                if (num === -1) continue;
                if (isCompress(num, i, j, k)) {
                    compress(i, j, k);
                    answer[num] -= i * i - 1;
                }
            }
        }
    }

    return answer;
}

console.log(
    solution([
        [1, 1, 0, 0],
        [1, 0, 0, 0],
        [1, 0, 0, 1],
        [1, 1, 1, 1],
    ]),
);
console.log(
    solution([
        [1, 1, 1, 1, 1, 1, 1, 1],
        [0, 1, 1, 1, 1, 1, 1, 1],
        [0, 0, 0, 0, 1, 1, 1, 1],
        [0, 1, 0, 0, 1, 1, 1, 1],
        [0, 0, 0, 0, 0, 0, 1, 1],
        [0, 0, 0, 0, 0, 0, 0, 1],
        [0, 0, 0, 0, 1, 0, 0, 1],
        [0, 0, 0, 0, 1, 1, 1, 1],
    ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 삼각 달팽이

[월간 코드 챌린지 시즌1 > 삼각 달팽이](https://programmers.co.kr/learn/courses/30/lessons/68645)

``` js
// 1
// function solution(n) {
//     let step = 0; // 0: down, 1: right, 2: up
//     let num = 1;
//     let location = 0;
//     const answerLeft = Array(n)
//         .fill()
//         .map((_) => Array());
//     const answerRight = Array(n)
//         .fill()
//         .map((_) => Array());

//     for (let i = n; i > 0; i--) {
//         switch (step) {
//             case 0:
//                 for (let j = 0; j < i; j++) {
//                     answerLeft[location].push(num);
//                     location++;
//                     num++;
//                 }
//                 location--;
//                 break;
//             case 1:
//                 for (let j = 0; j < i; j++) {
//                     answerLeft[location].push(num);
//                     num++;
//                 }
//                 break;
//             case 2:
//                 for (let j = 0; j < i; j++) {
//                     location--;
//                     answerRight[location].unshift(num);
//                     num++;
//                 }
//                 location++;
//                 break;
//         }
//         step = (step + 1) % 3;
//     }

//     return answerLeft.reduce((r, c, i) => [...r, ...answerLeft[i], ...answerRight[i]], []);
// }

// 2 - Refactoring
// function solution(n) {
//     let num = 1;
//     let location = 0;
//     const answerLeft = Array(n)
//         .fill()
//         .map((_) => Array());
//     const answerRight = Array(n)
//         .fill()
//         .map((_) => Array());

//     for (let i = n; i > 0; i -= 3) {
//         for (let j = 0; j < i; j++) answerLeft[location++].push(num++);
//         location--;
//         for (let j = 0; j < i - 1; j++) answerLeft[location].push(num++);
//         for (let j = 0; j < i - 2; j++) answerRight[location--].unshift(num++);
//         location++;
//     }

//     return answerLeft.reduce((r, c, i) => [...r, ...c, ...answerRight[i]], []);
// }

// 3 - Refactoring
/* 
    프로그래머스 - 다른 사람의 풀이 참고
*/
function solution(n) {
    let num = 0;
    let y = -1;
    let x = 0;
    const answer = Array(n)
        .fill()
        .map((_, i) => Array(i + 1).fill());

    for (let i = n; i > 0; i -= 3) {
        for (let j = 0; j < i; j++) answer[++y][x] = ++num;
        for (let j = 0; j < i - 1; j++) answer[y][++x] = ++num;
        for (let j = 0; j < i - 2; j++) answer[--y][--x] = ++num;
    }

    return answer.flat();
}

console.log(solution(4));
console.log(solution(5));
console.log(solution(6));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 괄호 회전하기

[월간 코드 챌린지 시즌2 > 괄호 회전하기](https://programmers.co.kr/learn/courses/30/lessons/76502)

``` js
// 1
// function solution(words) {
//     const isCorrect = (i) => {
//         const stack = [];

//         for (let a = i; a < wLength; a++) {
//             if (!sol(stack, words[a])) return false;
//         }

//         for (let b = 0; b < i; b++) {
//             if (!sol(stack, words[b])) return false;
//         }

//         return !stack.length;
//     };

//     const sol = (stack, word) => {
//         switch (word) {
//             case ']':
//                 if (stack[stack.length - 1] === '[') stack.pop();
//                 else return false;
//                 break;
//             case '}':
//                 if (stack[stack.length - 1] === '{') stack.pop();
//                 else return false;
//                 break;
//             case ')':
//                 if (stack[stack.length - 1] === '(') stack.pop();
//                 else return false;
//                 break;
//             default:
//                 stack.push(word);
//                 break;
//         }

//         return true;
//     };

//     const wLength = words.length;
//     let answer = 0;

//     for (let i = 0; i < wLength; i++) {
//         if (isCorrect(i)) answer++;
//     }

//     return answer;
// }

// 2 - Refactoring
function solution(words) {
    const pair = { ']': '[', '}': '{', ')': '(' };

    const isCorrect = (i) => {
        const stack = [];

        for (let a = i; a < wLength; a++) {
            if (!sol(stack, words[a])) return false;
        }

        for (let b = 0; b < i; b++) {
            if (!sol(stack, words[b])) return false;
        }

        return !stack.length;
    };

    const sol = (stack, word) => {
        if ([']', ')', '}'].includes(word)) {
            if (stack[stack.length - 1] === pair[word]) stack.pop();
            else return false;
        } else {
            stack.push(word);
        }

        return true;
    };

    let answer = 0;
    const wLength = words.length;

    for (let i = 0; i < wLength; i++) {
        if (isCorrect(i)) answer++;
    }

    return answer;
}

console.log(solution('[](){}'));
console.log(solution('}]()[{'));
console.log(solution('[)(]'));
console.log(solution('}}}'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 괄호 회전하기

[월간 코드 챌린지 시즌2 > 2개 이하로 다른 비트](https://programmers.co.kr/learn/courses/30/lessons/77885)

``` js
// 1 - 효율성 탈락
// function solution(words) {
//     const isAnswer = (x, word) => {
//         const wLength = word.length;
//         const nextNum = x.toString(2);
//         const nextNumLength = nextNum.length;
//         let diff = 0;

//         for (let i = 1; i <= nextNumLength; i++) {
//             const currentNum = word[wLength - i];

//             if ((currentNum ? currentNum : '0') !== nextNum[nextNumLength - i] && diff++ === 2)
//                 return false;
//         }

//         return diff ? true : false;
//     };

//     return words.map((x) => {
//         const word = x.toString(2);

//         while (x++) {
//             if (isAnswer(x, word)) return x;
//         }
//     });
// }

// 2 - 효율성 탈락
// function solution(words) {
//     return words.map((x) => {
//         const word = x;

//         while (1) {
//             if (
//                 [1, 2].includes(
//                     (word ^ ++x)
//                         .toString(2)
//                         .split('')
//                         .filter((x) => +x).length,
//                 )
//             )
//                 return x;
//         }
//     });
// }

// 3
function solution(words) {
    return words.map((x) => {
        const word = x.toString(2);
        let numCount = 0;

        for (let i = word.length - 1; i >= 0; i--) {
            if (+word[i]) numCount++;
            else break;
        }

        numCount = Math.pow(2, numCount - 1);

        return x + (numCount > 1 ? numCount : 1);
    });
}

console.log(solution([2, 7]));
console.log(
    solution([
        1001, 337, 0, 1, 333, 673, 343, 221, 898, 997, 121, 1015, 665, 779, 891, 421, 222, 256, 512,
        128, 100,
    ]),
);
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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 영어 끝말잇기

[Summer/Winter Coding(2019) > 영어 끝말잇기](https://programmers.co.kr/learn/courses/30/lessons/12981)

``` js
function solution(n, words) {
    const wordsLength = words.length;
    const history = [words[0]];

    for (let i = 1; i < wordsLength; i++) {
        if (words[i - 1].slice(-1) === words[i].slice(0, 1) && history.indexOf(words[i]) === -1) {
            history.push(words[i]);
        } else {
            return [(i % n) + 1, Math.floor(i / n) + 1];
        }
    }

    return [0, 0];
}

console.log(
    solution(3, ['tank', 'kick', 'know', 'wheel', 'land', 'dream', 'mother', 'robot', 'tank']),
);
console.log(
    solution(5, [
        'hello',
        'observe',
        'effect',
        'take',
        'either',
        'recognize',
        'encourage',
        'ensure',
        'establish',
        'hang',
        'gather',
        'refer',
        'reference',
        'estimate',
        'executive',
    ]),
);
console.log(solution(2, ['hello', 'one', 'even', 'never', 'now', 'world', 'draw']));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 점프와 순간 이동

[Summer/Winter Coding(~2018) > 점프와 순간 이동](https://programmers.co.kr/learn/courses/30/lessons/12980)

``` js
// 1
// function solution(n) {
//     let ans = 0;

//     while (n) {
//         if (n % 2 === 0) {
//             n /= 2;
//         } else {
//             n--;
//             ans++;
//         }
//     }

//     return ans;
// }

// 2 - Refactoring
function solution(n) {
    return n
        .toString(2)
        .split('')
        .filter((n) => +n).length;
}

console.log(solution(5));
console.log(solution(6));
console.log(solution(5000));
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

## 가장 큰 정사각형 찾기

[연습문제 > 가장 큰 정사각형 찾기](https://programmers.co.kr/learn/courses/30/lessons/12905)

``` js
// 1 - 효율성 탈락
// function solution(board) {
//     let answer = 0;

//     for (let i = 0; i < board.length - answer; i++) {
//         for (let j = 0; j < board[i].length - answer; j++) {
//             if (board[i][j]) {
//                 let temp = isSquare(i, j, 1);
//                 answer = answer > temp ? answer : temp;
//             }
//         }
//     }

//     function isSquare(x, y, n) {
//         if (board[x + n] && board[x + n][y] && board[x][y + n]) {
//             for (let i = x; i < x + n; i++) {
//                 if (!board[i][y + n]) return n;
//             }
//             for (let i = y; i < y + n; i++) {
//                 if (!board[x + n][i]) return n;
//             }
//             if (!board[x + n][y + n]) return n;
//             return isSquare(x, y, ++n);
//         } else return n;
//     }

//     return Math.pow(answer, 2);
// }

// 2 - 효율성 탈락
// function solution(board) {
//     function isSquare(n) {
//         for (let x = 0; x <= board.length - n; x++) {
//             for (let y = 0; y <= board[0].length - n; y++) {
//                 let noZero = true;

//                 for (let z = 0; z < n; z++) {
//                     if (board[x + z].slice().splice(y, n).indexOf(0) !== -1) {
//                         noZero = false;
//                         break;
//                     }
//                 }

//                 if (noZero) return n;
//             }
//         }
//         return isSquare(n - 1);
//     }

//     return Math.pow(isSquare(board[0].length < board.length ? board[0].length : board.length), 2);
// }

// 3
function solution(board) {
    const x = board[0].length;
    const y = board.length;
    let answer = 0;

    if (x === 1) {
        for (const i of board) {
            if (i[0]) return 1;
        }
        return 0;
    }

    if (y === 1) {
        return board[0].indexOf(1) === -1 ? 0 : 1;
    }

    for (let i = 1; i < y; i++) {
        for (let j = 1; j < x; j++) {
            if (board[i][j] > 0) {
                board[i][j] = Math.min(board[i - 1][j - 1], board[i][j - 1], board[i - 1][j]) + 1;
            }
            if (answer < board[i][j]) {
                answer = board[i][j];
            }
        }
    }

    return Math.pow(answer, 2);
}

console.log(solution([[1], [1]]));
console.log(
    solution([
        [0, 0, 1, 1, 0],
        [1, 1, 1, 1, 1],
        [1, 1, 1, 1, 1],
        [1, 1, 1, 1, 1],
        [0, 1, 1, 1, 1],
    ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## N개의 최소공배수

[연습문제 > N개의 최소공배수](https://programmers.co.kr/learn/courses/30/lessons/12953)

``` js
const gcd = (a, b) => {
    return b ? gcd(b, a % b) : Math.abs(a);
};

function solution(words) {
    return words.reduce((r, c) => (r * c) / gcd(r, c));
}

console.log(solution([2, 6, 8, 14]));
console.log(solution([1, 2, 3]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## JadenCase 문자열 만들기

[연습문제 > JadenCase 문자열 만들기](https://programmers.co.kr/learn/courses/30/lessons/12951)

``` js
function solution(s) {
    return s
        .split(' ')
        .map((str) => str.charAt(0).toUpperCase() + str.slice(1).toLowerCase())
        .join(' ');
}

console.log(solution('3people  unFollowed me'));
console.log(solution('for the last week'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 행렬의 곱셈

[연습문제 > 행렬의 곱셈](https://programmers.co.kr/learn/courses/30/lessons/12949)

``` js
// 1
// function solution(arr1, arr2) {
//     const sizeX = arr2[0].length;
//     const count = arr2.length;

//     return arr1.reduce((r, c) => {
//         const tempArray = [];
//         for (let j = 0; j < sizeX; j++) {
//             let temp = 0;
//             for (let k = 0; k < count; k++) {
//                 temp += c[k] * arr2[k][j];
//             }
//             tempArray.push(temp);
//         }
//         return [...r, tempArray];
//     }, []);
// }

// 2 - Refactoring
function solution(arr1, arr2) {
    return arr1.map((a) => arr2[0].map((_, i) => arr2.reduce((r, c, j) => (r += a[j] * c[i]), 0)));
}

console.log(
    solution(
        [
            [1, 4],
            [3, 2],
            [4, 1],
        ],
        [
            [3, 3],
            [3, 3],
        ],
    ),
);
console.log(
    solution(
        [
            [-2, 2],
            [1, 2],
            [1, 2],
            [1, 2],
            [1, 2],
        ],
        [
            [1, 1, 1, 1, 1, 1],
            [1, 1, 1, 1, 1, 1],
        ],
    ),
);
console.log(
    solution(
        [
            [1, 4, 3],
            [3, 2, 3],
            [3, 2, 3],
        ],
        [
            [3, 3],
            [3, 3],
            [3, 3],
        ],
    ),
);
console.log(
    solution(
        [
            [2, 3, 2],
            [4, 2, 4],
            [3, 1, 4],
        ],
        [
            [5, 4, 3],
            [2, 4, 1],
            [3, 1, 1],
        ],
    ),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 피보나치 수

[연습문제 > 피보나치 수](https://programmers.co.kr/learn/courses/30/lessons/12945)

``` js
function solution(n) {
    let history = 0;
    let answer = 1;

    for (let i = 1; i < n; i++) {
        const temp = (history + answer) % 1234567;
        history = answer;
        answer = temp;
    }

    return answer;
}

console.log(solution(3));
console.log(solution(5));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 최솟값 만들기

[연습문제 > 최솟값 만들기](https://programmers.co.kr/learn/courses/30/lessons/12941)

``` js
function solution(A, B){
    A.sort((a, b) => a - b);
    B.sort((a, b) => b - a);

    return A.reduce((r, c, i) => r + c * B[i], 0);
}

console.log(solution([1, 4, 2], [5, 4, 4]));
console.log(solution([1, 2], [3, 4]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 숫자의 표현

[연습문제 > 숫자의 표현](https://programmers.co.kr/learn/courses/30/lessons/12924)

``` js
// 1
// function solution(n) {
//     let answer = 1;

//     for (let i = 1; i < n / 2; i++) {
//         let temp = i;
//         let num = i;
//         while (temp < n) temp += ++num;
//         if (temp === n) answer++;
//     }

//     return answer;
// }

// 2 - Refactoring
/* 
    프로그래머스 - 다른 사람의 풀이 참고
    홀수인 약수의 개수를 찾으면 된다.
*/
function solution(n) {
    let answer = n % 2 ? 1 : 0;

    for (let i = 1; i < n / 2; i++) {
        if (!(n % i) && i % 2) answer++;
    }

    return answer;
}

console.log(solution(15));
console.log(solution(16));
console.log(solution(17));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 땅따먹기

[연습문제 > 땅따먹기](https://programmers.co.kr/learn/courses/30/lessons/12913)

``` js
function solution(land) {
    const size = 4;
    const answer = land[0];

    for (let i = 1; i < land.length; i++) {
        const tempI = answer.slice();
        for (let j = 0; j < size; j++) {
            const tempJ = tempI.slice();
            tempJ.splice(j, 1);
            answer[j] = land[i][j] + Math.max(...tempJ);
        }
    }

    return Math.max(...answer);
}

console.log(
    solution([
        [1, 2, 3, 5],
        [5, 6, 7, 8],
        [4, 3, 2, 1],
    ])
);
console.log(
    solution([
        [4, 3, 2, 1],
        [2, 2, 2, 1],
        [6, 6, 6, 4],
        [8, 7, 6, 5],
    ])
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 탑

사라진문제 > 스택/큐 > 탑

``` js
// 1
// function solution(heights) {
//     const answer = [];

//     while (heights.length) {
//         let temp = heights.pop();
//         let index = 0;
//         for (let x = heights.length - 1; x >= 0; x--) {
//             if (temp < heights[x]) {
//                 index = x + 1;
//                 break;
//             }
//         }
//         answer.unshift(index);
//     }

//     return answer;
// }

// 2 - Refactoring
function solution(heights) {
    return heights.map((v, i) => {
        while (i--) {
            if (heights[i] > v) return i + 1;
        }

        return 0;
    });
}

console.log(solution([6, 9, 5, 7, 4]));
console.log(solution([3, 9, 9, 3, 5, 7, 2]));
console.log(solution([1, 5, 3, 6, 7, 6, 5]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>

## 쇠막대기

사라진문제 > 스택/큐 > 쇠막대기

``` js
// 1
// function solution(arrangement) {
//     let location = 0;

//     return arrangement.split('').reduce((result, a, i) => {
//         if (a === '(' && arrangement[i+1] === '(') location++;
//         else if (a === ')' && arrangement[i-1] === '(') result += location;
//         else if (a === ')' && arrangement[i-1] === ')') {
//             location--;
//             result++;
//         }
//         return result;
//     },0)
// }

// 2 - Refactoring
function solution(arrangement) {
    let answer = 0;
    let stack = 0;

    arrangement = arrangement.replace(/\(\)/g, 0);

    for (let i = 0; i < arrangement.length; i++) {
        switch (arrangement[i]) {
            case '(':
                stack++;
                break;
            case '0':
                answer += stack;
                break;
            case ')':
                stack--;
                answer++;
                break;
        }
    }

    return answer;
}

console.log(solution('()(((()())(())()))(())'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)

</br></br>