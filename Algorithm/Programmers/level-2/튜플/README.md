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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)