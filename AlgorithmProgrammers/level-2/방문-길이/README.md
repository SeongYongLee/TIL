## 방문 길이

[Summer/Winter Coding(~2018) > 방문 길이](https://programmers.co.kr/learn/courses/30/lessons/49994)

``` js
function solution(dirs) {
    const answer = new Set();
    let x = 0;
    let y = 0;

    for (let i = 0; i < dirs.length; i++) {
        const first = '' + x + y;

        switch (dirs[i]) {
            case 'U':
                if (y === 5) continue;
                y++;
                break;
            case 'D':
                if (y === -5) continue;
                y--;
                break;
            case 'R':
                if (x === 5) continue;
                x++;
                break;
            case 'L':
                if (x === -5) continue;
                x--;
                break;
        }

        const second = '' + x + y;

        answer.add(first + second);
        answer.add(second + first);
    }

    return answer.size / 2;
}

console.log(solution('ULURRDLLU'));
console.log(solution('LULLLLLLU'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)