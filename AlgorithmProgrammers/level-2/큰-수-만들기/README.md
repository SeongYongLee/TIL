## 큰 수 만들기

[탐욕법(Greedy) > 큰 수 만들기](https://programmers.co.kr/learn/courses/30/lessons/42883)

``` js
function solution(number, k) {
    let answer = '';

    while (k > 0) {
        if (k === number.length) return answer;

        let maxIndex = 0;

        for (let i = 0; i <= k; i++) {
            if (number[i] === '9') {
                maxIndex = i;
                break;
            }
            maxIndex = number[maxIndex] >= number[i] ? maxIndex : i;
        }

        answer += number[maxIndex];
        number = number.slice(maxIndex + 1);
        k -= maxIndex;
    }

    return answer + number;
}

console.log(solution('1924', 2));
console.log(solution('1231234', 3));
console.log(solution('4177252841', 9));
console.log(solution('9', 0));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)