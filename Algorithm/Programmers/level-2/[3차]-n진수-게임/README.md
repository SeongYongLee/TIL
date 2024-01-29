## [3차] n진수 게임

[2018 KAKAO BLIND RECRUITMENT > [3차] n진수 게임](https://programmers.co.kr/learn/courses/30/lessons/17687)

``` js
function solution(n, t, m, p) {
    let str = '';
    const length = (t - 1) * m + p;

    for (let i = 0; str.length < length; i++) {
        str += i.toString(n);
    }

    return str
        .split('')
        .filter((_, i) => i % m === p - 1)
        .splice(0, t)
        .join('')
        .toUpperCase();
}

console.log(solution(2, 4, 2, 1));
console.log(solution(16, 16, 2, 1));
console.log(solution(16, 16, 2, 2));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)