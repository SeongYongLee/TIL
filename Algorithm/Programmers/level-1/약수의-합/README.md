## 약수의 합

[연습문제 > 약수의 합](https://programmers.co.kr/learn/courses/30/lessons/12928)

```js
function solution(n) {
  let answer = 0;
  let last = n;

  for (let x = 0; x < last; x++) {
    const temp = n / x;

    if (Number.isInteger(temp)) {
      answer += temp === x ? temp : temp + x;
    }

    last = temp;
  }

  return answer;
}

console.log(solution(12));
console.log(solution(5));
console.log(solution(600));
console.log(solution(1));
console.log(solution(0));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
