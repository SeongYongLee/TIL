## 영어 끝말잇기

[Summer/Winter Coding(2019) > 영어 끝말잇기](https://programmers.co.kr/learn/courses/30/lessons/12981)

``` js
function solution(n, words) {
    const wordsLength = words.length;
    const history = [words[0]];

    for (let i = 1; i < wordsLength; i++) {
        if (words[i - 1].slice(-1) === words[i].slice(0, 1) && history.indexOf(words[i]) === -1) {
            history.push(words[i]);
        } else {
            return [(i % n) + 1, Math.floor(i / n) + 1];
        }
    }

    return [0, 0];
}

console.log(
    solution(3, ['tank', 'kick', 'know', 'wheel', 'land', 'dream', 'mother', 'robot', 'tank']),
);
console.log(
    solution(5, [
        'hello',
        'observe',
        'effect',
        'take',
        'either',
        'recognize',
        'encourage',
        'ensure',
        'establish',
        'hang',
        'gather',
        'refer',
        'reference',
        'estimate',
        'executive',
    ]),
);
console.log(solution(2, ['hello', 'one', 'even', 'never', 'now', 'world', 'draw']));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)