## 소수 만들기

[Summer/Winter Coding(~2018) > 소수 만들기](https://programmers.co.kr/learn/courses/30/lessons/12977)

```js
// 1
// function isPrimeNum(n) {
//     // if (n === 0 || n === 1) return false;

//     for (let i = 2; i * i <= n; i++) {
//         if (!(n % i)) return false;
//     }

//     return true;
// }

// function solution(nums) {
//     let answer = 0;

//     const sol = (nums, start, end) => {
//         if (!end) {
//             if (isPrimeNum(nums.reduce((r, c) => r + c))) answer++;
//         } else {
//             for (let i = start; i <= nums.length - end; i++) {
//                 const temp = nums.slice();
//                 temp.splice(i, 1);
//                 sol(temp, i, end - 1);
//             }
//         }
//     };

//     sol(nums, 0, nums.length - 3);

//     return answer;
// }

// 2 - 에라토스테네스의 체
function eratos(nums) {
  const sqrt = Math.sqrt(nums);
  const arr = Array(nums + 1)
    .fill(true)
    .fill(false, 0, 2);

  for (let i = 2; i <= sqrt; i++) {
    if (!arr[i]) continue;

    for (let j = i * i; j <= nums; j += i) {
      arr[j] = false;
    }
  }

  return arr;
}

function solution(nums) {
  let answer = 0;
  const primeList = eratos(nums.reduce((r, c) => r + c));

  const sol = (nums, start, end) => {
    if (!end) {
      if (primeList[nums.reduce((r, c) => r + c)]) answer++;
    } else {
      for (let i = start; i <= nums.length - end; i++) {
        const temp = nums.slice();
        temp.splice(i, 1);
        sol(temp, i, end - 1);
      }
    }
  };

  sol(nums, 0, nums.length - 3);

  return answer;
}

console.log(solution([1, 2, 3, 4]));
console.log(solution([1, 2, 7, 6, 4]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
