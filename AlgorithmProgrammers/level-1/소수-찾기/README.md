## 소수 찾기

[연습문제 > 소수 찾기](https://programmers.co.kr/learn/courses/30/lessons/12921)

``` js
// 1 - 효율성 테스트 탈락
// function solution(n) {
//     const sosu = [];

//     for (let x = 2; x < n + 1; x++) {
//         let thisSosu = true;

//         for (let y = 0; y < sosu.length; y++) {
//             if (x % sosu[y] === 0) {
//                 thisSosu = false;
//                 break;
//             }
//         }

//         if (thisSosu) sosu.push(x);
//     }

//     return sosu.length;
// }

// 2 - sqrt를 사용하여 효율성 증가
// function solution(n) {
//     const sosu = [];
//     const sqrt = Math.sqrt(n);
//     let sqrtsosu = 0;
//     let sqrtlength = 0;

//     for (let x = 2; x < n + 1; x++) {
//         let thisSosu = true;

//         for (let y = 0; y < sqrtlength; y++) {
//             if (x % sosu[y] === 0) {
//                 thisSosu = false;
//                 break;
//             }
//         }

//         if (thisSosu) {
//             sosu.push(x);
//             if (sqrtsosu === 0) {
//                 sqrtlength = sosu.length;
//                 if (x > sqrt) sqrtsosu = x;
//             }
//         }
//     }

//     return sosu.length;
// }

// 3 - 에라토스테네스의 체
function solution(nums) {
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

    return arr.filter((e) => e).length;
}

console.log(solution(10));
console.log(solution(5));
console.log(solution(100));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)