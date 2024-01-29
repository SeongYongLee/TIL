## 문자열 내 p와 y의 개수

[연습문제 > 문자열 내 p와 y의 개수](https://programmers.co.kr/learn/courses/30/lessons/12916)

``` js
// 1
// function solution(s) {
//     let answer = 0;

//     for (let i = 0; i < s.length; i++) {
//         if (s[i].toLowerCase() === 'p') answer++;
//         else if (s[i].toLowerCase() === 'y') answer--;
//     }

//     return answer === 0;
// }

// 2 - Refactoring 
function solution(s) {
    return (
        s.toUpperCase().split('P').length === s.toUpperCase().split('Y').length
    );
}

console.log(solution("pPoooyY"));
console.log(solution("Pyy"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)