## 프린터

[스택/큐 > 프린터](https://programmers.co.kr/learn/courses/30/lessons/42587)

``` js
function solution(priorities, location) {
    let p = priorities.map((a, b) => [a, b]);
    let answer = 1;

    do {
        const temp = [p.shift()];

        while (p.length) {
            if (p[0][0] > temp[0][0]) p.push(...temp.splice(0, temp.length));
            temp.push(p.shift());
        }

        if (location === temp.shift()[1]) return answer;
        else p = temp.slice();
    } while (answer++);
}

console.log(solution([2, 1, 3, 2], 2));
console.log(solution([1, 1, 9, 1, 1, 1], 0));
console.log(solution([1], 0));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)