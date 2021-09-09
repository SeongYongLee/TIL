## 다음 큰 숫자

[연습문제 > 다음 큰 숫자](https://programmers.co.kr/learn/courses/30/lessons/12911)

``` js
function solution(n) {
  const count = (n) =>
    n
      .toString(2)
      .split('')
      .filter((x) => x === '1').length;

  const nLength = count(n);

  while (n++) if (nLength === count(n)) return n;
}

console.log(solution(78));
console.log(solution(15));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)