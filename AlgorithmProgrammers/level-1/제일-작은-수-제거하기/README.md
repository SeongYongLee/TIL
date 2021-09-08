## 제일 작은 수 제거하기

[연습문제 > 제일 작은 수 제거하기](https://programmers.co.kr/learn/courses/30/lessons/12935)

``` js
// 1
// function solution(arr) {
//     arr.splice(arr.indexOf(Math.min(...arr)), 1);
//     return arr.length ? arr : [-1];
// }
// 2 - Refactoring
function solution(arr) {
    if (arr.length === 1) return [-1]; 
    
    arr.splice(arr.indexOf(Math.min(...arr)), 1);
    return arr;
}


console.log(solution([4, 3, 2, 1]));
console.log(solution([10]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)