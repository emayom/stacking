#### TOC
1. [체육복](#뒤에-있는-큰-수-찾기)

## [체육복](https://school.programmers.co.kr/learn/courses/30/lessons/42862)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Greedy-red" alt="Greedy"/> 

```js
function solution(n, lost, reserve) {
    if(!lost.length) return n;
    if(!reserve.length) return n - lost.length;

    const r_set = new Set(reserve);
    const filtered = lost.filter(v => !r_set.delete(v)).sort((a,b)=> a-b);
    
    return n - filtered.filter(v => !r_set.delete(v-1) && !r_set.delete(v+1)).length;
}
```
