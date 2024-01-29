## 행렬의 곱셈

[연습문제 > 행렬의 곱셈](https://programmers.co.kr/learn/courses/30/lessons/12949)

``` js
// 1
// function solution(arr1, arr2) {
//     const sizeX = arr2[0].length;
//     const count = arr2.length;

//     return arr1.reduce((r, c) => {
//         const tempArray = [];
//         for (let j = 0; j < sizeX; j++) {
//             let temp = 0;
//             for (let k = 0; k < count; k++) {
//                 temp += c[k] * arr2[k][j];
//             }
//             tempArray.push(temp);
//         }
//         return [...r, tempArray];
//     }, []);
// }

// 2 - Refactoring
function solution(arr1, arr2) {
    return arr1.map((a) => arr2[0].map((_, i) => arr2.reduce((r, c, j) => (r += a[j] * c[i]), 0)));
}

console.log(
    solution(
        [
            [1, 4],
            [3, 2],
            [4, 1],
        ],
        [
            [3, 3],
            [3, 3],
        ],
    ),
);
console.log(
    solution(
        [
            [-2, 2],
            [1, 2],
            [1, 2],
            [1, 2],
            [1, 2],
        ],
        [
            [1, 1, 1, 1, 1, 1],
            [1, 1, 1, 1, 1, 1],
        ],
    ),
);
console.log(
    solution(
        [
            [1, 4, 3],
            [3, 2, 3],
            [3, 2, 3],
        ],
        [
            [3, 3],
            [3, 3],
            [3, 3],
        ],
    ),
);
console.log(
    solution(
        [
            [2, 3, 2],
            [4, 2, 4],
            [3, 1, 4],
        ],
        [
            [5, 4, 3],
            [2, 4, 1],
            [3, 1, 1],
        ],
    ),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)