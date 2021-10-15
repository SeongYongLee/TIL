## 전력망을 둘로 나누기

[위클리 챌린지 > 9주차 > 전력망을 둘로 나누기](https://programmers.co.kr/learn/courses/30/lessons/86971)

``` js
function solution(n, wires) {
    const answer = [[...wires[0], 1]];

    const findNextIndex = (index) => {
        const next = answer.findIndex((a) => a[1] === answer[index][0]);
        if (next !== -1) {
            answer[next][2]++;
            findNextIndex(next);
        }
    };

    for (let i = 1; i < wires.length; i++) {
        let dupNum = 0;
        let childNum = 0;
        for (let j = 0; j < answer.length; j++) {
            if ([answer[j][0], answer[j][1]].includes(wires[i][0])) {
                [dupNum, childNum] = wires[i];
                if (answer[j][1] === dupNum) answer[j][2]++;
                findNextIndex(j);
                break;
            }
            if ([answer[j][0], answer[j][1]].includes(wires[i][1])) {
                [childNum, dupNum] = wires[i];
                if (answer[j][1] === dupNum) answer[j][2]++;
                findNextIndex(j);
                break;
            }
        }

        dupNum ? answer.push([dupNum, childNum, 1]) : wires.push(wires[i]);
    }

    return (
        answer.reduce((r, c) => {
            const temp = Math.abs(c[2] - n / 2);

            return temp < r ? temp : r;
        }, Infinity) * 2
    );
}

console.log(solution(2, [[1, 2]]));
console.log(
    solution(9, [
        [1, 3],
        [4, 5],
        [2, 3],
        [3, 4],
        [4, 6],
        [4, 7],
        [7, 8],
        [7, 9],
    ]),
);
console.log(
    solution(4, [
        [1, 2],
        [2, 3],
        [3, 4],
    ]),
);
console.log(
    solution(7, [
        [1, 2],
        [2, 7],
        [3, 7],
        [3, 4],
        [4, 5],
        [6, 7],
    ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)