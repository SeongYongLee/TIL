## 문자열 내림차순으로 배치하기

[연습문제 > 문자열 내림차순으로 배치하기](https://programmers.co.kr/learn/courses/30/lessons/12917)

``` js
function solution(s) {
    return s.split('').sort().reverse().join('');
}

console.log(solution("Zbcdefg"));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)