## 2개 이하로 다른 비트

[월간 코드 챌린지 시즌2 > 2개 이하로 다른 비트](https://programmers.co.kr/learn/courses/30/lessons/77885)

``` js
// 1 - 효율성 탈락
// function solution(words) {
//     const isAnswer = (x, word) => {
//         const wLength = word.length;
//         const nextNum = x.toString(2);
//         const nextNumLength = nextNum.length;
//         let diff = 0;

//         for (let i = 1; i <= nextNumLength; i++) {
//             const currentNum = word[wLength - i];

//             if ((currentNum ? currentNum : '0') !== nextNum[nextNumLength - i] && diff++ === 2)
//                 return false;
//         }

//         return diff ? true : false;
//     };

//     return words.map((x) => {
//         const word = x.toString(2);

//         while (x++) {
//             if (isAnswer(x, word)) return x;
//         }
//     });
// }

// 2 - 효율성 탈락
// function solution(words) {
//     return words.map((x) => {
//         const word = x;

//         while (1) {
//             if (
//                 [1, 2].includes(
//                     (word ^ ++x)
//                         .toString(2)
//                         .split('')
//                         .filter((x) => +x).length,
//                 )
//             )
//                 return x;
//         }
//     });
// }

// 3
function solution(words) {
    return words.map((x) => {
        const word = x.toString(2);
        let numCount = 0;

        for (let i = word.length - 1; i >= 0; i--) {
            if (+word[i]) numCount++;
            else break;
        }

        numCount = Math.pow(2, numCount - 1);

        return x + (numCount > 1 ? numCount : 1);
    });
}

console.log(solution([2, 7]));
console.log(
    solution([
        1001, 337, 0, 1, 333, 673, 343, 221, 898, 997, 121, 1015, 665, 779, 891, 421, 222, 256, 512,
        128, 100,
    ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)