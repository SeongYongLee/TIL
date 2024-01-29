## 나머지가 1이 되는 수 찾기

[월간 코드 챌린지 시즌3 > 나머지가 1이 되는 수 찾기](https://programmers.co.kr/learn/courses/30/lessons/87389)

``` js
function solution(n) {
    let i = 1;

    while (i++) {
        if (n % i === 1) return i;
    }
}

console.log(solution(10));
console.log(solution(12));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)