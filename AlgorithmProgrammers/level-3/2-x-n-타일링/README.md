## 2 x n 타일링

[연습문제 > 2 x n 타일링](https://programmers.co.kr/learn/courses/30/lessons/12900)

``` js
function solution(n) {
    let historyAnswer = 0;
    let answer = 1;

    for (let i = 1; i <= n; i++) {
        const tempAnswer = (historyAnswer + answer) % 1000000007;
        historyAnswer = answer;
        answer = tempAnswer;
    }

    return answer;
}

console.log(solution(4));

// 1 = 1
// 2 (1+1) = 2
// 3 (1+2) = 3
// 4 (1+3+1)= 5
// 5 (1+3+4) = 8
// 6 (1+5+6+1) = 13
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)