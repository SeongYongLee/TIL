## 단속카메라

[탐욕법 > 단속카메라](https://programmers.co.kr/learn/courses/30/lessons/42884)

``` js
function solution(words) {
    words.sort((a, b) => (a[0] === b[0] ? a[1] - b[1] : a[0] - b[0]));

    let answer = 1;
    let index = words[0][1];

    for (let i = 1; i < words.length; i++) {
        if (index >= words[i][0]) {
            if (index > words[i][1]) index = words[i][1];
        } else {
            answer++;
            index = words[i][1];
        }
    }
    return answer;
}

console.log(
    solution([
        [-20, 15],
        [-14, -5],
        [-18, -14],
        [-18, -13],
        [-18, -16],
        [-5, -3],
    ])
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)