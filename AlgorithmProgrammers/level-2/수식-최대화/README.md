## 수식 최대화

[2020 카카오 인턴십 > 수식 최대화](https://programmers.co.kr/learn/courses/30/lessons/67257)

``` js
function solution(expression) {
    let answer = 0;
    let numTemp = '';
    const numArr = [];
    const expArr = [];
    const expList = ['+', '-', '*'];

    const sol = (expList, expArr, numArr) => {
        for (let i = 0; i < expList.length; i++) {
            const sliceExpList = expList.slice();
            const sliceExpArr = expArr.slice();
            const sliceNumArr = numArr.slice();
            const nextExp = sliceExpList.splice(i, 1)[0];

            for (let j = 0; j < sliceExpArr.length; j++) {
                if (sliceExpArr[j] === nextExp) {
                    let resultNum = 0;
                    switch (nextExp) {
                        case '+':
                            resultNum = +sliceNumArr[j] + +sliceNumArr[j + 1];
                            break;
                        case '-':
                            resultNum = +sliceNumArr[j] - +sliceNumArr[j + 1];
                            break;
                        case '*':
                            resultNum = +sliceNumArr[j] * +sliceNumArr[j + 1];
                            break;
                    }
                    sliceNumArr.splice(j, 2, resultNum);
                    sliceExpArr.splice(j, 1);
                    j--;
                }
            }
            
            if (sliceExpList.length) {
                sol(sliceExpList, sliceExpArr, sliceNumArr);
            } else {
                const result = Math.abs(...sliceNumArr);
                if (result > answer) answer = result;
            }
        }
    };

    for (let i = 0; i < expression.length; i++) {
        if (expList.includes(expression[i])) {
            numArr.push(numTemp);
            expArr.push(expression[i]);
            numTemp = '';
        } else numTemp += expression[i];
    }
    numArr.push(numTemp);

    sol(expList, expArr, numArr);

    return answer;
}

console.log(solution('100-200*300-500+20'));
console.log(solution('50*6-3*2'));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/AlgorithmProgrammers)