## 거리두기 확인하기

[2021 카카오 채용연계형 인턴십 > 거리두기 확인하기](https://programmers.co.kr/learn/courses/30/lessons/81302)

``` js
function solution(places) {
    const pLength = places[0].length;
    const nearP = (place, x, y) => {
        for (let i = x - 2 > 0 ? x - 2 : 0; i < (x + 3 < pLength ? x + 3 : pLength); i++) {
            const xAbs = Math.abs(x - i);
            for (
                let j = y - 2 + xAbs > 0 ? y - 2 + xAbs : 0;
                j < (y + 3 - xAbs < pLength ? y + 3 - xAbs : pLength);
                j++
            ) {
                if (place[i][j] === 'P' && !(x === i && y === j)) {
                    switch (xAbs) {
                        case 0:
                            if (Math.abs(y - j) === 1 || place[i][(y + j) / 2] !== 'X') return 1;
                            break;
                        case 2:
                            if (place[(x + i) / 2][j] !== 'X') return 1;
                            break;
                        case 1:
                            if (place[x][j] !== 'X' || place[i][y] !== 'X') return 1;
                            break;
                    }
                }
            }
        }
        return 0;
    };

    return places.map((place) => {
        for (let x = 0; x < pLength; x++) {
            const placeSplit = place[x].split('');
            for (let y = 0; y < pLength; y++) {
                if (placeSplit[y] === 'P') {
                    if (nearP(place, x, y)) return 0;
                    placeSplit[y] = 'O';
                    place[x] = placeSplit.join('');
                }
            }
        }
        return 1;
    });
}

console.log(
    solution([
        ['POOOP', 'OXXOX', 'OPXPX', 'OOXOX', 'POXXP'],
        ['POOPX', 'OXPXP', 'PXXXO', 'OXXXO', 'OOOPP'],
        ['PXOPX', 'OXOXP', 'OXPOX', 'OXXOP', 'PXPOX'],
        ['OOOXX', 'XOOOX', 'OOOXX', 'OXOOX', 'OOOOO'],
        ['PXPXP', 'XPXPX', 'PXPXP', 'XPXPX', 'PXPXP'],
    ])
);
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)