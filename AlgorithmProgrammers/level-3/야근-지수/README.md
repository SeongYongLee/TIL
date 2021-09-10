## 야근 지수

[연습문제 > 야근 지수](https://programmers.co.kr/learn/courses/30/lessons/12927)

``` js
function solution(n, works) {
    works.sort((a, b) => b - a);
    let index = 0;
    let historyNum = works[index++]--;
    n--;

    while (n) {
        const tempNum = works[index];
        if (tempNum !== historyNum) {
            index = 0;
            historyNum = tempNum;
            continue;
        }
        if (--works[index++] === -1) return 0;
        n--;
    }
    return works.reduce((r, c) => r + Math.pow(c, 2), 0);
}

console.log(solution(4, [4, 3, 3]));
console.log(solution(1, [2, 1, 2]));
console.log(solution(3, [1, 1]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)