## 최솟값 만들기

[연습문제 > 최솟값 만들기](https://programmers.co.kr/learn/courses/30/lessons/12941)

``` js
function solution(A, B){
    A.sort((a, b) => a - b);
    B.sort((a, b) => b - a);

    return A.reduce((r, c, i) => r + c * B[i], 0);
}

console.log(solution([1, 4, 2], [5, 4, 4]));
console.log(solution([1, 2], [3, 4]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)