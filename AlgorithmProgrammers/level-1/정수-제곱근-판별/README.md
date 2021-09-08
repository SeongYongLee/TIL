## 정수 제곱근 판별

[연습문제 > 정수 제곱근 판별](https://programmers.co.kr/learn/courses/30/lessons/12934)

``` js
function solution(n) {
    const sqrtN = Math.sqrt(n);
    return Number.isInteger(sqrtN) ? Math.pow(sqrtN + 1, 2) : -1;
}

console.log(solution(121));
console.log(solution(3));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)