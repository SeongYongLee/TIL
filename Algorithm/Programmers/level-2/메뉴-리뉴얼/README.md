## 메뉴 리뉴얼

[2021 KAKAO BLIND RECRUITMENT > 메뉴 리뉴얼](https://programmers.co.kr/learn/courses/30/lessons/72411)

```js
// 1
// function solution(orders, course) {
//     const answer = [];
//     const orderList = [];

//     function getOrderList(list, order, i) {
//         if (order.length > i) {
//             getOrderList(list, order, i + 1);
//             getOrderList([...list, order[i]], order, i + 1);
//         } else {
//             if (list.length > 1) orderList[orderList.length - 1].push(list.sort().join(''));
//         }
//     }

//     for (let i = 0; i < orders.length; i++) {
//         orderList.push([]);
//         getOrderList([], orders[i], 0);
//     }

//     for (let i = 0; i < course.length; i++) {
//         const tempObject = {};

//         for (let j = 0; j < orderList.length; j++) {
//             for (let k = 0; k < orderList[j].length; k++) {
//                 if (orderList[j][k].length !== course[i]) continue;

//                 if (tempObject[orderList[j][k]]) {
//                     tempObject[orderList[j][k]] += 1;
//                 } else {
//                     tempObject[orderList[j][k]] = 1;
//                 }
//             }
//         }

//         let tempArray = [];
//         let maxNum = 0;

//         for (const [key, value] of Object.entries(tempObject)) {
//             if (maxNum === value) {
//                 tempArray.push(key);
//             } else if (maxNum < value) {
//                 maxNum = value;
//                 tempArray = [key];
//             }
//         }

//         if (maxNum >= 2) answer.push(...tempArray);
//     }

//     return answer.sort();
// }

// 2 - Refactoring
// function solution(orders, course) {
//     const answer = [];
//     const orderList = [];
//     const answerObject = {};

//     function getOrderList(list, order, i) {
//         if (order.length > i) {
//             getOrderList(list, order, i + 1);
//             getOrderList([...list, order[i]], order, i + 1);
//         } else if (list.length > 1) orderList[orderList.length - 1].push(list.sort().join(''));
//     }

//     for (let i = 0; i < orders.length; i++) {
//         orderList.push([]);
//         getOrderList([], orders[i], 0);
//     }

//     for (let i = 0; i < course.length; i++) {
//         answerObject[course[i]] = {};
//     }

//     for (let j = 0; j < orderList.length; j++) {
//         for (let k = 0; k < orderList[j].length; k++) {
//             const index = orderList[j][k].length;
//             if (!answerObject[index]) continue;

//             if (answerObject[index][orderList[j][k]]) {
//                 answerObject[index][orderList[j][k]] += 1;
//             } else {
//                 answerObject[index][orderList[j][k]] = 1;
//             }
//         }
//     }

//     for (const index in answerObject) {
//         let maxNum = 0;

//         for (const [key, value] of Object.entries(answerObject[index])) {
//             if (maxNum === value) {
//                 tempArray.push(key);
//             } else if (maxNum < value) {
//                 maxNum = value;
//                 tempArray = [key];
//             }
//         }

//         if (maxNum >= 2) answer.push(...tempArray);
//     }

//     return answer.sort();
// }

// 3 - Refactoring
function solution(orders, course) {
  const answer = [];
  const orderList = [];
  const answerObject = {};
  const answerMax = {};

  function getOrderList(list, order, i) {
    if (order.length > i) {
      getOrderList(list, order, i + 1);
      getOrderList([...list, order[i]], order, i + 1);
    } else if (list.length > 1)
      orderList[orderList.length - 1].push(list.sort().join(""));
  }

  for (let i = 0; i < orders.length; i++) {
    orderList.push([]);
    getOrderList([], orders[i], 0);
  }

  for (let i = 0; i < course.length; i++) {
    answerObject[course[i]] = {};
    answerMax[course[i]] = { max: 1 };
  }

  for (let j = 0; j < orderList.length; j++) {
    for (let k = 0; k < orderList[j].length; k++) {
      const index = orderList[j][k].length;
      if (!answerObject[index]) continue;

      if (answerObject[index][orderList[j][k]]) {
        answerObject[index][orderList[j][k]] += 1;
        if (answerObject[index][orderList[j][k]] > answerMax[index].max) {
          answerMax[index].max = answerObject[index][orderList[j][k]];
          answerMax[index].list = [orderList[j][k]];
        } else if (
          answerObject[index][orderList[j][k]] === answerMax[index].max
        ) {
          answerMax[index].list.push(orderList[j][k]);
        }
      } else {
        answerObject[index][orderList[j][k]] = 1;
      }
    }
  }

  for (const index in answerMax) {
    if (answerMax[index].list) answer.push(...answerMax[index].list);
  }

  return answer.sort();
}

console.log(
  solution(["ABCFG", "AC", "CDE", "ACDE", "BCFG", "ACDEH"], [2, 3, 4]),
);
console.log(
  solution(["ABCDE", "AB", "CD", "ADE", "XYZ", "XYZ", "ACD"], [2, 3, 5]),
);
console.log(solution(["XYZ", "XWY", "WXA"], [2, 3, 4]));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)
