## 영어 끝말잇기

[월간 코드 챌린지 시즌1 > 이진 변환 반복하기](https://programmers.co.kr/learn/courses/30/lessons/70129)

``` js
// 1
// function sol(s, play_count, delete_count) {
//     const temp = s
//         .split('')
//         .reduce((r, c) => (c === '0' ? r : r + '1'), '').length;
//     const binaryTemp = temp.toString(2);

//     return s === binaryTemp
//         ? [play_count, delete_count]
//         : sol(binaryTemp, ++play_count, delete_count + s.length - temp);
// }

// function solution(s) {
//     return sol(s, 0, 0);
// }

// 2 - Refactoring 재귀
// function solution(s) {
//     const sol = (s, times, deleteCount) => {
//         if (s === '1') return [times, deleteCount];

//         const temp = s.split('').filter((v) => +v).length;

//         return sol(temp.toString(2), ++times, deleteCount + s.length - temp);
//     };

//     return sol(s, 0, 0);
// }

// 3 - Refactoring while
function solution(s) {
    let times = 0;
    let deleteCount = 0;

    while (s !== '1') {
        const temp = s.split('').filter((v) => +v).length;
        times++;
        deleteCount += s.length - temp;
        s = temp.toString(2);
    }

    return [times, deleteCount];
}

console.log(solution('110010101001'));
console.log(solution('01110'));
console.log(solution('1111111'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)