## 올바른 괄호

[연습문제 > 올바른 괄호](https://programmers.co.kr/learn/courses/30/lessons/12909)

``` js
// 1
function solution(s) {
    let answer = 0;
    const sLength = s.length;

    for (let i = 0; i < sLength; i++) {
        answer += s[i] === '(' ? 1 : -1;
        if (answer < 0) return false;
    }

    return answer === 0 ? true : false;
}

// 2 - Refactoring (1이 더 빠름)
// function solution(s) {
//     let answer = 0;
//     const sLength = s.length;

//     for (let i = 0; i < sLength; i++) {
//         answer += s[i] === '(' ? 1 : -1;
//         if (answer < 0 || answer > sLength - i - 1) return false;
//     }

//     return answer === 0 ? true : false;
// }

// console.log(solution('()()'));
// console.log(solution('(())()'));
// console.log(solution(')()('));
// console.log(solution('(()('));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)