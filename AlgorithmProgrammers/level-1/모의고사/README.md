## 모의고사

[완전탐색 > 모의고사](https://programmers.co.kr/learn/courses/30/lessons/42840)

``` js
// 1
// function solution(answers) {
//     const supos = [
//         [1, 2, 3, 4, 5],
//         [2, 1, 2, 3, 2, 4, 2, 5],
//         [3, 3, 1, 1, 2, 2, 4, 4, 5, 5],
//     ];

//     const result = supos.reduce((result, supo) => {
//         result.push(answers.filter((answer, j) => supo[j % supo.length] === answer).length);
//         return result;
//     }, []);

//     const max = Math.max.apply(null, result);

//     const answer = result.reduce((result, current, i) => {
//         if (current === max) result.push(i + 1);
//         return result;
//     }, []);

//     return answer;
// }

// 2 - Refactoring
function solution(answers) {
    const supos = [
        [1, 2, 3, 4, 5],
        [2, 1, 2, 3, 2, 4, 2, 5],
        [3, 3, 1, 1, 2, 2, 4, 4, 5, 5],
    ];
    const suposLength = supos.map((s) => s.length);

    const result = supos.reduce(
        (result, supo, i) => [
            ...result,
            answers.filter((answer, j) => supo[j % suposLength[i]] === answer).length,
        ],
        [],
    );

    const max = Math.max.apply(null, result);

    return result.reduce((result, c, i) => (c === max ? [...result, i + 1] : result), []);
}

console.log(solution([1, 2, 3, 4, 5]));
console.log(solution([1, 3, 2, 4, 2]));
console.log(solution([1, 2, 3, 4, 5, 1, 2, 3, 4, 5]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)