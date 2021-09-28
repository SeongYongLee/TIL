## 가장 큰 수

[정렬 > 가장 큰 수](https://programmers.co.kr/learn/courses/30/lessons/42746)

``` js
function solution(numbers) {
    const answer = numbers
        .map((i) => i + '')
        .sort((a, b) => b + a - (a + b))
        .join('');

    return answer[0] === '0' ? '0' : answer;
}

console.log(solution([3, 30, 34, 5, 9, 4, 40, 42]));
console.log(solution([[3, 30, 34, 5, 9], "9534330"],))
console.log(solution([[10, 101], '10110'],))
console.log(solution([[1, 11, 111, 1111], '1111111111'],))
console.log(solution([0, 0, 0, 0, 0, 0]))
console.log(solution([[2,20,200], '220200'],))
console.log(solution([[0,0,70], '7000'],))
console.log(solution([0,0,0,1000]))
console.log(solution([[0,0,1000,0], '1000000'],))
console.log(solution([[1000,0,0], '100000'],))
console.log(solution([[12,121], '12121'],))
console.log(solution([[21,212], '21221'],))
console.log(solution([[11, 12, 10], '121110'],))
console.log(solution([[0,0,0,1], '1000'],))
console.log(solution([[1,2,3,1,1,3], '332111'],))
console.log(solution([[1,2,21, 21], '221211']))
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)