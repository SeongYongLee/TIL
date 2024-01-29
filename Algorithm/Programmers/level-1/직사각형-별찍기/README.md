## 직사각형 별찍기

[연습문제 > 직사각형 별찍기](https://programmers.co.kr/learn/courses/30/lessons/12969)

``` js
/* 
    Use Node.js!!
*/
process.stdin.setEncoding('utf8');
process.stdin.on('data', data => {
    const dataSplit = data.split(" ");
    const row = '*'.repeat(+dataSplit[0]);
    const rowCount = +dataSplit[1];
    
    for (let i = 0; i < rowCount; i++) {
        console.log(row);
    }
});

// input : '5 3'
// input : '2 2'
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)