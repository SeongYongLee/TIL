# AlgorithmProgrammers - Level 2

* [스택/큐 > 기능개발](#기능개발)

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)

## 기능개발

[스택/큐 > 기능개발](https://programmers.co.kr/learn/courses/30/lessons/42586)

``` js
function solution(progresses, speeds) {
    const answer = [];
    
    while (speeds.length) {
        let count = 0;
        progresses = progresses.map((x, i) => x + speeds[i]);
        while (speeds.length) {
            if (progresses[0] >= 100) {
                progresses.shift();
                speeds.shift();
                count++;
            } else break;
        }
        if (count) answer.push(count);
    }
    
    return answer;
}

console.log(solution([93, 30, 55], [1, 30, 5]));
console.log(solution([95, 90, 99, 99, 80, 99], [1, 1, 1, 1, 1, 1]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)/[위로](#algorithmprogrammers---level-2)