## 자연수 뒤집어 배열로 만들기

[연습문제 > 자연수 뒤집어 배열로 만들기](https://programmers.co.kr/learn/courses/30/lessons/12932)

``` js
// 1
function solution(n) {
    return (n + '')
        .split('')
        .reverse()
        .map((x) => +x);
}

// 2 - Refactoring (더 느려짐)
// function solution(n) {
//     return (n + '').split('').reduce((r, c) => [+c, ...r], []);
// }

console.log(solution(12345));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)