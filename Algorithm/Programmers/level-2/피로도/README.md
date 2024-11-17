## 피로도

[위클리 챌린지 > 12주차 > 피로도](https://programmers.co.kr/learn/courses/30/lessons/87946)

```js
// 1
// function solution(k, dungeons) {
//     return dungeons
//         .sort((a, b) => (a[0] === b[0] ? a[1] - b[1] : a[0] - b[0]))
//         .reduce(
//             (r, c) => (r[0] >= c[1] ? [r[0] - c[1], ++r[1]] : r),
//             [k, 0]
//         )[1];
// }

// 2
// function solution(k, dungeons) {
//     return dungeons
//         .sort((a, b) => (a[1] === b[1] ? a[0] - b[0] : a[1] - b[1]))
//         .reduce((r, c) => (c[0] >= r[0] + c[1] ? [r[0] + c[1], ++r[1]] : r), [0, 0])[1];
// }

// 3 - 여기까지 문제 잘못이해
// function solution(k, dungeons) {
//     return dungeons
//         .sort((a, b) => (a[0] === b[0] ? a[1] - b[1] : a[0] - b[0]))
//         .reduce(
//             (r, c) => {
//                 if (c[0] >= r[0] + c[1]) {
//                     return [r[0] + c[1], ++r[1], [...r[2], c[1]]];
//                 } else {
//                     r[2].sort((a, b) => a - b);
//                     if (r[2][r[2].length - 1] > c[1]) {
//                         r[0] = r[0] - r[2][r[2].length - 1] + c[1];
//                         r[2][r[2].length - 1] = c[1];
//                     }
//                     return r;
//                 }
//             },
//             [0, 0, []]
//         )[1];
// }

// 4 - 잘못된 풀이 접근
// function solution(k, dungeons) {
//     return dungeons
//         .sort((a, b) => (a[0] === b[0] ? a[1] - b[1] : b[0] - a[0]))
//         .reduce(
//             (r, c) => {
//                 console.log(r, c, ...r[1]);
//                 if (r[0] >= Math.max(...c)) {
//                     return [r[0] - c[1], [...r[1], c[1]]];
//                 } else {
//                     r[1].sort((a, b) => a - b);
//                     if (r[1][r[1].length - 1] > c[1]) {
//                         const temp = r[0] + r[1][r[1].length - 1];
//                         if (temp > c[0]) {
//                             r[0] = temp - c[1];
//                             r[1][r[1].length - 1] = c[1];
//                         }
//                     }
//                     return r;
//                 }
//             },
//             [k, []]
//         )[1].length;
// }

// 5
function solution(k, dungeons) {
  let answer = 0;
  const stack = [[k, dungeons, 0]];

  while (stack.length) {
    const next = stack.pop();

    if (next[1].length <= 1)
      answer =
        answer > next[2] + next[1].length ? answer : next[2] + next[1].length;
    else {
      for (let i = 0; i < next[1].length; i++) {
        const sliceDungeons = next[1].slice();
        const spliceDungeons = sliceDungeons.splice(i, 1)[0];

        stack.push([
          next[0] - spliceDungeons[1],
          sliceDungeons.filter((d) => next[0] - spliceDungeons[1] >= d[0]),
          next[2] + 1,
        ]);
      }
    }
  }

  return answer;
}

console.log(
  solution(80, [
    [80, 20],
    [50, 40],
    [30, 10],
  ]),
);

console.log(
  solution(80, [
    [80, 20],
    [50, 40],
    [40, 30],
    [45, 10],
    [45, 10],
    [45, 10],
    [45, 10],
    [45, 10],
    [45, 1],
    [45, 1],
    [45, 1],
    [45, 1],
    [45, 1],
    [10, 2],
    [10, 2],
    [10, 2],
    [10, 2],
    [10, 2],
  ]),
);

console.log(
  solution(50, [
    [50, 10],
    [30, 10],
    [30, 5],
    [30, 15],
    [50, 10],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
    [50, 1],
  ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
