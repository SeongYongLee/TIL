## 서울에서 김서방 찾기

[연습문제 > 서울에서 김서방 찾기](https://programmers.co.kr/learn/courses/30/lessons/12919)

``` js
// 1
// function solution(seoul) {
//     return `김서방은 ${seoul.indexof('kim')}에 있다`;
// }

// 2 - 프로그래머스에서 템플릿 문자열 지원 X
function solution(seoul) {
    return '김서방은 ' + seoul.indexOf('Kim') + '에 있다';
}

console.log(solution(['Jane', 'Kim']));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)