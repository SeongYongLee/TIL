## 정수 내림차순으로 배치하기

[연습문제 > 정수 내림차순으로 배치하기](https://programmers.co.kr/learn/courses/30/lessons/12933)

``` js
function solution(n) {
    return +(n + '')
        .split('')
        .sort((x, y) => y - x)
        .join('');
}

console.log(solution(118372));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)