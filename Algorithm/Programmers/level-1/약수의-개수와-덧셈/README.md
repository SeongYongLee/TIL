## 약수의 개수와 덧셈

[월간 코드 챌린지 시즌2 > 약수의 개수와 덧셈](https://programmers.co.kr/learn/courses/30/lessons/77884)

```js
// 1
// function solution(left, right) {
//     let answer = 0;

//     for (let x = left; x <= right; x++) {
//         let count = 0;
//         let last = x;

//         for (let y = 0; y < last; y++) {
//             const temp = x / y;

//             if (Number.isInteger(temp)) {
//                 count += temp === y ? 1 : 2;
//             }

//             last = temp;
//         }
//         answer += count % 2 ? -x : x;
//     }

//     return answer;
// }

// 2
/* 
    Refactoring 제곱근이 정수면 약수의 갯수가 홀수이다.
*/
function solution(left, right) {
  let answer = 0;

  for (let x = left; x <= right; x++) {
    answer += Number.isInteger(Math.sqrt(x)) ? -x : x;
  }

  return answer;
}

console.log(solution(13, 17));
console.log(solution(24, 27));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
