## 문자열 압축

[2020 KAKAO BLIND RECRUITMENT > 문자열 압축](https://programmers.co.kr/learn/courses/30/lessons/60057)

```js
// 1
// function solution(s) {
//     const length = s.length;
//     let answer = length;

//     for (let i = 1; i <= length / 2; i++) {
//         const dupli = [];
//         let dupliLength = 0;

//         for (let j = 0; j < length; j += i) {
//             const str = s.slice(j, j + i);
//             if (dupli[dupli.length - 1] && dupli[dupli.length - 1][0] === str) {
//                 dupli[dupli.length - 1][1]++;
//             } else {
//                 dupli.push([str, 1]);
//             }
//         }

//         for (const j of dupli) {
//             dupliLength += j[1] > 1 ? j[0].length + (j[1] + '').length : j[0].length;
//         }

//         answer = dupliLength < answer ? dupliLength : answer;
//     }

//     return answer;
// }

// 2 - Refactoring
function solution(s) {
  const length = s.length;
  let answer = length;

  for (let i = 1; i <= length / 2; i++) {
    let tempStr = s.slice(0, 0 + i);
    let dupliCount = 1;
    let result = 0;

    for (let j = i; j < length; j += i) {
      const str = s.slice(j, j + i);
      if (tempStr === str) {
        dupliCount++;
      } else {
        result += dupliCount > 1 ? i + (dupliCount + "").length : i;
        tempStr = str;
        dupliCount = 1;
      }
    }
    result += dupliCount > 1 ? i + (dupliCount + "").length : tempStr.length;

    answer = result < answer ? result : answer;
  }

  return answer;
}

console.log(solution("aabbaccc"));
console.log(solution("ababcdcdababcdcd"));
console.log(solution("abcabcdede"));
console.log(solution("aaaaaaaaabbbaaaaaaaaabbb"));
console.log(solution("abcabcabcabcdededededede"));
console.log(solution("xababcdcdababcdcd"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
