## [1차] 비밀지도

[2018 KAKAO BLIND RECRUITMENT > [1차] 비밀지도](https://programmers.co.kr/learn/courses/30/lessons/17681)

``` js
// 1
// function solution(n, arr1, arr2) {
//     return arr1.map((a, i) =>
//         ('0'.repeat(n) + (a | arr2[i]).toString(2))
//             .slice(-n)
//             .split('')
//             .reduce((result, i) => result + (i === '1' ? '#' : ' '), ''),
//     );
// }

// 2 - Refactoring
const addZero = (n, s) => {
    return '0'.repeat(n - s.length) + s;
}

function solution(n, arr1, arr2) {
    return arr1.map((v, i) =>
        addZero(n, (v | arr2[i]).toString(2)).replace(/1|0/g, (a) => (+a ? '#' : ' ')),
    );
}
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)