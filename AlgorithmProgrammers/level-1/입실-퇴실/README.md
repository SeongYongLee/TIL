## 입실 퇴실

[위클리 챌린지 > 7주차 > 입실 퇴실](https://programmers.co.kr/learn/courses/30/lessons/86048)

``` js
// 1 - 잘못된 접근
// function solution(enter, leave) {
//     return enter
//         .reduce(
//             (answer, _, i) => {
//                 if (enter[i] === leave[0]) {
//                     const enterMeet = enter.slice(0, i + 1);

//                     for (let j = 0; j < enterMeet.length; j++) {
//                         const enterMeetSlice = enterMeet.slice();
//                         enterMeetSlice.splice(j, 1);
//                         enterMeetSlice.forEach((i) => answer[enterMeet[j] - 1].add(i));
//                     }
//                     console.log(...answer);
//                 }

//                 if (enter[leave.length - 1] === leave[enter.length - i - 1]) {
//                     const leaveMeet = leave.slice(-i - 1);

//                     for (let j = 0; j < leaveMeet.length; j++) {
//                         const leaveMeetSlice = leaveMeet.slice();
//                         leaveMeetSlice.splice(j, 1);
//                         leaveMeetSlice.forEach((i) => answer[leaveMeet[j] - 1].add(i));
//                     }
//                     console.log(...answer);
//                 }

//                 return answer;
//             },
//             new Array(enter.length).fill().map((_) => new Set()),
//         )
//         .map((a) => a.size);
// }

// 2
function solution(enter, leave) {
    const peopleLength = enter.length;
    const answer = Array(peopleLength).fill(0);
    const enterIndex = Array(peopleLength);
    const leaveIndex = Array(peopleLength);
    const addAnswer = (i, j) => {
        answer[i]++;
        answer[j]++;
    };

    for (let i = 0; i < peopleLength; i++) {
        enterIndex[enter[i] - 1] = i;
        leaveIndex[leave[i] - 1] = i;
    }

    for (let i = 0; i < peopleLength; i++) {
        for (let j = i + 1; j < peopleLength; j++) {
            // 두 비교 대상을 비교 한다.
            if (enterIndex[i] > enterIndex[j]) {
                // 들어오는 순서와 나가는 순서가 엇갈린 경우 무조건 만난다.
                if (leaveIndex[i] < leaveIndex[j]) {
                    addAnswer(i, j);
                } else {
                    // 들어오는 순서와 나가는 순서가 엇갈리지 않은 경우
                    // 먼저 나가야 할 사람들이 비교 대상보다 나중에 들어올 때 무조건 만난다.
                    for (let k = leaveIndex[j] - 1; k >= 0; k--) {
                        if (enterIndex[i] < enterIndex[leave[k] - 1]) {
                            addAnswer(i, j);
                            break;
                        }
                    }
                }
            } else {
                if (leaveIndex[i] > leaveIndex[j]) {
                    addAnswer(i, j);
                } else {
                    for (let k = leaveIndex[i] - 1; k >= 0; k--) {
                        if (enterIndex[j] < enterIndex[leave[k] - 1]) {
                            addAnswer(i, j);
                            break;
                        }
                    }
                }
            }
        }
    }
    return answer;
}

console.log(solution([1, 4, 2, 3], [2, 1, 3, 4]));
console.log(solution([1, 3, 2], [1, 2, 3]));
console.log(solution([3, 2, 1], [2, 1, 3]));
console.log(solution([3, 2, 1], [1, 3, 2]));
console.log(solution([1, 4, 2, 3], [2, 1, 4, 3]));
console.log(solution([1, 2, 3], [3, 2, 1]));
console.log(solution([1, 2, 3], [1, 2, 3]));
console.log(solution([1, 2, 3, 4], [3, 4, 2, 1]));
console.log(solution([1, 4, 5, 3, 2], [5, 4, 3, 2, 1])); // [4, 1, 1, 2, 2]
console.log(solution([1, 10, 9, 2, 3, 8, 7, 4, 5, 6], [10, 9, 8, 7, 6, 5, 4, 3, 2, 1])); // [9, 7, 7, 5, 5, 5, 3, 3, 1, 1]
console.log(solution([1, 2, 3, 4], [4, 2, 1, 3])); // [3, 3, 3, 3]
console.log(solution([1, 2, 3, 4, 5], [5, 3, 1, 2, 4])); // [4, 4, 4, 4, 4]
console.log(solution([1, 3, 2, 4, 6, 5, 8, 7, 9, 10], [9, 5, 1, 10, 7, 4, 8, 6, 2, 3])); // [8, 9, 9, 9, 8, 9, 9, 9, 8, 6]
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)