## 로또의 최고 순위와 최저 순위

[2021 Dev-Matching: 웹 백엔드 개발자(상반기) > 로또의 최고 순위와 최저 순위](https://programmers.co.kr/learn/courses/30/lessons/77484)

```js
// 1
// function solution(lottos, win_nums) {
//     let minimumRank = 7;
//     let highestRank = 0;

//     for (let i = 0; i < lottos.length; i++) {
//         if (lottos[i] === 0) {
//             highestRank++;
//             continue;
//         }

//         if (win_nums.includes(lottos[i])) minimumRank--;
//     }

//     highestRank = minimumRank - highestRank;

//     return [highestRank === 7 ? 6 : highestRank, minimumRank === 7 ? 6 : minimumRank];
// }

// 2 - Refactoring
function solution(lottos, win_nums) {
  const rank = [6, 6, 5, 4, 3, 2, 1];
  let minimumCount = 0;
  let unknowCount = 0;

  for (let i = 0; i < lottos.length; i++) {
    if (lottos[i] === 0) {
      unknowCount++;
    } else if (win_nums.includes(lottos[i])) {
      minimumCount++;
    }
  }

  return [rank[minimumCount + unknowCount], rank[minimumCount]];
}

console.log(solution([44, 1, 0, 0, 31, 25], [31, 10, 45, 1, 6, 19]));
console.log(solution([0, 0, 0, 0, 0, 0], [38, 19, 20, 40, 15, 25]));
console.log(solution([45, 4, 35, 20, 3, 9], [20, 9, 3, 45, 4, 35]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
