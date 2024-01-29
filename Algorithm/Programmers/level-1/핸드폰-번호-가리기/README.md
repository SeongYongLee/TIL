## 핸드폰 번호 가리기

[연습문제 > 핸드폰 번호 가리기](https://programmers.co.kr/learn/courses/30/lessons/12948)

``` js
// 1
// function solution(phone_number) {
//     const split_number = phone_number.split('');
//     const snLength = split_number.length;

//     return '*'.repeat(snLength - 4) + split_number.slice(snLength - 4, snLength).join('');
// }

// 2 - Refactoring
function solution(phone_number) {
    return '*'.repeat(phone_number.length - 4) + phone_number.slice(-4);
}

console.log(solution('01033334444'));
console.log(solution('027778888'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)