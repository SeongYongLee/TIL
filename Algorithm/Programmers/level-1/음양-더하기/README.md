## 음양 더하기

[월간 코드 챌린지 시즌2 > 음양 더하기](https://programmers.co.kr/learn/courses/30/lessons/76501)

```js
function solution(absolutes, signs) {
  return absolutes.reduce((r, c, i) => r + (signs[i] ? +c : -c), 0);
}

console.log(solution([4, 7, 12], [true, false, true]));
console.log(solution([1, 2, 3], [false, false, true]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
