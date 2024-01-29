## 입국심사

[이분탐색 > 입국심사](https://programmers.co.kr/learn/courses/30/lessons/43238)

``` js
function solution(n, times) {
    times.sort((a, b) => a - b);

    const tLength = times.length;
    let left = 1;
    let right = n * times[tLength - 1];
    let answer = right;

    outer: while (left <= right) {
        const mid = parseInt((left + right) / 2);
        let count = 0;

        for (let i = 0; i < tLength; i++) {
            count += parseInt(mid / times[i]);
            if (count >= n) {
                answer = mid;
                right = mid - 1;
                continue outer;
            }
        }

        left = mid + 1;
    }

    return answer;
}

console.log(solution(5, [4, 7, 10, 11]));
console.log(solution(6, [7, 10, 100]));
console.log(solution(6, [7, 10, 11]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)