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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)