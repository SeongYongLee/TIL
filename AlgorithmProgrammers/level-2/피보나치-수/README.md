## 피보나치 수

[연습문제 > 피보나치 수](https://programmers.co.kr/learn/courses/30/lessons/12945)

``` js
function solution(n) {
    let history = 0;
    let answer = 1;

    for (let i = 1; i < n; i++) {
        const temp = (history + answer) % 1234567;
        history = answer;
        answer = temp;
    }

    return answer;
}

console.log(solution(3));
console.log(solution(5));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)