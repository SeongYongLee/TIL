## 나누어 떨어지는 숫자 배열

[연습문제 > 나누어 떨어지는 숫자 배열](https://programmers.co.kr/learn/courses/30/lessons/12910)

```js
function solution(arr, divisor) {
  const answer = arr.filter((x) => x % divisor === 0).sort((a, b) => a - b);

  return answer.length ? answer : [-1];
}

console.log(solution([5, 9, 7, 10], 5));
console.log(solution([2, 36, 1, 3], 1));
console.log(solution([3, 2, 6], 10));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
