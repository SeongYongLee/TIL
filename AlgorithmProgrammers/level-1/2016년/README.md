## 2016년

[연습문제 > 2016년](https://programmers.co.kr/learn/courses/30/lessons/12901)

``` js
// 1
// function solution(a, b) {
//     const week = ['THU', 'FRI', 'SAT', 'SUN', 'MON', 'TUE', 'WED'];
//     const year = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
//     let temp = 0;

//     for (let x = 0; x < a - 1; x++) temp += year[x];
//     return week[(temp + b) % 7];
// }

// 2 - new Date
function solution(a, b) {
    return ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'][
        new Date('2016-' + a + '-' + b).getDay()
    ];
}

console.log(solution(5, 24));
console.log(solution(12, 31));
console.log(solution(1, 1));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)