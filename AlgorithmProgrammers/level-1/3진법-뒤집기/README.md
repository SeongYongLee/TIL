## 3진법 뒤집기

[월간 코드 챌린지 시즌1 > 3진법 뒤집기](https://programmers.co.kr/learn/courses/30/lessons/68935)

``` js
function solution(a, b) {
    return a.reduce((r, _, i) => r + a[i] * b[i], 0);
}

console.log(solution(45));
console.log(solution(125));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)