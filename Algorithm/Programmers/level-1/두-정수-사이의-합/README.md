## 두 정수 사이의 합

[연습문제 > 두 정수 사이의 합](https://programmers.co.kr/learn/courses/30/lessons/12912)

``` js
function solution(a, b) {
    const calc = (min, max) => {
        let answer = 0;
        
        for (let i = min; i <= max; i++) {
            answer += i;
        }
        
        return answer;
    }
    
    return a > b ? calc(b, a) : calc(a, b);
}

console.log(solution(3, 5));
console.log(solution(3, 3));
console.log(solution(5, 3));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)