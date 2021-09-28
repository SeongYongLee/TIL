## 소수 찾기

[완전탐색 > 소수 찾기](https://programmers.co.kr/learn/courses/30/lessons/42839)

``` js
function isPrimeNum(n) {
    if (n === 0 || n === 1) return false;
    for (let i = 2; i * i <= n; i++) {
        if (!(n % i)) return false;
    }
    return true;
}

function solution(numbers) {
    const numberSplit = numbers.split('');
    const answer = new Set();

    const findPrimeNum = (currentNum, remainNum) => {
        for (let i = 0; i < remainNum.length; i++) {
            const remainNumSlice = remainNum.slice();
            const currentNumSlice = +(currentNum + remainNumSlice.splice(i, 1));

            if (isPrimeNum(currentNumSlice)) answer.add(currentNumSlice);
            findPrimeNum(currentNumSlice, remainNumSlice);
        }
    };

    findPrimeNum('', numberSplit);

    return answer.size;
}

console.log(solution('17'));
console.log(solution('011'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)