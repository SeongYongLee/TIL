# AlgorithmProgrammers - Level 1

* [2019 카카오 개발자 겨울 인턴십 > 크레인 인형뽑기 게임](#크레인-인형뽑기-게임)

* [2020 카카오 인턴십 > 키패드 누르기](#키패드-누르기)

* [2021 KAKAO BLIND RECRUITMENT > 신규 아이디 추천](#신규-아이디-추천)

* [2021 Dev-Matching: 웹 백엔드 개발자(상반기) > 로또의 최고 순위와 최저 순위](#로또의-최고-순위와-최저-순위)

* [월간 코드 챌린지 시즌1 > 내적](#내적)

* [월간 코드 챌린지 시즌1 > 3진법 뒤집기](#3진법-뒤집기)

* [월간 코드 챌린지 시즌2 > 음양 더하기](#음양-더하기)

* [월간 코드 챌린지 시즌2 > 약수의 개수와 덧셈](#약수의-개수와-덧셈)

* [찾아라 프로그래밍 마에스터 > 폰켓몬](#폰켓몬)

* [해시 > 완주하지 못한 선수](#완주하지-못한-선수)

* [완전탐색 > 모의고사](#모의고사)

* [탐욕법(Greedy) > 체육복](#체육복)

* [정렬 > K번째 수](#K번째-수)

* [연습문제 > 2016년](#2016년)

* [연습문제 > 가운데 글자 가져오기](#가운데-글자-가져오기)

* [연습문제 > 두 정수 사이의 합](#두-정수-사이의-합)

* [연습문제 > 제일 작은 수 제거하기](#제일-작은-수-제거하기)

* [연습문제 > 하샤드 수](#하샤드-수)

* [연습문제 > 같은 숫자는 싫어](#같은-숫자는-싫어)

* [연습문제 > 나누어 떨어지는 숫자 배열](#나누어-떨어지는-숫자-배열)

* [연습문제 > 문자열 내 마음대로 정렬하기](#문자열-내-마음대로-정렬하기)

* [연습문제 > 문자열 내 p와 y의 개수](#문자열-내-p와-y의-개수)

* [연습문제 > 문자열 내림차순으로 배치하기](#문자열-내림차순으로-배치하기)

* [연습문제 > 문자열 다루기 기본](#문자열-다루기-기본)

* [연습문제 > 서울에서 김서방 찾기](#서울에서-김서방-찾기)

* [연습문제 > 소수 찾기](#소수-찾기)

* [연습문제 > 수박수박수박수박수박수?](#수박수박수박수박수박수)

* [연습문제 > 문자열을 정수로 바꾸기](#문자열을-정수로-바꾸기)

* [연습문제 > 시저 암호](#시저-암호)

* [연습문제 > 약수의 합](#약수의-합)

* [연습문제 > 이상한 문자 만들기](#이상한-문자-만들기)

* [연습문제 > 자릿수 더하기](#자릿수-더하기)

* [연습문제 > 자연수 뒤집어 배열로 만들기](#자연수-뒤집어-배열로-만들기)

* [연습문제 > 정수 내림차순으로 배치하기](#정수-내림차순으로-배치하기)

* [연습문제 > 정수 제곱근 판별](#정수-제곱근-판별)

* [연습문제 > 제일 작은 수 제거하기](#제일-작은-수-제거하기)

* [연습문제 > 짝수와 홀수](#짝수와-홀수)

* [연습문제 > 정수 제곱근 판별](#정수-제곱근-판별)

* [연습문제 > 제일 작은 수 제거하기](#제일-작은-수-제거하기)

* [연습문제 > 짝수와 홀수](#짝수와-홀수)

* [연습문제 > 최대공약수와 최소공배수](#최대공약수와-최소공배수)

* [연습문제 > 콜라츠 추측](#콜라츠-추측)

* [연습문제 > 평균 구하기](#평균-구하기)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)

## 크레인 인형뽑기 게임

[2019 카카오 개발자 겨울 인턴십 > 크레인 인형뽑기 게임](https://programmers.co.kr/learn/courses/30/lessons/64061)

``` js
// 1
// function solution(board, moves) {
//     let answer = 0;
//     const result = [];

//     for (let x = 0; x < moves.length; x++) {
//         const temp = moves[x] - 1;
//         for (let y = 0; y < board.length; y++) {
//             if (board[y][temp]) {
//                 if (result && result[result.length - 1] === board[y][temp]) {
//                     result.pop();
//                     answer += 2;
//                 } else {
//                     result.push(board[y][temp]);
//                 }
//                 board[y][temp] = 0;
//                 break;
//             }
//         }
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

// 3 - Refactoring
function solution(board, moves) {
    let answer = 0;
    const result = [];

    const filter = board.reduce(
        (result, x) => x.map((y, i) => y !== 0 ? [...(result[i] || []), y] : result[i]),
        [],
    );

    for (let x = 0; x < moves.length; x++) {
        const temp = filter[moves[x] - 1].shift();
        if (!temp) continue;
        if (temp === result[result.length - 1]) {
            result.pop();
            answer += 2;
            continue;
        }
        result.push(temp);
    }

    return answer;
}

console.log(
    solution(
        [
            [0, 0, 0, 0, 0],
            [0, 0, 1, 0, 3],
            [0, 2, 5, 0, 1],
            [4, 2, 4, 4, 2],
            [3, 5, 1, 3, 1],
        ],
        [1, 5, 3, 5, 1, 2, 1, 4],
    ),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 키패드 누르기

[2020 카카오 인턴십 > 키패드 누르기](https://programmers.co.kr/learn/courses/30/lessons/67256)

``` js
function solution(numbers, hand) {
    // 10 = *, 11 = 0, 12 = #
    let leftFinger = 10;
    let rightFinger = 12;
    let answer = '';

    const moveLeftFinger = (n) => {
        answer += 'L';
        leftFinger = n;
    };
    const moveRightFinger = (n) => {
        answer += 'R';
        rightFinger = n;
    };
    const setDistance = (n) => {
        if ([0].includes(n)) {
            return 0;
        } else if ([1, 3].includes(n)) {
            return 1;
        } else if ([2, 4, 6].includes(n)) {
            return 2;
        } else if ([5, 7, 9].includes(n)) {
            return 3;
        } else {
            // [8,10].includes(n)
            return 4;
        }
    };

    for (let n of numbers) {
        if (n === 0) n = 11;

        if ([1, 4, 7].includes(n)) {
            moveLeftFinger(n);
        } else if ([3, 6, 9].includes(n)) {
            moveRightFinger(n);
        } else {
            // [2,5,8,11].includes(n)
            const left = setDistance(Math.abs(leftFinger - n));
            const right = setDistance(Math.abs(rightFinger - n));

            if (left < right) {
                moveLeftFinger(n);
            } else if (left > right) {
                moveRightFinger(n);
            } else {
                hand === 'left' ? moveLeftFinger(n) : moveRightFinger(n);
            }
        }
        // console.log(n, leftFinger, rightFinger);
    }

    return answer;
}

console.log(solution([1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5], 'right'));
console.log(solution([7, 0, 8, 2, 8, 3, 1, 5, 7, 6, 2], 'left'));
console.log(solution([1, 2, 3, 4, 5, 6, 7, 8, 9, 0], 'right'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 신규 아이디 추천

[2021 KAKAO BLIND RECRUITMENT > 신규 아이디 추천](https://programmers.co.kr/learn/courses/30/lessons/72410)

``` js
// 1
// function solution(new_id) {
//     const low_new_id = new_id.toLowerCase(); // 1

//     let answer = '';
//     let history = '';

//     for (let i = 0; i < low_new_id.length; i++) {
//         const charCode = low_new_id[i].charCodeAt();

//         if (
//             Number.isInteger(+low_new_id[i]) ||
//             (charCode >= 97 && charCode <= 122) ||
//             [45, 95].includes(charCode) ||
//             (charCode === 46 && history !== low_new_id[i]) // 2, 3
//         ) {
//             answer += low_new_id[i];
//             history = low_new_id[i];
//         }
//     }

//     if (answer[0] === '.') answer = answer.slice(1); // 4
//     answer = answer.slice(0, 15); // 6
//     if (answer[answer.length - 1] === '.') answer = answer.slice(0, answer.length - 1); // 4, 6
//     if (!answer) answer = 'a'; // 5

//     const len = answer.length;

//     return len > 2 ? answer : answer + answer.charAt(len - 1).repeat(3 - len);
// }

// 2 - 정규 표현식
// function solution(new_id) {
//     const answer = new_id
//         .toLowerCase() // 1
//         .replace(/[^\w-.]/g, '') // 2
//         .replace(/\.+/g, '.') // 3
//         .replace(/^\./g, '') // 4
//         .slice(0, 15) // 6
//         .replace(/\.$/g, '') // 4
//         .replace(/^$/, 'a'); // 5

//     const len = answer.length;

//     return len > 2 ? answer : answer + answer.charAt(len - 1).repeat(3 - len); // 7
// }

// 3 - 정규 표현식 + padEnd
function solution(new_id) {
    const answer = new_id
        .toLowerCase() // 1
        .replace(/[^\w-.]/g, '') // 2
        .replace(/\.+/g, '.') // 3
        .replace(/^\./g, '') // 4
        .slice(0, 15) // 6
        .replace(/\.$/g, '') // 4
        .padEnd(1, 'a') // 5

    const len = answer.length;

    return answer.padEnd(3, answer[len - 1]); // 7
}

console.log(solution('...!@BaT#*..y.abcdefghijklm'));
console.log(solution('z-+.^.'));
console.log(solution());
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 내적

[2021 Dev-Matching: 웹 백엔드 개발자(상반기) > 로또의 최고 순위와 최저 순위](https://programmers.co.kr/learn/courses/30/lessons/77484)

``` js
// 1
// function solution(lottos, win_nums) {
//     let minimumRank = 7;
//     let highestRank = 0;

//     for (let i = 0; i < lottos.length; i++) {
//         if (lottos[i] === 0) {
//             highestRank++;
//             continue;
//         }

//         if (win_nums.includes(lottos[i])) minimumRank--;
//     }

//     highestRank = minimumRank - highestRank;

//     return [highestRank === 7 ? 6 : highestRank, minimumRank === 7 ? 6 : minimumRank];
// }

// 2 - Refactoring
function solution(lottos, win_nums) {
    const rank = [6, 6, 5, 4, 3, 2, 1];
    let minimumCount = 0;
    let unknowCount = 0;

    for (let i = 0; i < lottos.length; i++) {
        if (lottos[i] === 0) {
            unknowCount++;
        } else if (win_nums.includes(lottos[i])) {
            minimumCount++;
        }
    }

    return [rank[minimumCount + unknowCount], rank[minimumCount]];
}

console.log(solution([44, 1, 0, 0, 31, 25], [31, 10, 45, 1, 6, 19]));
console.log(solution([0, 0, 0, 0, 0, 0], [38, 19, 20, 40, 15, 25]));
console.log(solution([45, 4, 35, 20, 3, 9], [20, 9, 3, 45, 4, 35]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 내적

[월간 코드 챌린지 시즌1 > 내적](https://programmers.co.kr/learn/courses/30/lessons/70128)

``` js
function solution(a, b) {
    return a.reduce((r, _, i) => r + a[i] * b[i], 0);
}

console.log(solution([1, 2, 3, 4], [-3, -1, 0, 2]));
console.log(solution([-1, 0, 1], [1, 0, -1]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 3진법 뒤집기

[월간 코드 챌린지 시즌1 > 3진법 뒤집기](https://programmers.co.kr/learn/courses/30/lessons/68935)

``` js
function solution(a, b) {
    return a.reduce((r, _, i) => r + a[i] * b[i], 0);
}

console.log(solution(45));
console.log(solution(125));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 음양 더하기

[월간 코드 챌린지 시즌2 > 음양 더하기](https://programmers.co.kr/learn/courses/30/lessons/76501)

``` js
function solution(absolutes, signs) {
    return absolutes.reduce((r, c, i) => r + (signs[i] ? +c : -c), 0);
}

console.log(solution([4, 7, 12], [true, false, true]));
console.log(solution([1, 2, 3], [false, false, true]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 약수의 개수와 덧셈

[월간 코드 챌린지 시즌2 > 약수의 개수와 덧셈](https://programmers.co.kr/learn/courses/30/lessons/77884)

``` js
// 1
// function solution(left, right) {
//     let answer = 0;

//     for (let x = left; x <= right; x++) {
//         let count = 0;
//         let last = x;

//         for (let y = 0; y < last; y++) {
//             const temp = x / y;

//             if (Number.isInteger(temp)) {
//                 count += temp === y ? 1 : 2;
//             }

//             last = temp;
//         }
//         answer += count % 2 ? -x : x;
//     }

//     return answer;
// }

// 2
/* 
    Refactoring 제곱근이 정수면 약수의 갯수가 홀수이다.
*/
function solution(left, right) {
    let answer = 0;

    for (let x = left; x <= right; x++) {
        answer += Number.isInteger(Math.sqrt(x)) ? -x : x;
    }

    return answer;
}

console.log(solution(13, 17));
console.log(solution(24, 27));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 폰켓몬

[찾아라 프로그래밍 마에스터 > 폰켓몬](https://programmers.co.kr/learn/courses/30/lessons/1845)

``` js
function solution(nums) {
    const numCount = new Set(nums).size;
    const numMax = nums.length / 2;
    
    return numCount > numMax ? numMax : numCount;
}

console.log(solution([3, 1, 2, 3]));
console.log(solution([3, 3, 3, 2, 2, 4]));
console.log(solution([3, 3, 3, 2, 2, 2]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 완주하지 못한 선수

[해시 > 완주하지 못한 선수](https://programmers.co.kr/learn/courses/30/lessons/42576)

``` js
// 1
// function solution(participant, completion) {
//     participant.sort();
//     completion.sort();

//     const pLength = participant.length;

//     for (let i = 0; i < pLength; i++) {
//         if (participant[i] !== completion[i]) return participant[i];
//     }
// }

// 2 - 해시 (Key-value pair)
/* 
    프로그래머스 - 다른 사람의 풀이 참고
    var solution=(_,$)=>_.find(_=>!$[_]--,$.map(_=>$[_]=($[_]|0)+1))
*/
function solution(participant, completion) {
    completion.map((name) => (completion[name] = (completion[name] | 0) + 1));

    return participant.find((name) => !completion[name]--);
}

console.log(solution(['leo', 'kiki', 'eden'], ['eden', 'kiki']));
console.log(
    solution(
        ['marina', 'josipa', 'nikola', 'vinko', 'filipa'],
        ['josipa', 'filipa', 'marina', 'nikola'],
    ),
);
console.log(solution(['mislav', 'stanko', 'mislav', 'ana'], ['stanko', 'ana', 'mislav']));
console.log(
    solution(
        ['mislav', 'stanko', 'mislav', 'ana', 'mislav', 'stanko'],
        ['mislav', 'stanko', 'mislav', 'ana', 'mislav'],
    ),
);
console.log(
    solution(
        ['mislav', 'stanko', 'mislav', 'ana', 'mislav'],
        ['stanko', 'ana', 'mislav', 'mislav'],
    ),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 모의고사

[완전탐색 > 모의고사](https://programmers.co.kr/learn/courses/30/lessons/42840)

``` js
// 1
// function solution(answers) {
//     const supos = [
//         [1, 2, 3, 4, 5],
//         [2, 1, 2, 3, 2, 4, 2, 5],
//         [3, 3, 1, 1, 2, 2, 4, 4, 5, 5],
//     ];

//     const result = supos.reduce((result, supo) => {
//         result.push(answers.filter((answer, j) => supo[j % supo.length] === answer).length);
//         return result;
//     }, []);

//     const max = Math.max.apply(null, result);

//     const answer = result.reduce((result, current, i) => {
//         if (current === max) result.push(i + 1);
//         return result;
//     }, []);

//     return answer;
// }

// 2 - Refactoring
function solution(answers) {
    const supos = [
        [1, 2, 3, 4, 5],
        [2, 1, 2, 3, 2, 4, 2, 5],
        [3, 3, 1, 1, 2, 2, 4, 4, 5, 5],
    ];
    const suposLength = supos.map((s) => s.length);

    const result = supos.reduce(
        (result, supo, i) => [
            ...result,
            answers.filter((answer, j) => supo[j % suposLength[i]] === answer).length,
        ],
        [],
    );

    const max = Math.max.apply(null, result);

    return result.reduce((result, c, i) => (c === max ? [...result, i + 1] : result), []);
}

console.log(solution([1, 2, 3, 4, 5]));
console.log(solution([1, 3, 2, 4, 2]));
console.log(solution([1, 2, 3, 4, 5, 1, 2, 3, 4, 5]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 체육복

[탐욕법(Greedy) > 체육복](https://programmers.co.kr/learn/courses/30/lessons/42862)

``` js
function solution(n, lost, reserve) {
    return lost.reduce((r, c) => {
        let a = reserve.indexOf(c);
        if (a !== -1) {
            reserve.splice(a, 1);
            return r;
        }
        a = reserve.indexOf(c - 1);
        if (a !== -1) {
            reserve.splice(a, 1);
            return r;
        }
        a = reserve.indexOf(c + 1);
        if (a !== -1 && lost.indexOf(c + 1) === -1) {
            reserve.splice(a, 1);
            return r;
        }
        return --r;
    }, n);
}

console.log(solution(5, [2, 4], [1, 3, 5]));
console.log(solution(5, [2, 4], [3]));
console.log(solution(3, [3], [1]));
console.log(solution(4, [4, 2], [1, 3]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## K번째 수

[정렬 > K번째 수](https://programmers.co.kr/learn/courses/30/lessons/42748)

``` js
function solution(array, commands) {
    return commands.reduce(
        (answer, c) => [...answer, array.slice(c[0] - 1, c[1]).sort((x, y) => x - y)[c[2] - 1]],
        [],
    );
}

console.log(
    solution(
        [1, 5, 2, 6, 3, 7, 4],
        [
            [2, 5, 3],
            [4, 4, 1],
            [1, 7, 3],
        ],
    ),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 2016년

[연습문제 > 2016년](https://programmers.co.kr/learn/courses/30/lessons/12901)

``` js
// 1
// function solution(a, b) {
//     const week = ['THU', 'FRI', 'SAT', 'SUN', 'MON', 'TUE', 'WED'];
//     const year = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
//     let temp = 0;

//     for (let x = 0; x < a - 1; x++) temp += year[x];
//     return week[(temp + b) % 7];
// }

// 2 - new Date
function solution(a, b) {
    return ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'][
        new Date('2016-' + a + '-' + b).getDay()
    ];
}

console.log(solution(5, 24));
console.log(solution(12, 31));
console.log(solution(1, 1));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 가운데 글자 가져오기

[연습문제 > 가운데 글자 가져오기](https://programmers.co.kr/learn/courses/30/lessons/12903)

``` js
function solution(s) {
    const length = s.length;
    const mid = length / 2;

    return s.slice(length % 2 === 0 ? mid - 1 : mid, mid + 1);
}

console.log(solution("abcde"));
console.log(solution("qwer"));
console.log(solution("abcdef"));
console.log(solution("a"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 두 정수 사이의 합

[연습문제 > 두 정수 사이의 합](https://programmers.co.kr/learn/courses/30/lessons/12912)

``` js
function solution(a, b) {
    const calc = (min, max) => {
        let answer = 0;
        
        for (let i = min; i <= max; i++) {
            answer += i;
        }
        
        return answer;
    }
    
    return a > b ? calc(b, a) : calc(a, b);
}

console.log(solution(3, 5));
console.log(solution(3, 3));
console.log(solution(5, 3));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 제일 작은 수 제거하기

[연습문제 > 제일 작은 수 제거하기](https://programmers.co.kr/learn/courses/30/lessons/12935)

``` js
function solution(arr) {
    arr.splice(arr.indexOf(Math.min(...arr)), 1);
    return arr.length ? arr : [-1];
}

console.log(solution([4, 3, 2, 1]));
console.log(solution([10]));
```

</br></br>

## 하샤드 수

[연습문제 > 하샤드 수](https://programmers.co.kr/learn/courses/30/lessons/12947)

``` js
function solution(x) {
    return !(x % (x + '').split('').reduce((i, j) => +i + +j));
}

console.log(solution(10));
console.log(solution(12));
console.log(solution(11));
console.log(solution(13));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 같은 숫자는 싫어

[연습문제 > 같은 숫자는 싫어](https://programmers.co.kr/learn/courses/30/lessons/12906)

``` js
function solution(arr) {
    const answer = [];
    const aLength = arr.length;
    
    for (let x = 0; x < aLength; x++) {
        if (arr[x] !== arr[x+1]) answer.push(arr[x]);
    }
    
    return answer;
}

console.log(solution([1, 1, 3, 3, 0, 1, 1]));
console.log(solution([4, 4, 4, 3, 3]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 나누어 떨어지는 숫자 배열

[연습문제 > 나누어 떨어지는 숫자 배열](https://programmers.co.kr/learn/courses/30/lessons/12910)

``` js
function solution(arr, divisor) {
    const answer = arr.filter(x => x % divisor === 0).sort((a, b) => a - b);
    
    return answer.length ? answer : [-1];
}

console.log(solution([5, 9, 7, 10], 5));
console.log(solution([2, 36, 1, 3], 1));
console.log(solution([3, 2, 6], 10));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 문자열 내 마음대로 정렬하기

[연습문제 > 문자열 내 마음대로 정렬하기](https://programmers.co.kr/learn/courses/30/lessons/12915)

``` js
function solution(strings, n) {
    return strings.sort((a, b) => 
                        a[n] === b[n] ? (a > b ? 1 : -1) : (a[n] > b[n] ? 1 : -1));
}

console.log(solution(["sun", "bed", "car"], 1));
console.log(solution(["abce", "abcd", "cdx"], 2));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 문자열 내 p와 y의 개수

[연습문제 > 문자열 내 p와 y의 개수](https://programmers.co.kr/learn/courses/30/lessons/12916)

``` js
// 1
// function solution(s) {
//     let answer = 0;

//     for (let i = 0; i < s.length; i++) {
//         if (s[i].toLowerCase() === 'p') answer++;
//         else if (s[i].toLowerCase() === 'y') answer--;
//     }

//     return answer === 0;
// }

// 2 - Refactoring 
function solution(s) {
    return (
        s.toUpperCase().split('P').length === s.toUpperCase().split('Y').length
    );
}

console.log(solution("pPoooyY"));
console.log(solution("Pyy"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 문자열 내림차순으로 배치하기

[연습문제 > 문자열 내림차순으로 배치하기](https://programmers.co.kr/learn/courses/30/lessons/12917)

``` js
function solution(s) {
    return s.split('').sort().reverse().join('');
}

console.log(solution("Zbcdefg"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 문자열 다루기 기본

[연습문제 > 문자열 다루기 기본](https://programmers.co.kr/learn/courses/30/lessons/12918)

``` js
function solution(s) {
    return [4, 6].includes(s.length) && +s + '' === s ? true : false;
}

console.log(solution("a234"));
console.log(solution("1234"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 서울에서 김서방 찾기

[연습문제 > 서울에서 김서방 찾기](https://programmers.co.kr/learn/courses/30/lessons/12919)

``` js
// 1
// function solution(seoul) {
//     return `김서방은 ${seoul.indexof('kim')}에 있다`;
// }

// 2 - 프로그래머스에서 템플릿 문자열 지원 X
function solution(seoul) {
    return '김서방은 ' + seoul.indexOf('Kim') + '에 있다';
}

console.log(solution(['Jane', 'Kim']));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 소수 찾기

[연습문제 > 소수 찾기](https://programmers.co.kr/learn/courses/30/lessons/12921)

``` js
// 1 - 효율성 테스트 탈락
// function solution(n) {
//     const sosu = [];

//     for (let x = 2; x < n + 1; x++) {
//         let thisSosu = true;

//         for (let y = 0; y < sosu.length; y++) {
//             if (x % sosu[y] === 0) {
//                 thisSosu = false;
//                 break;
//             }
//         }

//         if (thisSosu) sosu.push(x);
//     }

//     return sosu.length;
// }

// 2 - sqrt를 사용하여 효율성 증가
// function solution(n) {
//     const sosu = [];
//     const sqrt = Math.sqrt(n);
//     let sqrtsosu = 0;
//     let sqrtlength = 0;

//     for (let x = 2; x < n + 1; x++) {
//         let thisSosu = true;

//         for (let y = 0; y < sqrtlength; y++) {
//             if (x % sosu[y] === 0) {
//                 thisSosu = false;
//                 break;
//             }
//         }

//         if (thisSosu) {
//             sosu.push(x);
//             if (sqrtsosu === 0) {
//                 sqrtlength = sosu.length;
//                 if (x > sqrt) sqrtsosu = x;
//             }
//         }
//     }

//     return sosu.length;
// }

// 3 - 에라토스테네스의 체
function solution(nums) {
    const sqrt = Math.sqrt(nums);
    const arr = Array(nums + 1)
        .fill(true)
        .fill(false, 0, 2);

    for (let i = 2; i <= sqrt; i++) {
        if (!arr[i]) continue;

        for (let j = i * i; j <= nums; j += i) {
            arr[j] = false;
        }
    }

    return arr.filter((e) => e).length;
}

console.log(solution(10));
console.log(solution(5));
console.log(solution(100));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 수박수박수박수박수박수?

[연습문제 > 수박수박수박수박수박수?](https://programmers.co.kr/learn/courses/30/lessons/12922)

``` js
// 1
// function solution(n) {
//     let answer = '';

//     for (let x = 0; x < n; x++) {
//         answer += x % 2 === 0 ? '수' : '박';
//     }

//     return answer;
// }

// 2 - repeat 사용
function solution(n) {
    return '수박'.repeat(n / 2) + (n % 2 ? '수' : '');
}

console.log(solution(1));
console.log(solution(3));
console.log(solution(4));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 문자열을 정수로 바꾸기

[연습문제 > 문자열을 정수로 바꾸기](https://programmers.co.kr/learn/courses/30/lessons/12925)

``` js
function solution(s) {
    return +s;
}

console.log(solution("1234"));
console.log(solution("-1234"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 시저 암호

[연습문제 > 시저 암호](https://programmers.co.kr/learn/courses/30/lessons/12926)

``` js
// 1
// function solution(s, n) {
//     let answer = '';

//     const lowerCase = ['a'.charCodeAt(),'z'.charCodeAt()];
//     const upperCase = ['A'.charCodeAt(),'Z'.charCodeAt()];

//     for (let x = 0; x < s.length; x++) {
//        let temp = s[x].charCodeAt();

//        if (lowerCase[0] <= temp && temp <= lowerCase[1]) {
//            temp += n;
//            if (temp > lowerCase[1]) temp -= (lowerCase[1] - lowerCase[0] + 1);
//            answer += String.fromCharCode(temp);
//        } else if (upperCase[0] <= temp && temp <= upperCase[1]) {
//            temp += n;
//            if (temp > upperCase[1]) temp -= (upperCase[1] - upperCase[0] + 1);
//            answer += String.fromCharCode(temp);
//        } else answer += ' ';
//     }

//     return answer;
// }

// 2 - Refactoring
// function solution(s, n) {
//     let answer = '';

//     const lowerCase = ['a'.charCodeAt(), 'z'.charCodeAt()];
//     const upperCase = ['A'.charCodeAt(), 'Z'.charCodeAt()];

//     for (let x = 0; x < s.length; x++) {
//         let temp = s[x].charCodeAt();

//         if (temp === 32) {
//             answer += ' ';
//             continue;
//         }

//         if (temp >= lowerCase[0]) {
//             temp += n;
//             answer += String.fromCharCode(temp > lowerCase[1] ? temp - 26 : temp);
//         } else {
//             temp += n;
//             answer += String.fromCharCode(temp > upperCase[1] ? temp - 26 : temp);
//         }
//     }

//     return answer;
// }

// 3 - Refactoring
/* 
    프로그래머스 - 다른 사람의 풀이 참고
*/
// function solution(s, n) {
//     let answer = '';
//     const sLength = s.length;

//     for (let x = 0; x < sLength; x++) {
//         const temp = s[x].charCodeAt();

//         answer +=
//             temp === 32 ? ' ' : String.fromCharCode((temp & 96) + (((temp % 32) - 1 + n) % 26) + 1);
//     }

//     return answer;
// }

// 4 - 정규 표현식 + replace
/* 
    프로그래머스 - 다른 사람의 풀이 참고
    replace의 성능이 너무 좋다.
*/
function solution(s, n) {
    return s.replace(
        /[a-z]/gi,
        (c) =>
            [
                (c = c.charCodeAt(0)),
                String.fromCharCode((c & 96) + (((c % 32) + n - 1) % 26) + 1),
            ][1],
    );
}

console.log(solution('AB', 1));
console.log(solution('z', 1));
console.log(solution('a B z', 4));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 약수의 합

[연습문제 > 약수의 합](https://programmers.co.kr/learn/courses/30/lessons/12928)

``` js
function solution(n) {
    let answer = 0;
    let last = n;

    for (let x = 0; x < last; x++) {
        const temp = n / x;

        if (Number.isInteger(temp)) {
            answer += temp === x ? temp : temp + x;
        }

        last = temp;
    }

    return answer;
}

console.log(solution(12));
console.log(solution(5));
console.log(solution(600));
console.log(solution(1));
console.log(solution(0));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 이상한 문자 만들기

[연습문제 > 이상한 문자 만들기](https://programmers.co.kr/learn/courses/30/lessons/12930)

``` js
// 1
// function solution(s) {
//     return s
//         .split(' ')
//         .reduce((result, i) => {
//             for (let x = 0; x < i.length; x++) {
//                 result += x % 2 === 0 ? i[x].toUpperCase() : i[x].toLowerCase();
//             }
//             result += ' ';
//             return result;
//         }, '')
//         .substring(0, s.length);
// }

// 2 - Refactoring
// function solution(s) {
//     return s
//         .split(' ')
//         .map((x) =>
//             x
//                 .split('')
//                 .map((y, i) => (i % 2 === 0 ? y.toUpperCase() : y.toLowerCase()))
//                 .join(''),
//         )
//         .join(' ');
// }

// 3 - Refactoring
function solution(s) {
    let answer = '';
    const sLength = s.length;
    let count = 0;

    for (let i = 0; i < sLength; i++) {
        if (s[i] === ' ') {
            answer += ' ';
            count = 0;
        } else {
            answer += count % 2 === 0 ? s[i].toUpperCase() : s[i].toLowerCase();
            count++;
        }
    }

    return answer;
}

console.log(solution('try hello world'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 자릿수 더하기

[연습문제 > 자릿수 더하기](https://programmers.co.kr/learn/courses/30/lessons/12931)

``` js
function solution(n) {
    return (n + '').split('').reduce((r, i) => r + +i, 0);
}

console.log(solution(123));
console.log(solution(987));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 자연수 뒤집어 배열로 만들기

[연습문제 > 자연수 뒤집어 배열로 만들기](https://programmers.co.kr/learn/courses/30/lessons/12932)

``` js
// 1
function solution(n) {
    return (n + '')
        .split('')
        .reverse()
        .map((x) => +x);
}

// 2 - Refactoring (더 느려짐)
// function solution(n) {
//     return (n + '').split('').reduce((r, c) => [+c, ...r], []);
// }

console.log(solution(12345));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 정수 내림차순으로 배치하기

[연습문제 > 정수 내림차순으로 배치하기](https://programmers.co.kr/learn/courses/30/lessons/12933)

``` js
function solution(n) {
    return +(n + '')
        .split('')
        .sort((x, y) => y - x)
        .join('');
}

console.log(solution(118372));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 정수 제곱근 판별

[연습문제 > 정수 제곱근 판별](https://programmers.co.kr/learn/courses/30/lessons/12934)

``` js
function solution(n) {
    const sqrtN = Math.sqrt(n);
    return Number.isInteger(sqrtN) ? Math.pow(sqrtN + 1, 2) : -1;
}

console.log(solution(121));
console.log(solution(3));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 제일 작은 수 제거하기

[연습문제 > 제일 작은 수 제거하기](https://programmers.co.kr/learn/courses/30/lessons/12935)

``` js
function solution(arr) {
    if (arr.length === 1) return [-1]; 
    
    arr.splice(arr.indexOf(Math.min(...arr)), 1);
    return arr;
}

console.log(solution([4, 3, 2, 1]));
console.log(solution([10]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 짝수와 홀수

[연습문제 > 짝수와 홀수](https://programmers.co.kr/learn/courses/30/lessons/12937)

``` js
function solution(num) {
    return num % 2 === 0 ? 'Even' : 'Odd';
}

console.log(solution(3));
console.log(solution(4));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 최대공약수와 최소공배수

[연습문제 > 최대공약수와 최소공배수](https://programmers.co.kr/learn/courses/30/lessons/12940)

``` js
// 1
// function solution(n, m) {
//     let max = 1;

//     for (let x = m > n ? n : m; x > 1; x--) {
//         if (Number.isInteger(n / x) && Number.isInteger(m / x)) {
//             max = x;
//             break;
//         }
//     }

//     return [max, (m * n) / max];
// }

// 2 - 유클리드 호제법
function solution(n, m) {
    const greatestCommonDivisor = (a, b) => {
        console.log(a, b);
        return b ? greatestCommonDivisor(b, a % b) : Math.abs(a);
    };

    const greatestCommon = greatestCommonDivisor(n, m);
    return [greatestCommon, (n * m) / greatestCommon];
}

console.log(solution(3, 12));
console.log(solution(2, 5));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 콜라츠 추측

[연습문제 > 콜라츠 추측](https://programmers.co.kr/learn/courses/30/lessons/12943)

``` js
function solution(num) {
    for (let answer = 0; answer < 500; answer++) {
        if (num === 1) return answer;
        num = num % 2 === 0 ? num / 2 : num * 3 + 1;
    }
    return -1;
}

console.log(solution(6));
console.log(solution(16));
console.log(solution(626331));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>

## 평균 구하기

[연습문제 > 평균 구하기](https://programmers.co.kr/learn/courses/30/lessons/12944)

``` js
function solution(arr) {
    return arr.reduce((r, c) => r + c) / arr.length;
}

console.log(solution([1, 2, 3, 4]));
console.log(solution([5, 5]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)

</br></br>