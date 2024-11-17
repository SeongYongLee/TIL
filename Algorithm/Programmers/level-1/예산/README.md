## 예산

[Summer/Winter Coding(~2018) > 예산](https://programmers.co.kr/learn/courses/30/lessons/12982)

```js
// 1
// function solution(d, budget) {
//     for (const [i, x] of d.sort((x, y) => x - y).entries()) {
//         budget -= x;
//         if (budget < 0) return i;
//         else if (budget === 0) return i + 1;
//     }
//     return d.length;
// }

// 2 - Refactoring
function solution(d, budget) {
  const dlength = d.length;
  d.sort((x, y) => x - y);

  for (let i = 0; i < dlength; i++) {
    budget -= d[i];
    if (budget < 0) return i;
    else if (budget === 0) return i + 1;
  }

  return d.length;
}
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
