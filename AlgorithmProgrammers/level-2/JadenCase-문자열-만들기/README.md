## JadenCase 문자열 만들기

[연습문제 > JadenCase 문자열 만들기](https://programmers.co.kr/learn/courses/30/lessons/12951)

``` js
function solution(s) {
    return s
        .split(' ')
        .map((str) => str.charAt(0).toUpperCase() + str.slice(1).toLowerCase())
        .join(' ');
}

console.log(solution('3people  unFollowed me'));
console.log(solution('for the last week'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)