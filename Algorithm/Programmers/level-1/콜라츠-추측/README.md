## 콜라츠 추측

[연습문제 > 콜라츠 추측](https://programmers.co.kr/learn/courses/30/lessons/12943)

```js
function solution(num) {
  for (let answer = 0; answer < 500; answer++) {
    if (num === 1) return answer;
    num = num % 2 === 0 ? num / 2 : num * 3 + 1;
  }
  return -1;
}

console.log(solution(6));
console.log(solution(16));
console.log(solution(626331));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
