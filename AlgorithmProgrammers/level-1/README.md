# AlgorithmProgrammers - Level 1

* [크레인 인형뽑기 게임](#크레인-인형뽑기-게임)
* [신규 아이디 추천](#신규-아이디-추천)
* [완주하지 못한 선수](#완주하지-못한-선수)

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
        (result, x) => x.map((y, i) => y !== 0 ? [...(result[i] || []), y] : result[i] || []),
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

// 2 - 해시 (Key-value pair), 
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