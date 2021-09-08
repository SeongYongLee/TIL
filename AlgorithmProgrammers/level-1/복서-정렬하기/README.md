## 복서 정렬하기

[위클리 챌린지 > 6주차 > 복서 정렬하기](https://programmers.co.kr/learn/courses/30/lessons/85002)

``` js
const pad = (n, width = 3) =>
    n.length >= width ? n : new Array(width - n.length + 1).join('0') + n;

function solution(weights, head2head) {
    return head2head
        .reduce((answer, records, i) => {
            let fightCount = 0;
            let winCount = 0;
            let weightCount = 0;

            for (let j = 0; j < records.length; j++) {
                if (i === j || records[j] === 'N') continue;
                fightCount++;
                if (records[j] === 'W') {
                    winCount++;
                    if (weights[i] < weights[j]) weightCount++;
                }
            }

            return [
                ...answer,
                [
                    i + 1,
                    fightCount ? winCount / fightCount : 0,
                    `${pad(weightCount + '')}${pad(weights[i] + '')}`,
                ],
            ];
        }, [])
        .sort((a, b) => (b[1] === a[1] ? b[2] - a[2] : b[1] - a[1]))
        .map((a) => a[0]);
}

console.log(solution([50, 82, 75, 120], ['NLWL', 'WNLL', 'LWNW', 'WWLN']));
console.log(solution([145, 92, 86], ['NLW', 'WNL', 'LWN']));
console.log(solution([60, 70, 60], ['NNN', 'NNN', 'NNN']));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)