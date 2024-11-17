## 두 개 뽑아서 더하기

[월간 코드 챌린지 시즌1 > 두 개 뽑아서 더하기](https://programmers.co.kr/learn/courses/30/lessons/68644)

```js
function solution(words) {
  const answer = new Set();
  const wLength = words.length;

  for (let i = 0; i < wLength; i++) {
    for (let j = i + 1; j < wLength; j++) {
      answer.add(words[i] + words[j]);
    }
  }

  return [...answer].sort((a, b) => a - b);
}

console.log(solution([2, 1, 3, 4, 1]));
console.log(solution([5, 0, 2, 7]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
