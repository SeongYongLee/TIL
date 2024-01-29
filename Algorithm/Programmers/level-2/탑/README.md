## 탑

사라진문제 > 스택/큐 > 탑

``` js
// 1
// function solution(heights) {
//     const answer = [];

//     while (heights.length) {
//         let temp = heights.pop();
//         let index = 0;
//         for (let x = heights.length - 1; x >= 0; x--) {
//             if (temp < heights[x]) {
//                 index = x + 1;
//                 break;
//             }
//         }
//         answer.unshift(index);
//     }

//     return answer;
// }

// 2 - Refactoring
function solution(heights) {
    return heights.map((v, i) => {
        while (i--) {
            if (heights[i] > v) return i + 1;
        }

        return 0;
    });
}

console.log(solution([6, 9, 5, 7, 4]));
console.log(solution([3, 9, 9, 3, 5, 7, 2]));
console.log(solution([1, 5, 3, 6, 7, 6, 5]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)