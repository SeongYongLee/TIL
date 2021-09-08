## 완주하지 못한 선수

[해시 > 완주하지 못한 선수](https://programmers.co.kr/learn/courses/30/lessons/42576)

``` js
// 1
// function solution(participant, completion) {
//     participant.sort();
//     completion.sort();

//     const pLength = participant.length;

//     for (let i = 0; i < pLength; i++) {
//         if (participant[i] !== completion[i]) return participant[i];
//     }
// }

// 2 - 해시 (Key-value pair)
/* 
    프로그래머스 - 다른 사람의 풀이 참고
    var solution=(_,$)=>_.find(_=>!$[_]--,$.map(_=>$[_]=($[_]|0)+1))
*/
function solution(participant, completion) {
    completion.map((name) => (completion[name] = (completion[name] | 0) + 1));

    return participant.find((name) => !completion[name]--);
}

console.log(solution(['leo', 'kiki', 'eden'], ['eden', 'kiki']));
console.log(
    solution(
        ['marina', 'josipa', 'nikola', 'vinko', 'filipa'],
        ['josipa', 'filipa', 'marina', 'nikola'],
    ),
);
console.log(solution(['mislav', 'stanko', 'mislav', 'ana'], ['stanko', 'ana', 'mislav']));
console.log(
    solution(
        ['mislav', 'stanko', 'mislav', 'ana', 'mislav', 'stanko'],
        ['mislav', 'stanko', 'mislav', 'ana', 'mislav'],
    ),
);
console.log(
    solution(
        ['mislav', 'stanko', 'mislav', 'ana', 'mislav'],
        ['stanko', 'ana', 'mislav', 'mislav'],
    ),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)