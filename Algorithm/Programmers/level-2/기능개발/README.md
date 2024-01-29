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
// function solution(board, moves) {
//     let answer = 0;
//     const result = [];

//     let fitstFilter = board.reduce((result, x, i) => x.map((i, y) => [...(result[y] || []), i]), []);
//     let secondFilter = fitstFilter.map((x, i) => x.filter((x) => x !== 0).reverse());

//     for (let x = 0; x < moves.length; x++) {
//         const temp = secondFilter[moves[x] - 1].pop();
//         if (!temp) continue;
//         if (temp === result[result.length - 1]) {
//             result.pop();
//             answer += 2;
//             continue;
//         }
//         result.push(temp);
//     }
//     return answer;
// }

// 3 - Change Approach
/* 
    프로그래머스 - 다른 사람의 풀이 참고
*/
function solution(progresses, speeds) {
    const answer = [0];
    const days = progresses.map((p, i) => Math.ceil((100 - p) / speeds[i]));
    const dlength = days.length;
    let maxDay = days[0];

    for (let i = 0, j = 0; i < dlength; i++) {
        if (days[i] <= maxDay) {
            answer[j] += 1;
        } else {
            maxDay = days[i];
            answer[++j] = 1;
        }
    }

    return answer;
}

console.log(solution([93, 30, 55], [1, 30, 5]));
console.log(solution([95, 90, 99, 99, 80, 99], [1, 1, 1, 1, 1, 1]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)