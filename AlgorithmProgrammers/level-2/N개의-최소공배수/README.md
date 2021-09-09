## N개의 최소공배수

[연습문제 > N개의 최소공배수](https://programmers.co.kr/learn/courses/30/lessons/12953)

``` js
const gcd = (a, b) => {
    return b ? gcd(b, a % b) : Math.abs(a);
};

function solution(words) {
    return words.reduce((r, c) => (r * c) / gcd(r, c));
}

console.log(solution([2, 6, 8, 14]));
console.log(solution([1, 2, 3]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)