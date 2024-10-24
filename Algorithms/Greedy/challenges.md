#### TOC
1. [체육복](#체육복)
1. [조이스틱](#조이스틱)

## [체육복](https://school.programmers.co.kr/learn/courses/30/lessons/42862)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Greedy-red" alt="Greedy"/> 

```js
// Set 자료구조 활용
function solution(n, lost, reserve) {
    if(!lost.length) return n;
    if(!reserve.length) return n - lost.length;

    const r_set = new Set(reserve);
    
    return n - lost.filter(v => !r_set.delete(v))
                    .sort((a,b)=> a-b)
                    .filter(v => !r_set.delete(v-1) && !r_set.delete(v+1)).length;
}

// 배열 활용 
function solution(n, lost, reserve) {
    if(!lost.length) return n;
    if(!reserve.length) return n - lost.length;
    
    const students = Array.from({length: n}).fill(1);

    const haveExtra = (n) => {
        if(students[n-1] > 0) return true;
        else {
            students[n-1] = 1;
            return false;
        }
    }
    
    const lend = (n) => {
        if(students[n-2] < 0) students[n-2] = 1;
        else if(students[n] < 0) students[n] = 1;
    }
    
    // 체육복을 도난당한 학생
    lost.forEach(number => students[number-1] = -1);
   
    reserve.filter(haveExtra)   // 여벌 체육복이 있고, 체육복을 도난당하지 않은 학생 
            .sort((a,b)=> a-b)  // 오름차순 정렬
            .forEach(lend);     // 바로 앞번호의 학생이나 바로 뒷번호의 학생에게 빌려줌
    
    return students.filter(number => number > 0).length;
}
```

##### Review 

```
제한사항
- 전체 학생의 수는 2명 이상 30명 이하입니다.
- 체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
- 여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
- 여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
- 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.
```

## [조이스틱](https://school.programmers.co.kr/learn/courses/30/lessons/42860)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Greedy-red" alt="Greedy"/> 

```js
function solution(name) {
    const A = 'A'.charCodeAt();
    const Z = 'Z'.charCodeAt();
    
    const n = name.length;

    const { total, move } = [...name].reduce((acc, current, i) => {
        let next = i + 1;
        
        while (next < n && name[next] === 'A') next++;
        
        // 커서 조작 
        const move = Math.min(
            acc.move,           // 좌우 단방향(initial)    
            i * 2 + (n - next), // 우측 -> 좌측 -> 좌측 
            (n - next) * 2 + i  // 좌측 -> 좌측 -> 우측
        )
        
        // 알파벳 조작
        const total =  acc.total + Math.min(
            current.charCodeAt() - A,       // A -> to
            1 + Z - current.charCodeAt(),   // A -> Z(via) -> to
        )
                
        return { total, move };
                                        
    }, { total: 0, move: n - 1 });
    
    return total + move;   
}
```

##### Review 

```
제한 사항
- name은 알파벳 대문자로만 이루어져 있습니다.
- name의 길이는 1 이상 20 이하입니다.
```
