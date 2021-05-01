# AlgorithmProgrammers - Level 2

* [스택/큐 > 기능개발](#기능개발)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)

## 기능개발

[스택/큐 > 기능개발](https://programmers.co.kr/learn/courses/30/lessons/42586)

``` js
// 1
// function solution(progresses, speeds) {
//     const answer = [];
    
//     while (speeds.length) {
//         let count = 0;
//         progresses = progresses.map((x, i) => x + speeds[i]);
//         while (speeds.length) {
//             if (progresses[0] >= 100) {
//                 progresses.shift();
//                 speeds.shift();
//                 count++;
//             } else break;
//         }
//         if (count) answer.push(count);
//     }
    
//     return answer;
// }

// 2 - Refactoring
function solution(board, moves) {
    let answer = 0;
    const result = [];

    let fitstFilter = board.reduce((result, x, i) => x.map((i, y) => [...(result[y] || []), i]), []);
    let secondFilter = fitstFilter.map((x, i) => x.filter((x) => x !== 0).reverse());

    for (let x = 0; x < moves.length; x++) {
        const temp = secondFilter[moves[x] - 1].pop();
        if (!temp) continue;
        if (temp === result[result.length - 1]) {
            result.pop();
            answer += 2;
            continue;
        }
        result.push(temp);
    }
    return answer;
}

console.log(solution([93, 30, 55], [1, 30, 5]));
console.log(solution([95, 90, 99, 99, 80, 99], [1, 1, 1, 1, 1, 1]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)