## 짝지어 제거하기

[2017 팁스타운 > 짝지어 제거하기](https://programmers.co.kr/learn/courses/30/lessons/12973)

``` js
function solution(s) {
    const temp = [];

    for (let i = 0; i < s.length; i++) {
        if (temp[temp.length - 1] === s[i]) temp.pop();
        else temp.push(s[i]);
    }

    return temp.length ? 0 : 1;
}

console.log(solution('baabaa'));
console.log(solution('baabaa'));
console.log(solution('cdcd'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)