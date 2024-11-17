## 상호 평가

[위클리 챌린지 > 2주차 > 상호 평가](https://programmers.co.kr/learn/courses/30/lessons/83201)

```js
function solution(scores) {
  const getGrade = (score) => {
    const sumScore = score.reduce((r, s) => r + s) / score.length;

    return sumScore >= 90
      ? "A"
      : sumScore >= 80
        ? "B"
        : sumScore >= 70
          ? "C"
          : sumScore >= 50
            ? "D"
            : "F";
  };

  return scores
    .reduce(
      (result, score) => score.map((s, i) => [...(result[i] || []), s]),
      [],
    )
    .reduce((result, score, i) => {
      const sliceScore = score.slice();
      const selfScore = score.splice(i, 1);

      return (
        result +
        getGrade(
          selfScore > Math.max(...score) || selfScore < Math.min(...score)
            ? score
            : sliceScore,
        )
      );
    }, "");
}

console.log(
  solution([
    [100, 90, 98, 88, 65],
    [50, 45, 99, 85, 77],
    [47, 88, 95, 80, 67],
    [61, 57, 100, 80, 65],
    [24, 90, 94, 75, 65],
  ]),
);
console.log(
  solution([
    [50, 90],
    [50, 87],
  ]),
);
console.log(
  solution([
    [70, 49, 90],
    [68, 50, 38],
    [73, 31, 100],
  ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
