## 점프와 순간 이동

[Summer/Winter Coding(~2018) > 점프와 순간 이동](https://programmers.co.kr/learn/courses/30/lessons/12980)

``` js
// 1
// function solution(n) {
//     let ans = 0;

//     while (n) {
//         if (n % 2 === 0) {
//             n /= 2;
//         } else {
//             n--;
//             ans++;
//         }
//     }

//     return ans;
// }

// 2 - Refactoring
function solution(n) {
    return n
        .toString(2)
        .split('')
        .filter((n) => +n).length;
}

console.log(solution(5));
console.log(solution(6));
console.log(solution(5000));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)