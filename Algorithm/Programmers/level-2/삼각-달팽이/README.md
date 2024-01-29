## 삼각 달팽이

[월간 코드 챌린지 시즌1 > 삼각 달팽이](https://programmers.co.kr/learn/courses/30/lessons/68645)

``` js
// 1
// function solution(n) {
//     let step = 0; // 0: down, 1: right, 2: up
//     let num = 1;
//     let location = 0;
//     const answerLeft = Array(n)
//         .fill()
//         .map((_) => Array());
//     const answerRight = Array(n)
//         .fill()
//         .map((_) => Array());

//     for (let i = n; i > 0; i--) {
//         switch (step) {
//             case 0:
//                 for (let j = 0; j < i; j++) {
//                     answerLeft[location].push(num);
//                     location++;
//                     num++;
//                 }
//                 location--;
//                 break;
//             case 1:
//                 for (let j = 0; j < i; j++) {
//                     answerLeft[location].push(num);
//                     num++;
//                 }
//                 break;
//             case 2:
//                 for (let j = 0; j < i; j++) {
//                     location--;
//                     answerRight[location].unshift(num);
//                     num++;
//                 }
//                 location++;
//                 break;
//         }
//         step = (step + 1) % 3;
//     }

//     return answerLeft.reduce((r, c, i) => [...r, ...answerLeft[i], ...answerRight[i]], []);
// }

// 2 - Refactoring
// function solution(n) {
//     let num = 1;
//     let location = 0;
//     const answerLeft = Array(n)
//         .fill()
//         .map((_) => Array());
//     const answerRight = Array(n)
//         .fill()
//         .map((_) => Array());

//     for (let i = n; i > 0; i -= 3) {
//         for (let j = 0; j < i; j++) answerLeft[location++].push(num++);
//         location--;
//         for (let j = 0; j < i - 1; j++) answerLeft[location].push(num++);
//         for (let j = 0; j < i - 2; j++) answerRight[location--].unshift(num++);
//         location++;
//     }

//     return answerLeft.reduce((r, c, i) => [...r, ...c, ...answerRight[i]], []);
// }

// 3 - Refactoring
/* 
    프로그래머스 - 다른 사람의 풀이 참고
*/
function solution(n) {
    let num = 0;
    let y = -1;
    let x = 0;
    const answer = Array(n)
        .fill()
        .map((_, i) => Array(i + 1).fill());

    for (let i = n; i > 0; i -= 3) {
        for (let j = 0; j < i; j++) answer[++y][x] = ++num;
        for (let j = 0; j < i - 1; j++) answer[y][++x] = ++num;
        for (let j = 0; j < i - 2; j++) answer[--y][--x] = ++num;
    }

    return answer.flat();
}

console.log(solution(4));
console.log(solution(5));
console.log(solution(6));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)