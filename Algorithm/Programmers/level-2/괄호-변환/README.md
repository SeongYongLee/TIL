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

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)