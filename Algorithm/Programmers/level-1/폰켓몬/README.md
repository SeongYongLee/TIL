## 폰켓몬

[찾아라 프로그래밍 마에스터 > 폰켓몬](https://programmers.co.kr/learn/courses/30/lessons/1845)

``` js
function solution(nums) {
    const numCount = new Set(nums).size;
    const numMax = nums.length / 2;
    
    return numCount > numMax ? numMax : numCount;
}

console.log(solution([3, 1, 2, 3]));
console.log(solution([3, 3, 3, 2, 2, 4]));
console.log(solution([3, 3, 3, 2, 2, 2]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)