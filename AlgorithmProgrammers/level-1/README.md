# AlgorithmProgrammers - Level 1

* [크레인 인형뽑기 게임](#크레인-인형뽑기-게임)
* [신규 아이디 추천](#신규-아이디-추천)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)

## 크레인 인형뽑기 게임

[2019 카카오 개발자 겨울 인턴십 > 크레인 인형뽑기 게임](https://programmers.co.kr/learn/courses/30/lessons/64061)


``` js
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
function solution(new_id) {
    const low_new_id = new_id.toLowerCase(); // 1

    let answer = '';
    let history = '';

    for (let i = 0; i < low_new_id.length; i++) {
        const charCode = low_new_id[i].charCodeAt();

        if (
            Number.isInteger(+low_new_id[i]) ||
            (charCode >= 97 && charCode <= 122) ||
            [45, 95].includes(charCode) ||
            (charCode === 46 && history !== low_new_id[i]) // 2, 3
        ) {
            answer += low_new_id[i];
            history = low_new_id[i];
        }
    }

    if (answer[0] === '.') answer = answer.slice(1); // 4
    answer = answer.slice(0, 15); // 6
    if (answer[answer.length - 1] === '.') answer = answer.slice(0, answer.length - 1); // 4, 6
    if (!answer) answer = 'a'; // 5

    const len = answer.length;

    return len > 2 ? answer : answer + answer.charAt(len - 1).repeat(3 - len);
}

// 정규 표현식 풀이
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

console.log(solution('...!@BaT#*..y.abcdefghijklm'));
console.log(solution('z-+.^.'));
console.log(solution());
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)