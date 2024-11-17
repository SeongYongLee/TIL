## 124 나라의 숫자

[연습문제 > 124 나라의 숫자](https://programmers.co.kr/learn/courses/30/lessons/12899)

```js
// 1
// function solution(n) {
//     const temp = n.toString(3).split('');

//     for (let x = temp.length - 1; x >= 0; x--) {
//         switch (+temp[x]) {
//             case 0:
//                 if (x !== 0) {
//                     temp[x - 1] = +temp[x - 1] - 1;
//                     temp[x] = 4;
//                 } else temp.shift();
//                 break;
//             case -1:
//                 temp[x - 1] = +temp[x - 1] - 1;
//                 temp[x] = 2;
//                 break;
//         }
//     }

//     return temp.join('');
// }
// /*
// 1   1   1
// 2   2   2
// 3   10  4   !
// 4   11  11
// 5   12  12
// 6   20  14  !
// 7   21  21
// 8   22  22
// 9   100 24  !
// 10  101 41  !
// 11  102 42  !
// 12  110 44  !
// 13  111 111
// 14  112 112
// 15  120 114 !
// 16  121 121
// */

// 2 - Refactoring
/* 
    프로그래머스 - 다른 사람의 풀이 참고
*/
function solution(n) {
  return n ? solution(parseInt((n - 1) / 3)) + [1, 2, 4][(n - 1) % 3] : "";
}
// /*
// 1   1           1
// 2   1*2         2
// 3   1*3         4
// 4   3*1+1*1     11
// 5   3*1+1*2     12
// 6   3*1+1*3     14
// 7   3*2+1*1     21
// */

console.log(solution(1));
console.log(solution(2));
console.log(solution(3));
console.log(solution(4));
console.log(solution(13));
console.log(solution(10));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
