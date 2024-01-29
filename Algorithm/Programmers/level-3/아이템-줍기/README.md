## 아이템 줍기

[위클리 챌린지 > 11주차 > 아이템 줍기](https://programmers.co.kr/learn/courses/30/lessons/84021)

``` js
// 1 - 테스트 케이스 빗나감
// function solution(rectangle, characterX, characterY, itemX, itemY) {
//     const box = Array(51)
//         .fill()
//         .map((_) => Array(51).fill(0));

//     for (let i = 0; i < rectangle.length; i++) {
//         for (let j = rectangle[i][0] + 1; j < rectangle[i][2]; j++) {
//             for (let k = rectangle[i][1] + 1; k < rectangle[i][3]; k++) {
//                 box[k][j] = 2;
//             }
//         }
//         box[rectangle[i][1]][rectangle[i][0]] =
//             box[rectangle[i][1]][rectangle[i][0]] > 1
//                 ? box[rectangle[i][1]][rectangle[i][0]]
//                 : 1;
//         box[rectangle[i][3]][rectangle[i][0]] =
//             box[rectangle[i][3]][rectangle[i][0]] > 1
//                 ? box[rectangle[i][3]][rectangle[i][0]]
//                 : 1;
//         box[rectangle[i][1]][rectangle[i][2]] =
//             box[rectangle[i][1]][rectangle[i][2]] > 1
//                 ? box[rectangle[i][1]][rectangle[i][2]]
//                 : 1;
//         box[rectangle[i][3]][rectangle[i][2]] =
//             box[rectangle[i][3]][rectangle[i][2]] > 1
//                 ? box[rectangle[i][3]][rectangle[i][2]]
//                 : 1;
//     }

//     console.table(box);
//     console.log(box[characterY][characterX]);

//     let lotation = -1; // ['left', 'right', 'top', 'bottom'];
//     const move = [
//         [0, -1],
//         [0, 1],
//         [1, 0],
//         [-1, 0],
//     ];
//     const nextLotation = [2, 3, 1, 0];
//     const blockLotation = [3, 2, 0, 1];

//     if (box[characterY - 1][characterX] === 2) {
//         lotation = 0;
//     }
//     if (box[characterY + 1][characterX] === 2) {
//         lotation = 1;
//     }
//     if (box[characterY][characterX + 1] === 2) {
//         lotation = 2;
//     }
//     if (box[characterY][characterX - 1] === 2) {
//         lotation = 3;
//     }
//     if (box[characterY - 1][characterX - 1] === 2) {
//         lotation = 3;
//     }

//     if (box[characterY - 1][characterX + 1] === 2) {
//         lotation = 1;
//     }

//     if (box[characterY + 1][characterX + 1] === 2) {
//         lotation = 2;
//     }

//     if (box[characterY + 1][characterX - 1] === 2) {
//         lotation = 0;
//     }

//     let count = 0;

//     while (++count) {
//         console.log(count, lotation, characterY, characterX);
//         characterY += move[lotation][0];
//         characterX += move[lotation][1];

//         if (box[characterY][characterX] === 2) {
//             characterY -= move[lotation][0];
//             characterX -= move[lotation][1];
//             count--;
//             lotation = blockLotation[lotation];
//         } else if (box[characterY][characterX] === 1) {
//             lotation = nextLotation[lotation];
//         }

//         if (itemX === characterX && itemY === characterY) break;
//     }

//     console.log(count);

//     var answer = 0;

//     return answer;
// }

// 2 - 테스트 케이스 한 번 더 빗나감
// function solution(rectangle, characterX, characterY, itemX, itemY) {
//     const lineBox = Array(51)
//         .fill()
//         .map((_) => Array(51).fill(0));

//     for (let i = 0; i < rectangle.length; i++) {
//         for (let j = rectangle[i][0] + 1; j < rectangle[i][2]; j++) {
//             lineBox[rectangle[i][1]][j] =
//                 lineBox[rectangle[i][1]][j] === 2 ? 3 : 2;
//             lineBox[rectangle[i][3]][j] =
//                 lineBox[rectangle[i][3]][j] === 2 ? 3 : 2;
//         }
//         for (let j = rectangle[i][1] + 1; j < rectangle[i][3]; j++) {
//             lineBox[j][rectangle[i][0]] =
//                 lineBox[j][rectangle[i][0]] === 2 ? 3 : 2;
//             lineBox[j][rectangle[i][2]] =
//                 lineBox[j][rectangle[i][2]] === 2 ? 3 : 2;
//         }
//         lineBox[rectangle[i][1]][rectangle[i][0]] = 1;
//         lineBox[rectangle[i][3]][rectangle[i][0]] = 1;
//         lineBox[rectangle[i][1]][rectangle[i][2]] = 1;
//         lineBox[rectangle[i][3]][rectangle[i][2]] = 1;
//     }

//     const move = [
//         [0, -1],
//         [0, 1],
//         [1, 0],
//         [-1, 0],
//     ];
//     const nextLotation = [2, 3, 1, 0];
//     const blockLotation = [3, 2, 0, 1];
//     let total = 0;
//     let answer = 0;

//     console.table(lineBox);

//     outer: for (let i = 0; i < 4; i++) {
//         let count = 0;
//         let lotation = i; // ['left', 'right', 'top', 'bottom'];
//         let y = characterY;
//         let x = characterX;

//         while (++count) {
//             y += move[lotation][0];
//             x += move[lotation][1];

//             if (!lineBox[y] || !lineBox[y][x]) continue outer;

//             if (lineBox[y][x] === 3) {
//                 lotation = blockLotation[lotation];
//             } else if (lineBox[y][x] === 1) {
//                 lotation = nextLotation[lotation];
//             }

//             if (itemX === x && itemY === y) answer = count;
//             if (characterX === x && characterY === y) {
//                 total = count;
//                 break outer;
//             }
//         }
//     }

//     return total - answer < answer ? total - answer : answer;
// }

// 3
function solution(rectangle, characterX, characterY, itemX, itemY) {
    const box = Array(51)
        .fill()
        .map((_) => Array(51).fill());

    for (let i = 0; i < rectangle.length; i++) {
        for (let j = rectangle[i][0] + 1; j < rectangle[i][2]; j++) {
            box[rectangle[i][1]][j] = box[rectangle[i][1]][j] === 3 ? 3 : 1;
            box[rectangle[i][3]][j] = box[rectangle[i][3]][j] === 2 ? 2 : 0;
        }
        for (let j = rectangle[i][1] + 1; j < rectangle[i][3]; j++) {
            box[j][rectangle[i][0]] = box[j][rectangle[i][0]] === 0 ? 0 : 3;
            box[j][rectangle[i][2]] = box[j][rectangle[i][2]] === 1 ? 1 : 2;
        }
        box[rectangle[i][1]][rectangle[i][0]] = 1;
        box[rectangle[i][3]][rectangle[i][0]] = 3;
        box[rectangle[i][1]][rectangle[i][2]] = 2;
        box[rectangle[i][3]][rectangle[i][2]] = 0;
    }

    const move = [
        [0, -1],
        [0, 1],
        [1, 0],
        [-1, 0],
    ]; // ['left', 'right', 'top', 'bottom'];
    let total = 0;
    let answer = 0;
    let y = characterY;
    let x = characterX;
    let count = 0;

    while (++count) {
        const lotation = box[y][x];
        y += move[lotation][0];
        x += move[lotation][1];

        if (itemX === x && itemY === y) answer = count;
        if (characterX === x && characterY === y) {
            total = count;
            break;
        }
    }

    return total - answer < answer ? total - answer : answer;
}

console.log(
    solution(
        [
            [1, 1, 7, 4],
            [3, 2, 5, 5],
            [4, 3, 6, 9],
            [2, 6, 8, 8],
        ],
        1,
        3,
        7,
        8
    )
);

console.log(
    solution(
        [
            [1, 1, 8, 4],
            [2, 2, 4, 9],
            [3, 6, 9, 8],
            [6, 3, 7, 7],
        ],
        9,
        7,
        6,
        1
    )
);
console.log(solution([[1, 1, 5, 7]], 1, 1, 4, 7));
console.log(
    solution(
        [
            [2, 1, 7, 5],
            [6, 4, 10, 10],
        ],
        3,
        1,
        7,
        10
    )
);
console.log(
    solution(
        [
            [2, 2, 5, 5],
            [1, 3, 6, 4],
            [3, 1, 4, 6],
        ],
        1,
        4,
        6,
        3
    )
);
console.log(
    solution(
        [
            [1, 1, 3, 7],
            [2, 2, 7, 4],
            [4, 3, 6, 6],
        ],
        1,
        2,
        6,
        6
    )
);

console.log(
    solution(
        [
            [1, 1, 4, 4],
            [2, 2, 5, 5],
            [3, 3, 7, 8],
        ],
        1,
        1,
        5,
        3
    )
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)