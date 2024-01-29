## 문자열 다루기 기본

[연습문제 > 문자열 다루기 기본](https://programmers.co.kr/learn/courses/30/lessons/12918)

``` js
function solution(s) {
    return [4, 6].includes(s.length) && +s + '' === s ? true : false;
}

console.log(solution("a234"));
console.log(solution("1234"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)