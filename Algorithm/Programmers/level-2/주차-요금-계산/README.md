## 주차 요금 계산

[2022 KAKAO BLIND RECRUITMENT > 주차 요금 계산](https://school.programmers.co.kr/learn/courses/30/lessons/92341)

```js
function solution(fees, records) {
  const answer = [];
  const [basicTime, basicFee, unitTime, unitFee] = fees;
  const result = {};

  records.map((record) => {
    const [time, carNumber, status] = record.split(" ");

    if (!result[carNumber]) {
      result[carNumber] = {
        total: 0,
        inTime: null,
      };
    }

    if (status === "IN") {
      result[carNumber].inTime = time;

      return;
    }

    if (status === "OUT") {
      const inTime = result[carNumber].inTime.split(":");
      const outTime = time.split(":");

      const inTotal = parseInt(inTime[0]) * 60 + parseInt(inTime[1]);
      const outTotal = parseInt(outTime[0]) * 60 + parseInt(outTime[1]);

      result[carNumber].total += outTotal - inTotal;
      result[carNumber].inTime = null;

      return;
    }
  });

  Object.keys(result)
    .sort()
    .forEach((key) => {
      const car = result[key];

      if (car.inTime) {
        const inTime = car.inTime.split(":");
        car.total += 1439 - (parseInt(inTime[0]) * 60 + parseInt(inTime[1]));
      }

      const totalFee =
        basicFee +
        (car.total > basicTime
          ? Math.ceil((car.total - basicTime) / unitTime) * unitFee
          : 0);

      answer.push(totalFee);
    });

  return answer;
}

console.log(
  solution(
    [180, 5000, 10, 600],
    [
      "05:34 5961 IN",
      "06:00 0000 IN",
      "06:34 0000 OUT",
      "07:59 5961 OUT",
      "07:59 0148 IN",
      "18:59 0000 IN",
      "19:09 0148 OUT",
      "22:59 5961 IN",
      "23:00 5961 OUT",
    ]
  )
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
