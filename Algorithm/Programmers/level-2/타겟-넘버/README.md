## 타겟 넘버

[깊이/너비 우선 탐색(DFS/BFS) > 타겟 넘버](https://programmers.co.kr/learn/courses/30/lessons/43165)

```js
// 1
// function solution(numbers, target) {
//     let answer = 0;
//     const sumNumber = numbers.reduce((r, n) => r + n);
//     if (sumNumber === target) return 1;
//     numbers.sort((x, y) => x - y);

//     const isTarget = (num, sum) => {
//         const numTemp = num.slice();
//         const numCurrent = numTemp.splice(0, 1);
//         const minus = sum - numCurrent * 2;
//         if (minus === target) answer++;
//         if (numTemp.length !== 0) {
//             isTarget(numTemp, sum);
//             if (minus > 0) isTarget(numTemp, minus);
//         }
//     };

//     isTarget(numbers, sumNumber);

//     return answer;
// }

// 2 - Refactoring
function solution(numbers, target) {
  let answer = 0;
  const sumNumber = numbers.reduce((r, n) => r + n);
  if (sumNumber === target) return 1;
  numbers.sort((x, y) => x - y);

  const isTarget = (index, sum) => {
    const minus = sum - numbers[index] * 2;
    index++;

    if (minus === target) answer++;
    if (index !== numbers.length && minus > 0) {
      isTarget(index, sum);
      isTarget(index, minus);
    }
  };

  isTarget(0, sumNumber);

  return answer;
}

console.log(solution([1, 1, 1, 1, 1], 3));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
