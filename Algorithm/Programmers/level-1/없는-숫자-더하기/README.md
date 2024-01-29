## 없는 숫자 더하기

[월간 코드 챌린지 시즌3 > 없는 숫자 더하기](https://programmers.co.kr/learn/courses/30/lessons/86051)

``` js
function solution(words) {
    let answer = 0;

    for (let i = 0; i < 10; i++) {
        if (words.indexOf(i) === -1) answer += i;
    }

    return answer;
}

console.log(solution([1, 2, 3, 4, 6, 7, 8, 0]));
console.log(solution([5, 8, 4, 0, 6, 7, 9]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)