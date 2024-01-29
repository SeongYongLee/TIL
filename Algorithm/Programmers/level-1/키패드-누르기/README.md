## 키패드 누르기

[2020 카카오 인턴십 > 키패드 누르기](https://programmers.co.kr/learn/courses/30/lessons/67256)

``` js
function solution(numbers, hand) {
    // 10 = *, 11 = 0, 12 = #
    let leftFinger = 10;
    let rightFinger = 12;
    let answer = '';

    const moveLeftFinger = (n) => {
        answer += 'L';
        leftFinger = n;
    };
    const moveRightFinger = (n) => {
        answer += 'R';
        rightFinger = n;
    };
    const setDistance = (n) => {
        if ([0].includes(n)) {
            return 0;
        } else if ([1, 3].includes(n)) {
            return 1;
        } else if ([2, 4, 6].includes(n)) {
            return 2;
        } else if ([5, 7, 9].includes(n)) {
            return 3;
        } else {
            // [8,10].includes(n)
            return 4;
        }
    };

    for (let n of numbers) {
        if (n === 0) n = 11;

        if ([1, 4, 7].includes(n)) {
            moveLeftFinger(n);
        } else if ([3, 6, 9].includes(n)) {
            moveRightFinger(n);
        } else {
            // [2,5,8,11].includes(n)
            const left = setDistance(Math.abs(leftFinger - n));
            const right = setDistance(Math.abs(rightFinger - n));

            if (left < right) {
                moveLeftFinger(n);
            } else if (left > right) {
                moveRightFinger(n);
            } else {
                hand === 'left' ? moveLeftFinger(n) : moveRightFinger(n);
            }
        }
        // console.log(n, leftFinger, rightFinger);
    }

    return answer;
}

console.log(solution([1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5], 'right'));
console.log(solution([7, 0, 8, 2, 8, 3, 1, 5, 7, 6, 2], 'left'));
console.log(solution([1, 2, 3, 4, 5, 6, 7, 8, 9, 0], 'right'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)