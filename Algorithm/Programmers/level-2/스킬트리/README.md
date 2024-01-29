## 스킬트리

[Summer/Winter Coding(~2018) > 스킬트리](https://programmers.co.kr/learn/courses/30/lessons/49993)

``` js
function solution(skill, skill_trees) {
    const calc = (s) =>
        skill.indexOf(
            s
                .split('')
                .filter((x) => skill.indexOf(x) !== -1)
                .join(''),
        ) === 0;

    return skill_trees.filter((s) => calc(s)).length;
}

console.log(solution('CBD', ['BACDE', 'CBADF', 'AECB', 'BDA']));
```

[뒤로](https://github.com/SeongYongLee/TIL/tree/main/Algorithm/Programmers)