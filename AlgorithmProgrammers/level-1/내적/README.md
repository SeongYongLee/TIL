## 내적

[월간 코드 챌린지 시즌1 > 내적](https://programmers.co.kr/learn/courses/30/lessons/70128)

``` js
function solution(a, b) {
    return a.reduce((r, _, i) => r + a[i] * b[i], 0);
}

console.log(solution([1, 2, 3, 4], [-3, -1, 0, 2]));
console.log(solution([-1, 0, 1], [1, 0, -1]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)