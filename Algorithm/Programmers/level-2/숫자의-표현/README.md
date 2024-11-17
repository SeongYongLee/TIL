## 숫자의 표현

[연습문제 > 숫자의 표현](https://programmers.co.kr/learn/courses/30/lessons/12924)

```js
// 1
// function solution(n) {
//     let answer = 1;

//     for (let i = 1; i < n / 2; i++) {
//         let temp = i;
//         let num = i;
//         while (temp < n) temp += ++num;
//         if (temp === n) answer++;
//     }

//     return answer;
// }

// 2 - Refactoring
/* 
    프로그래머스 - 다른 사람의 풀이 참고
    홀수인 약수의 개수를 찾으면 된다.
*/
function solution(n) {
  let answer = n % 2 ? 1 : 0;

  for (let i = 1; i < n / 2; i++) {
    if (!(n % i) && i % 2) answer++;
  }

  return answer;
}

console.log(solution(15));
console.log(solution(16));
console.log(solution(17));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
