## 최대공약수와 최소공배수

[연습문제 > 최대공약수와 최소공배수](https://programmers.co.kr/learn/courses/30/lessons/12940)

```js
// 1
// function solution(n, m) {
//     let max = 1;

//     for (let x = m > n ? n : m; x > 1; x--) {
//         if (Number.isInteger(n / x) && Number.isInteger(m / x)) {
//             max = x;
//             break;
//         }
//     }

//     return [max, (m * n) / max];
// }

// 2 - 유클리드 호제법
function solution(n, m) {
  const greatestCommonDivisor = (a, b) => {
    return b ? greatestCommonDivisor(b, a % b) : Math.abs(a);
  };

  const greatestCommon = greatestCommonDivisor(n, m);
  return [greatestCommon, (n * m) / greatestCommon];
}

console.log(solution(3, 12));
console.log(solution(2, 5));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
