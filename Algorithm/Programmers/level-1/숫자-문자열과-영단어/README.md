## 숫자 문자열과 영단어

* [2021 카카오 채용연계형 인턴십 > 숫자 문자열과 영단어](https://programmers.co.kr/learn/courses/30/lessons/81301)

``` js
// 1
// function solution(s) {
//     const strList = [
//         'zero',
//         'one',
//         'two',
//         'three',
//         'four',
//         'five',
//         'six',
//         'seven',
//         'eight',
//         'nine',
//     ];
//     let remainList = strList.slice();
//     let remainIndex = 0;
//     let answer = '';

//     for (let i = 0; i < s.length; i++) {
//         if (Number.isInteger(+s[i])) {
//             answer += s[i];
//         } else {
//             remainList = remainList.filter((list) => list[remainIndex] === s[i]);
//             if (remainList.length === 1) {
//                 answer += strList.indexOf(remainList[0]);
//                 i += remainList[0].length - remainIndex - 1;
//                 remainList = strList.slice();
//                 remainIndex = 0;
//             } else {
//                 remainIndex++;
//             }
//         }
//     }

//     return +answer;
// }

// 2 - Refactoring
function solution(s) {
    const numbers = [
        'zero',
        'one',
        'two',
        'three',
        'four',
        'five',
        'six',
        'seven',
        'eight',
        'nine',
    ];
    let answer = s;

    for (let i = 0; i < numbers.length; i++) {
        answer = answer.split(numbers[i]).join(i);
    }

    return +answer;
}

console.log(solution('one4seveneight'));
console.log(solution('23four5six7'));
console.log(solution('2three45sixseven'));
console.log(solution('123'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)