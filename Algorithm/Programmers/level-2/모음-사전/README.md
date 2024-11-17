## 모음 사전

[위클리 챌린지 > 5주차 > 모음 사전](https://programmers.co.kr/learn/courses/30/lessons/84512)

```js
function solution(words) {
  return words
    .split("")
    .reduce(
      (r, c, i) =>
        r + [781, 156, 31, 6, 1][i] * ["A", "E", "I", "O", "U"].indexOf(c) + 1,
      0,
    );
}

console.log(solution("AAAAE"));
console.log(solution("AAAE"));
console.log(solution("I"));
console.log(solution("EIO"));

// A - 1
// AA - 2
// AAA - 3
// AAAA - 4 AAAAA E I O U
// AAAE - 10 (1 + 1 + 1 + (1 * 1) + (1 * 5)) + 1
// AAAI - 16
// AAAO - 22
// AAAU - 28 (1 + 1 + 1 + (4 * 1) + (4 * 5)) + 1
// AAE - 34 (1 + 1 + (1 * 1) + (5 * 1) + (5 * 5)) + 1
// AAEA - 35
// AAI - 65
// AAO - 96
// AAU - 127 (1 + 1 + (4 * 1) + (4 * 30)) + 1
// 1 =>
// 6 (1 * 5 + 1) =>
// 31 (6 * 5 + 1) =>
// 156 (31 * 5 + 1) =>
// 781 (156 * 5 + 1)
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
