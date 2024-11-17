## 쇠막대기

사라진문제 > 스택/큐 > 쇠막대기

```js
// 1
// function solution(arrangement) {
//     let location = 0;

//     return arrangement.split('').reduce((result, a, i) => {
//         if (a === '(' && arrangement[i+1] === '(') location++;
//         else if (a === ')' && arrangement[i-1] === '(') result += location;
//         else if (a === ')' && arrangement[i-1] === ')') {
//             location--;
//             result++;
//         }
//         return result;
//     },0)
// }

// 2 - Refactoring
function solution(arrangement) {
  let answer = 0;
  let stack = 0;

  arrangement = arrangement.replace(/\(\)/g, 0);

  for (let i = 0; i < arrangement.length; i++) {
    switch (arrangement[i]) {
      case "(":
        stack++;
        break;
      case "0":
        answer += stack;
        break;
      case ")":
        stack--;
        answer++;
        break;
    }
  }

  return answer;
}

console.log(solution("()(((()())(())()))(())"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
