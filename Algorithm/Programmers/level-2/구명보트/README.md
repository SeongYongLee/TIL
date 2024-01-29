## 구명보트

[탐욕법(Greedy) > 구명보트](https://programmers.co.kr/learn/courses/30/lessons/42885)

``` js
// 1
// function solution(people, limit) {
//     let answer = 0;
//     let pLength = people.length;

//     people.sort((a, b) => b - a);

//     while (pLength > 1) {
//         if (people[0] <= limit / 2) return answer + Math.round(pLength / 2);

//         if (people[0] + people[pLength - 1] > limit) {
//             pLength--;
//         } else {
//             people.pop();
//             pLength -= 2;
//         }

//         people.shift();
//         answer++;
//     }

//     return pLength === 1 ? ++answer : answer;
// }

// 2
// function solution(people, limit) {
//     let first = 0;
//     let pLength = people.length - 1;

//     people.sort((a, b) => b - a);

//     while (first <= pLength) {
//         if (people[first] <= limit / 2)
//             return first + Math.round((pLength - first + 1) / 2);

//         if (people[first] + people[pLength] <= limit) pLength--;

//         first++;
//     }

//     return first;
// }

// 3
function solution(people, limit) {
    let answer = -1;
    let pLength = people.length - 1;

    people.sort((a, b) => b - a);

    while (++answer <= pLength) {
        if (people[answer] <= limit / 2)
            return answer + Math.round((pLength - answer + 1) / 2);

        if (people[answer] + people[pLength] <= limit) pLength--;
    }

    return answer;
}

console.log(solution([70, 50, 80, 50], 100));
console.log(solution([70, 80, 50], 100));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)