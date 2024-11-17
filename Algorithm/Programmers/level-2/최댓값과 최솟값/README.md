## 최댓값과 최솟값

[연습문제 > 최댓값과 최솟값](https://programmers.co.kr/learn/courses/30/lessons/12939)

```js
// 1
// function solution(s) {
//     const sSplit = s.split(' ');
//     let min = +sSplit[0];
//     let max = min;

//     for (let i = 1; i < sSplit.length; i++) {
//         const num = +sSplit[i];
//         if (num > max) max = num;
//         if (num < min) min = num;
//     }

//     return `${min} ${max}`;
// }
// 2 - Refactoring
function solution(s) {
  const arr = s.split(" ");

  return `${Math.min(...arr)} ${Math.max(...arr)}`;
}

console.log(solution("1 2 3 4"));
console.log(solution("-1 -2 -3 -4"));
console.log(solution("-1 -1"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
