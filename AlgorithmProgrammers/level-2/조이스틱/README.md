## 조이스틱

[탐욕법(Greedy) > 조이스틱](https://programmers.co.kr/learn/courses/30/lessons/42860)

``` js
function solution(name) {
    const nameLength = name.length;
    const engArray = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 
    'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'];
    const nameArray = name.split('');
    let answer = Infinity;

    getAnswer(Array(nameLength).fill('A'), 0, 0);

    function getAnswer(currentArray, index, total) {
        if (total > answer) return;

        let endCount = 0;

        for (let i = 0; i < nameLength; i++) {
            if (nameArray[i] !== currentArray[i]) {
                const temp = currentArray.slice();
                const distEng =
                    engArray.indexOf(nameArray[i]) - engArray.indexOf(temp[i]);
                const distIndex = Math.abs(i - index);

                temp[i] = nameArray[i];

                getAnswer(
                    temp,
                    i,
                    total +
                        (distEng > 13 ? 26 - distEng : distEng) +
                        (distIndex > nameLength / 2
                            ? nameLength - distIndex
                            : distIndex)
                );
            } else endCount++;
        }

        if (endCount === nameLength) {
            if (answer > total) answer = total;
            return;
        }
    }
    return answer;
}

console.log(solution('JEROEN'));
console.log(solution('JAN'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)