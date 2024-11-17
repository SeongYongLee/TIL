## 시저 암호

[연습문제 > 시저 암호](https://programmers.co.kr/learn/courses/30/lessons/12926)

```js
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

console.log(solution("AB", 1));
console.log(solution("z", 1));
console.log(solution("a B z", 4));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
