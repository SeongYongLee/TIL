## n^2 배열 자르기

- [월간 코드 챌린지 시즌3 > n^2 배열 자르기](https://programmers.co.kr/learn/courses/30/lessons/87390)

```js
// 1 (시간 초과)
// function solution(n, left, right) {
//     const answer = [];

//     for (let i = 1; i < n + 1; i++) {
//         for (let j = 1; j < n + 1; j++) {
//             answer.push(i < j ? j : i);
//         }
//     }

//     return answer.splice(left, right - left + 1);
// }

// 2 (시간 초과)
// function solution(n, left, right) {
//     const answer = [];
//     let count = 0;

//     for (let i = 1; i < n + 1; i++) {
//         for (let j = 1; j < n + 1; j++) {
//             if (++count > left) {
//                 if (count < right + 2) answer.push(i < j ? j : i);
//                 else return answer;
//             }
//         }
//     }
// }

// 3 (시간 초과)
// function solution(n, left, right) {
//     const nLength = n + 1;
//     const answer = [];
//     const answerLastLength = right - left;
//     let answerLength = 0;
//     let count = 0;

//     for (let i = 1; i < nLength; i++) {
//         for (let j = 1; j < nLength; j++) {
//             if (++count > left) {
//                 answer.push(i < j ? j : i);
//                 if (answerLength++ === answerLastLength) return answer;
//             }
//         }
//     }
// }

// 4
function solution(n, left, right) {
  const nLength = n + 1;
  const answer = [];
  const answerLastLength = right - left + 1;
  let answerLength = 0;
  let i = Math.floor((left + 1) / n);
  let count = (i - 1) * n;

  for (i; i < nLength; i++) {
    for (let j = 1; j < nLength; j++) {
      if (++count > left) {
        answer.push(i < j ? j : i);
        if (++answerLength === answerLastLength) return answer;
      }
    }
  }
}

console.log(solution(3, 2, 5));
console.log(solution(4, 7, 14));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
