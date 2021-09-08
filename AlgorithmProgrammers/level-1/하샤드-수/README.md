## 하샤드 수

[연습문제 > 하샤드 수](https://programmers.co.kr/learn/courses/30/lessons/12947)

``` js
function solution(x) {
    return !(x % (x + '').split('').reduce((r, i) => +r + +i));
}

console.log(solution(10));
console.log(solution(12));
console.log(solution(11));
console.log(solution(13));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)