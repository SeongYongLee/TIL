## 오픈채팅방

[2019 KAKAO BLIND RECRUITMENT > 오픈채팅방](https://programmers.co.kr/learn/courses/30/lessons/42888)

```js
function solution(record) {
  const answer = [];
  const id = {};
  const string = {
    Enter: "님이 들어왔습니다.",
    Leave: "님이 나갔습니다.",
  };

  for (let i = 0; i < record.length; i++) {
    const temp = record[i].split(" ");

    if (temp[0] !== "Change") answer.push([temp[1], temp[0]]);
    if (temp[2]) id[temp[1]] = temp[2];
  }

  return answer.map((x) => `${id[x[0]]}${string[x[1]]}`);
}

console.log(
  solution([
    "Enter uid1234 Muzi",
    "Enter uid4567 Prodo",
    "Leave uid1234",
    "Enter uid1234 Prodo",
    "Change uid4567 Ryan",
  ]),
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
