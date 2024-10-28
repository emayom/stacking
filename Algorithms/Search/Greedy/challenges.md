#### TOC
1. [체육복](#체육복)
1. [조이스틱](#조이스틱)
1. [큰 수 만들기](#큰-수-만들기)
1. [구명보트](#구명보트)

## [체육복](https://school.programmers.co.kr/learn/courses/30/lessons/42862)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Level 1-blue" alt="Level 1"/> <img src="https://img.shields.io/badge/-Greedy-red" alt="Greedy"/> 

```js
// Set 자료구조 활용
function solution(n, lost, reserve) {
    const r_set = new Set(reserve);
    
    return n - lost.sort((a,b)=> a-b)
                    .filter(v => !r_set.delete(v))   
                    .filter(v => !r_set.delete(v-1) && !r_set.delete(v+1)).length;
}

// 배열 활용 
function solution(n, lost, reserve) {
    const students = Array.from({length: n}).fill(1);

    const haveExtra = (n) => {
        if(students[n-1] > 0) return true;
        else {
            students[n-1] = 1;  // 여벌 체육복이 있지만, 도난당한 학생 → 제외
            return false;
        }
    }
    
    const lend = (n) => {
        if(students[n-2] < 0) students[n-2] = 1;
        else if(students[n] < 0) students[n] = 1;
    }
    
    // 체육복을 도난당한 학생
    lost.forEach(number => students[number-1] = -1);
   
    reserve.sort((a,b)=> a-b)  // 오름차순 정렬
            .filter(haveExtra)   // 여벌 체육복이 있고, 체육복을 도난당하지 않은 학생 필터링 
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

체육복 문제는 **아래의 조건을 만족하며 <u>최대한 많은</u> 학생들이 체육 수업에 참여하도록 체육복을 대여하는 것**이 목표이며,  
입력 크기의 크기는 2 이상 30 이하로 시간 복잡도나 공간 복잡도는 상대적으로 풀이에 중요한 요소가 아니라는 점을 유추할 수 있다.  

1. 여벌 체육복이 있는 학생은 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있으며, 
2. 여벌 체육복을 가져온 학생이 체육복을 도난당했을 경우 체육복을 빌려줄 수 없다.

잘못된 대여를 방지하기 위해서는 `reserve(여벌 체육복을 가져온 학생)`으로부터 대여를 할 수 없는 학생 제거하는 것은 반드시 바로 앞 번호의 학생이나 바로 뒷번호의 학생에게 체육복을 빌려주는 선택 이전에 실행되어야 하는데 이를 통해 대여가 가능한 학생들만 남겨지게 되고, 이후의 대여 과정에서 선택의 유효성을 보장할 수 있다. 

또한, 정렬을 통해 대여 선택의 우선순위를 부여하는 것이 중요하다. 예를 들어, `[2, 4]`번 학생이 체육복을 도난당하고, `[3, 1, 5]`번 학생이 여벌 체육복을 가지고 있는 경우를 떠올려보자 정렬이 되지 않은 상태에서 탐욕적 선택을 시도한다면 2번 학생이 먼저 3번 학생에게 대여를 요청하게 되어 4번 학생이 체육복을 대여할 수 있는 기회를 놓칠 수 있다. 이때 정렬을 통해 번호 순으로 대여를 진행하면, 각 학생이 대여할 수 있는 체육복의 최대한을 확보할 수 있어 부분의 최적 해가 전체의 최적 해로 이어질 수 있다. 

의사 코드로 나타내면 다음과 같다. 

- **정렬을 통해 선택의 순차성 보장** 
- `reserve(여벌 체육복을 가져온 학생)` 배열으로부터 대여를 할 수 없는 학생 제거
- 바로 앞번호나 바로 뒷번호의 학생 중 가능한 학생에게 빌려주는 선택을 반복
    - `오름차순`의 경우: 바로 앞번호에게 먼저 대여 없으면 바로 뒷번호에게 대여
    - `내림차순`의 경우: 뒷번호에게 먼저 대여 없으면 바로 앞번호에게 대여

## [조이스틱](https://school.programmers.co.kr/learn/courses/30/lessons/42860)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Level 2-green" alt="Level 2"/>  <img src="https://img.shields.io/badge/-Greedy-red" alt="Greedy"/> 

```js
function solution(name) {
    const A = 'A'.charCodeAt();
    const Z = 'Z'.charCodeAt();
    
    const n = name.length;

    const { total, move } = [...name].reduce((acc, current, i) => {
        let next = i + 1;
        
        while (next < n && name[next] === 'A') next++;
        
        // 1. 커서 조작 
        const move = Math.min(
            acc.move,           // 1-1. 좌우 단방향(initial)    
            i * 2 + (n - next), // 1-2. 우측 → 좌측 → 좌측 
            (n - next) * 2 + i  // 1-3. 좌측 → 좌측 → 우측
        )
        
        // 2. 알파벳 조작
        const total =  acc.total + Math.min(
            current.charCodeAt() - A,       // 2-1. A → to
            1 + Z - current.charCodeAt(),   // 2-2. A → Z(via) → to
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

## [큰 수 만들기](https://school.programmers.co.kr/learn/courses/30/lessons/42883)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Level 2-green" alt="Level 2"/> <img src="https://img.shields.io/badge/-Greedy-red" alt="Greedy"/> 

```js
function solution(number, k) {
    const stack = [];
    const idx = [...number].findIndex(current => {
        if(k === 0) return true;    // 얼리 리턴
        
        while(stack.length && stack.at(-1) < current && 0 < k){
            stack.pop();
            k--;
        }
        
        stack.push(current);
    });
  
    // 얼리 리턴 되었다면
    if(idx > -1) return stack.join('') + number.slice(idx);
    
    return stack.slice(0, number.length - k).join('');
}
```

##### Review 

```
제한 조건
- number는 2자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 number의 자릿수 미만인 자연수입니다.
```

## [구명보트](https://school.programmers.co.kr/learn/courses/30/lessons/42885)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Level 2-green" alt="Level 2"/> <img src="https://img.shields.io/badge/-Greedy-red" alt="Greedy"/> 

```js
function solution(people, limit) {
    let cnt = 0;
    
    people.sort((a,b)=> b-a);

    for(let i = 0; i < people.length; i++){    
        if(people[i] < limit && i < people.length-1 && people[i] + people.at(-1) <= limit){
            people.pop();
        } 
        cnt++;
    }
    
    return cnt;
}
```

##### Review 

```
제한사항
- 무인도에 갇힌 사람은 1명 이상 50,000명 이하입니다.
- 각 사람의 몸무게는 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 항상 사람들의 몸무게 중 최댓값보다 크게 주어지므로 사람들을 구출할 수 없는 경우는 없습니다.
```
