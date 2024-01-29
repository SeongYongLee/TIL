## 멀쩡한 사각형

[Summer/Winter Coding(2019) > 멀쩡한 사각형](https://programmers.co.kr/learn/courses/30/lessons/62048)

``` js
// 1
// const gcd = (a, b) => {
//     return b ? gcd(b, a % b) : Math.abs(a);
// };

// function solution(w, h) {
//     const temp = gcd(w, h);

//     return w * h - (w / temp + h / temp - 1) * temp;
// }

// 2 - Refactoring
const gcd = (a, b) => {
    return b ? gcd(b, a % b) : Math.abs(a);
};

function solution(w, h) {
    return w * h - (w + h - gcd(w, h));
}

console.log(solution(8, 12));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)