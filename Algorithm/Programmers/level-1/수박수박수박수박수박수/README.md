## 수박수박수박수박수박수?

[연습문제 > 수박수박수박수박수박수?](https://programmers.co.kr/learn/courses/30/lessons/12922)

```js
// 1
// function solution(n) {
//     let answer = '';

//     for (let x = 0; x < n; x++) {
//         answer += x % 2 === 0 ? '수' : '박';
//     }

//     return answer;
// }

// 2 - repeat 사용
function solution(n) {
  return "수박".repeat(n / 2) + (n % 2 ? "수" : "");
}

console.log(solution(1));
console.log(solution(3));
console.log(solution(4));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
