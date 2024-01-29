## 교점에 별 만들기

[위클리 챌린지 > 10주차 > 교점에 별 만들기](https://programmers.co.kr/learn/courses/30/lessons/87377)

``` js
function solution(line) {
    const arrayX = [];
    const arrayY = [];

    for (let i = 0; i < line.length; i++) {
        for (let j = i + 1; j < line.length; j++) {
            const denominator = line[j][0] * line[i][1] - line[j][1] * line[i][0];
            const x = (line[j][1] * line[i][2] - line[j][2] * line[i][1]) / denominator;
            const y = (line[j][2] * line[i][0] - line[j][0] * line[i][2]) / denominator;

            if (Number.isInteger(x) && Number.isInteger(y)) {
                arrayX.push(x);
                arrayY.push(y);
            }
        }
    }

    const yMin = Math.min(...arrayY);
    const xMin = Math.min(...arrayX);
    const yLength = Math.max(...arrayY) - yMin + 1;
    const xLength = Math.max(...arrayX) - xMin + 1;

    const answer = Array(yLength)
        .fill()
        .map((_) => Array(xLength).fill('.'));

    for (let i = 0; i < arrayX.length; i++) {
        answer[yLength - 1 - (arrayY[i] - yMin)][arrayX[i] - xMin] = '*';
    }

    return answer.map((a) => a.join(''));
}

console.log(
    solution([
        [2, -1, 4],
        [-2, -1, 4],
        [0, -1, 1],
        [5, -8, -12],
        [5, 8, 12],
    ]),
);
console.log(
    solution([
        [0, 1, -1],
        [1, 0, -1],
        [1, 0, 1],
    ]),
);
console.log(
    solution([
        [1, -1, 0],
        [2, -1, 0],
    ]),
);
console.log(
    solution([
        [1, -1, 0],
        [2, -1, 0],
        [4, -1, 0],
    ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)