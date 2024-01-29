## 멀리 뛰기

[연습문제 > 멀리 뛰기](https://programmers.co.kr/learn/courses/30/lessons/12914)

``` js
function solution(n) {
    let historyAnswer = 0;
    let answer = 1;

    for (let i = 1; i <= n; i++) {
        const tempAnswer = (historyAnswer + answer) % 1234567;
        historyAnswer = answer;
        answer = tempAnswer;
    }

    return answer;
}

console.log(solution(4));
console.log(solution(3));

// 1 = 1
// 2 (1+1) = 2
// 3 (1+2) = 3
// 4 (1+3+1) = 5
// 5 (1+4+3) = 8
// 6
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)