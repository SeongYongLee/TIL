## 쿼드압축 후 개수 세기

[월간 코드 챌린지 시즌1 > 쿼드압축 후 개수 세기](https://programmers.co.kr/learn/courses/30/lessons/68936)

```js
function solution(arr) {
  const answer = arr.reduce(
    (r, a) => {
      a.map((b) => r[b]++);
      return r;
    },
    [0, 0],
  );
  const isCompress = (num, i, j, k) => {
    for (let a = j; a < j + i; a++) {
      for (let b = k; b < k + i; b++) {
        if (num !== arr[a][b]) return false;
      }
    }
    return true;
  };
  const compress = (i, j, k) => {
    for (let a = j; a < j + i; a++) {
      for (let b = k; b < k + i; b++) {
        arr[a][b] = -1;
      }
    }
  };

  const aLength = arr.length;

  for (let i = aLength; i > 1; i /= 2) {
    for (let j = 0; j < aLength; j += i) {
      for (let k = 0; k < aLength; k += i) {
        const num = arr[j][k];
        if (num === -1) continue;
        if (isCompress(num, i, j, k)) {
          compress(i, j, k);
          answer[num] -= i * i - 1;
        }
      }
    }
  }

  return answer;
}

console.log(
  solution([
    [1, 1, 0, 0],
    [1, 0, 0, 0],
    [1, 0, 0, 1],
    [1, 1, 1, 1],
  ]),
);
console.log(
  solution([
    [1, 1, 1, 1, 1, 1, 1, 1],
    [0, 1, 1, 1, 1, 1, 1, 1],
    [0, 0, 0, 0, 1, 1, 1, 1],
    [0, 1, 0, 0, 1, 1, 1, 1],
    [0, 0, 0, 0, 0, 0, 1, 1],
    [0, 0, 0, 0, 0, 0, 0, 1],
    [0, 0, 0, 0, 1, 0, 0, 1],
    [0, 0, 0, 0, 1, 1, 1, 1],
  ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
