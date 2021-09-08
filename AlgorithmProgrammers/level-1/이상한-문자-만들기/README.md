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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)