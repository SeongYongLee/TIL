## [1차] 뉴스 클러스터링

[2018 KAKAO BLIND RECRUITMENT > [1차] 뉴스 클러스터링](https://programmers.co.kr/learn/courses/30/lessons/17677)

``` js
// 1
// function solution(str1, str2) {
//     const upperStr1 = str1.toUpperCase().split('');
//     const upperStr2 = str2.toUpperCase().split('');
//     const isCharStr1 = upperStr1
//         .map((s) => s.charCodeAt())
//         .map((s) => (90 >= s && s >= 65 ? 1 : 0));
//     const isCharStr2 = upperStr2
//         .map((s) => s.charCodeAt())
//         .map((s) => (90 >= s && s >= 65 ? 1 : 0));
//     const str1Array = [];
//     const str2Array = [];

//     for (let i = 0; i < isCharStr1.length - 1; i++) {
//         if (isCharStr1[i] && isCharStr1[i + 1]) {
//             str1Array.push(upperStr1.slice(i, i + 2).join(''));
//         }
//     }
//     for (let i = 0; i < isCharStr2.length - 1; i++) {
//         if (isCharStr2[i] && isCharStr2[i + 1]) {
//             str2Array.push(upperStr2.slice(i, i + 2).join(''));
//         }
//     }

//     const union = [];
//     const intersection = [];

//     for (let i = 0; i < str1Array.length; i++) {
//         if (str2Array.indexOf(str1Array[i]) >= 0) {
//             intersection.push(...str2Array.splice(str2Array.indexOf(str1Array[i]), 1));
//         }
//         union.push(str1Array[i]);
//     }

//     for (let i = 0; i < str2Array.length; i++) {
//         union.push(str2Array[i]);
//     }

//     return union.length === 0 ? 65536 : Math.floor((65536 * intersection.length) / union.length);
// }

// 2 - Refactoring
function solution(str1, str2) {
    const upperStr1 = str1.toUpperCase().split('');
    const upperStr2 = str2.toUpperCase().split('');
    const isCharStr1 = upperStr1.map((s) => s.charCodeAt()).map((s) => 90 >= s && s >= 65);
    const isCharStr2 = upperStr2.map((s) => s.charCodeAt()).map((s) => 90 >= s && s >= 65);
    const str1Array = [];
    const str2Array = [];

    for (let i = 0; i < isCharStr1.length - 1; i++) {
        if (isCharStr1[i] && isCharStr1[i + 1]) {
            str1Array.push(upperStr1.slice(i, i + 2).join(''));
        }
    }
    for (let i = 0; i < isCharStr2.length - 1; i++) {
        if (isCharStr2[i] && isCharStr2[i + 1]) {
            str2Array.push(upperStr2.slice(i, i + 2).join(''));
        }
    }

    let union = str1Array.length;
    const intersection = [];

    for (let i = 0; i < str1Array.length; i++) {
        const index = str2Array.indexOf(str1Array[i]);
        if (index !== -1) {
            intersection.push(...str2Array.splice(index, 1));
        }
    }

    union += str2Array.length;

    return union === 0 ? 65536 : Math.floor((65536 * intersection.length) / union);
}

console.log(solution('FRANCE', 'french'));
console.log(solution('aa1+aa2', 'AAAA12'));
console.log(solution('=M*C^2', 'e=m*c^2'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)