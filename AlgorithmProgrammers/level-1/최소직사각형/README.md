## 최소직사각형

[위클리 챌린지 > 8주차 > 최소직사각형](https://programmers.co.kr/learn/courses/30/lessons/86491)

``` js
function solution(sizes) {
    return sizes
        .reduce(
            (r, c) =>
                c[0] > c[1]
                    ? [c[0] > r[0] ? c[0] : r[0], c[1] > r[1] ? c[1] : r[1]]
                    : [c[1] > r[0] ? c[1] : r[0], c[0] > r[1] ? c[0] : r[1]],
            [0, 0],
        )
        .reduce((r, c) => r * c);
}

console.log(
    solution([
        [60, 50],
        [30, 70],
        [60, 30],
        [80, 40],
    ]),
);
console.log(
    solution([
        [10, 7],
        [12, 3],
        [8, 15],
        [14, 7],
        [5, 15],
    ]),
);
console.log(
    solution([
        [14, 4],
        [19, 6],
        [6, 16],
        [18, 7],
        [7, 11],
    ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)