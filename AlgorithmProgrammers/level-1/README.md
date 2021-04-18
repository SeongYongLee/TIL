# AlgorithmProgrammers - Level 1

* [크레인 인형뽑기 게임](#크레인-인형뽑기-게임)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)

## 크레인 인형뽑기 게임

[2019 카카오 개발자 겨울 인턴십 > 크레인 인형뽑기 게임](https://programmers.co.kr/learn/courses/30/lessons/64061)


``` js
function solution(board, moves) {
    let answer = 0;
    const result = [];

    const filter = board.reduce(
        (result, x) => x.map((y, i) => y !== 0 ? [...(result[i] || []), y] : result[i] || []),
        [],
    );

    for (let x = 0; x < moves.length; x++) {
        const temp = filter[moves[x] - 1].shift();
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
console.log(
    solution(
        [
            [0, 0, 0, 0, 0],
            [0, 0, 1, 0, 3],
            [0, 2, 5, 0, 1],
            [4, 2, 4, 4, 2],
            [3, 5, 1, 3, 1],
        ],
        [1, 5, 3, 5, 1, 2, 1, 4],
    ),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-1)