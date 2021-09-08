## 실패율

[2019 KAKAO BLIND RECRUITMENT > 실패율](https://programmers.co.kr/learn/courses/30/lessons/42889)

``` js
function solution(N, stages) {
    const answer = [];
    let survivor = stages.length;

    for (let x = 1; x <= N; x++) {
        if (survivor === 0) {
            answer.push([x, 0]);
        } else {
            stages = stages.filter((s) => s !== x);
            const clearCount = stages.length;
            answer.push([x, (survivor - clearCount) / survivor]);
            survivor = clearCount;
        }
    }

    return answer.sort((x, y) => (y[1] === x[1] ? x[0] - y[0] : y[1] - x[1])).map((x) => x[0]);
}

console.log(solution(5, [2, 1, 2, 6, 2, 4, 3, 3]));
console.log(solution(4, [4, 4, 4, 4, 4]));
console.log(solution(8, [1, 2, 3, 4, 5, 6, 7]));
console.log(solution(1, [1, 2]));
console.log(solution(4, [2, 2, 2, 2, 2]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)