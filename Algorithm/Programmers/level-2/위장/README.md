## 위장

[해시 > 위장](https://programmers.co.kr/learn/courses/30/lessons/42578)

```js
// 1
// function solution(clothes) {
//     let sortNum = [];
//     let sortKind = [];

//     for (let i = 0; i < clothes.length; i++) {
//         let temp = sortKind.indexOf(clothes[i][1])
//         if (temp === -1) {
//             sortKind.push(clothes[i][1]);
//             sortNum.push(1);
//         } else {
//             sortNum[temp]++;
//         }
//     }

//     return sortNum.reduce((i,j) => i * (j + 1), 1) - 1;
// }

// 2 - Refactoring
function solution(clothes) {
  let answer = 1;
  const sortKind = {};

  for (let c of clothes) {
    sortKind[c[1]] = (sortKind[c[1]] || 0) + 1;
  }
  for (let s in sortKind) {
    answer *= sortKind[s] + 1;
  }

  return answer - 1;
}

console.log(
  solution([
    ["yellow_hat", "headgear"],
    ["blue_sunglasses", "eyewear"],
    ["green_turban", "headgear"],
  ]),
);
console.log(
  solution([
    ["crow_mask", "face"],
    ["blue_sunglasses", "face"],
    ["smoky_makeup", "face"],
  ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
