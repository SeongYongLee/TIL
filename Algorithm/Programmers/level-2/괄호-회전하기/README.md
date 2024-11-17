## 괄호 회전하기

[월간 코드 챌린지 시즌2 > 괄호 회전하기](https://programmers.co.kr/learn/courses/30/lessons/76502)

```js
// 1
// function solution(words) {
//     const isCorrect = (i) => {
//         const stack = [];

//         for (let a = i; a < wLength; a++) {
//             if (!sol(stack, words[a])) return false;
//         }

//         for (let b = 0; b < i; b++) {
//             if (!sol(stack, words[b])) return false;
//         }

//         return !stack.length;
//     };

//     const sol = (stack, word) => {
//         switch (word) {
//             case ']':
//                 if (stack[stack.length - 1] === '[') stack.pop();
//                 else return false;
//                 break;
//             case '}':
//                 if (stack[stack.length - 1] === '{') stack.pop();
//                 else return false;
//                 break;
//             case ')':
//                 if (stack[stack.length - 1] === '(') stack.pop();
//                 else return false;
//                 break;
//             default:
//                 stack.push(word);
//                 break;
//         }

//         return true;
//     };

//     const wLength = words.length;
//     let answer = 0;

//     for (let i = 0; i < wLength; i++) {
//         if (isCorrect(i)) answer++;
//     }

//     return answer;
// }

// 2 - Refactoring
function solution(words) {
  const pair = { "]": "[", "}": "{", ")": "(" };

  const isCorrect = (i) => {
    const stack = [];

    for (let a = i; a < wLength; a++) {
      if (!sol(stack, words[a])) return false;
    }

    for (let b = 0; b < i; b++) {
      if (!sol(stack, words[b])) return false;
    }

    return !stack.length;
  };

  const sol = (stack, word) => {
    if (["]", ")", "}"].includes(word)) {
      if (stack[stack.length - 1] === pair[word]) stack.pop();
      else return false;
    } else {
      stack.push(word);
    }

    return true;
  };

  let answer = 0;
  const wLength = words.length;

  for (let i = 0; i < wLength; i++) {
    if (isCorrect(i)) answer++;
  }

  return answer;
}

console.log(solution("[](){}"));
console.log(solution("}]()[{"));
console.log(solution("[)(]"));
console.log(solution("}}}"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
