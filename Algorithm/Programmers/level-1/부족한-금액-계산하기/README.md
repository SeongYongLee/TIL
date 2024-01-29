## 부족한 금액 계산하기

[위클리 챌린지 > 1주차 > 부족한 금액 계산하기](https://programmers.co.kr/learn/courses/30/lessons/82612)

``` js
function solution(price, money, count) {
    const answer = price * (count + 1) * (count / 2) - money;

    return answer > 0 ? answer : 0;
}

console.log(solution(3, 20, 4));

// 1 1
// 3 2
// 6 3
// 10 4
// 15 5
// 21 6 (n + 1) * (n / 2)
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)