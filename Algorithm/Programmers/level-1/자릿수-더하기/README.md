## 자릿수 더하기

[연습문제 > 자릿수 더하기](https://programmers.co.kr/learn/courses/30/lessons/12931)

``` js
function solution(n) {
    return (n + '').split('').reduce((r, i) => r + +i, 0);
}

console.log(solution(123));
console.log(solution(987));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)