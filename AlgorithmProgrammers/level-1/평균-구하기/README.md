## 평균 구하기

[연습문제 > 평균 구하기](https://programmers.co.kr/learn/courses/30/lessons/12944)

``` js
function solution(arr) {
    return arr.reduce((r, c) => r + c) / arr.length;
}

console.log(solution([1, 2, 3, 4]));
console.log(solution([5, 5]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)