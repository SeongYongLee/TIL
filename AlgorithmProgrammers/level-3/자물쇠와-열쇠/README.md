## 자물쇠와 열쇠

[2020 KAKAO BLIND RECRUITMENT > 자물쇠와 열쇠](https://programmers.co.kr/learn/courses/30/lessons/60059)

``` js
function solution(key, lock) {
    const keyLength = key.length;
    const lockLength = lock.length;
    let rotateKey = key;

    function rotate(array) {
        return array.reduce((result, x) => {
            for (let i = 0; i < keyLength; i++) {
                result[keyLength - i - 1] = [
                    ...(result[keyLength - i - 1] || []),
                    x[i],
                ];
            }
            return result;
        }, []);
    }
    function isFull(li, lj, key, lock) {
        for (let ki = 0; ki < keyLength; ki++) {
            for (let kj = 0; kj < keyLength; kj++) {
                if (
                    li + ki >= 0 &&
                    lj + kj >= 0 &&
                    li + ki < lockLength &&
                    lj + kj < lockLength
                ) {
                    lock[li + ki][lj + kj] += key[ki][kj];
                    if (lock[li + ki][lj + kj] !== 1) return false;
                }
            }
        }
        for (let i = 0; i < lockLength; i++) {
            for (let j = 0; j < lockLength; j++) {
                if (lock[i][j] !== 1) return false;
            }
        }
        return true;
    }

    for (let i = 0; i < 4; i++) {
        for (let li = -keyLength + 1; li < lockLength; li++) {
            for (let lj = -keyLength + 1; lj < lockLength; lj++) {
                if (isFull(li, lj, rotateKey, JSON.parse(JSON.stringify(lock))))
                    return true;
            }
        }
        if (i === 3) return false;
        else rotateKey = rotate(rotateKey);
    }
}

console.log(
    solution(
        [
            [0, 0, 0],
            [1, 0, 0],
            [0, 1, 1],
        ],
        [
            [1, 1, 1],
            [1, 1, 0],
            [1, 0, 1],
        ]
    )
);
console.log(
    solution(
        [
            [0, 1, 0],
            [1, 1, 1],
            [0, 1, 1],
        ],
        [
            [1, 1, 1, 1, 1],
            [1, 1, 1, 1, 1],
            [1, 1, 1, 0, 0],
            [1, 1, 0, 0, 0],
            [1, 1, 1, 0, 1],
        ]
    )
);
console.log(
    solution(
        [
            [1, 1, 1],
            [0, 0, 1],
            [1, 1, 1],
        ],
        [
            [0, 1, 1, 1],
            [1, 1, 1, 1],
            [1, 1, 1, 1],
            [1, 1, 1, 1],
        ]
    )
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)