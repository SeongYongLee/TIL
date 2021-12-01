## H-Index

[정렬 > H-Index](https://programmers.co.kr/learn/courses/30/lessons/42747)

``` js
// 1
// function solution(citations) {
//     for (let i = citations.length; i > 0; i--) {
//         const temp = citations.filter((s) => s >= i).length;
//         if (temp >= i && citations.length - temp <= i) return i;
//     }

//     return 0;
// }

// 2 - Refactoring
function solution(citations) {
    citations = citations.sort((a, b) => b - a);

    let i = -1;

    while (++i < citations[i]) {}

    return i;
}

console.log(solution([3, 0, 6, 1, 5]));
console.log(solution([10, 10, 10]));
console.log(solution([0, 0, 0]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)