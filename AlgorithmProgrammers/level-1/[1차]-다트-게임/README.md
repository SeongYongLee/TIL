## [1차] 다트 게임

[2018 KAKAO BLIND RECRUITMENT > [1차] 다트 게임](https://programmers.co.kr/learn/courses/30/lessons/17682)

``` js
function solution(dartResult) {
    var answer = [];

    let tempInteger = '';

    for (let x = 0; x < dartResult.length; x++) {
        if (Number.isInteger(+dartResult[x])) {
            tempInteger += dartResult[x];
        } else {
            switch (dartResult[x]) {
                case 'S':
                    answer.push(+tempInteger);
                    break;
                case 'D':
                    answer.push(Math.pow(+tempInteger, 2));
                    break;
                case 'T':
                    answer.push(Math.pow(+tempInteger, 3));
                    break;
                case '*':
                    answer[answer.length - 1] *= 2;
                    if (answer[answer.length - 2]) answer[answer.length - 2] *= 2;
                    break;
                case '#':
                    answer[answer.length - 1] *= -1;
                    break;
            }
            tempInteger = '';
        }
    }

    return answer.reduce((a, b) => a + b);
}

console.log(solution('1S2D*3T'));
console.log(solution('1D2S#10S'));
console.log(solution('1D2S0T'));
console.log(solution('1S*2T*3S'));
console.log(solution('1D#2S*3S'));
console.log(solution('1T2D3D#'));
console.log(solution('1D2S3T*'));
console.log(solution('10S2D*3T'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)