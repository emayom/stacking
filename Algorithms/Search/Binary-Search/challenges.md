#### TOC
1. [입국심사](#입국심사)
1. [금과 은 운반하기](#금과-은-운반하기)

## [입국심사](#입국심사)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Level 3-orange" alt="Level 3"/> <img src="https://img.shields.io/badge/-Binary Search-mediumseagreen" alt="Binary Search"/> 

```js
function solution(n, times) {
    let answer;
    let left = 1;
    let right = Math.max(...times) * n; // 최대 10^18
   
   // O(log(10^18))
    while(left <= right){
        const mid = Math.floor((left+right)/2); // 범위를 반으로 줄여가며 이분탐색 
        const people = times.reduce((acc, time) => acc += Math.floor(mid/time), 0); // 루프 당 𝑂(𝑚) 연산 (최대 10^5)
        
        if(people >= n){
            answer = mid;
            right = mid-1; 
        } else if(people < n) {
            left = mid+1;
        }
    }

    return answer;
}
```

##### Review 

```
제한사항
- 입국심사를 기다리는 사람은 1명 이상 1,000,000,000명 이하입니다.
- 각 심사관이 한 명을 심사하는데 걸리는 시간은 1분 이상 1,000,000,000분 이하입니다.
- 심사관은 1명 이상 100,000명 이하입니다.
```

## [금과 은 운반하기](https://school.programmers.co.kr/learn/courses/30/lessons/86053)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Level 3-orange" alt="Level 3"/> <img src="https://img.shields.io/badge/-Binary Search-mediumseagreen" alt="Binary Search"/> 

```js
function solution(a, b, g, s, w, t) {
    let answer;
    let left = 0;    
    // 최대 값 추정 
    // 전달 총량(최대 10^9) / 가장 낮은 적재 중량(최소 1) * 편도 이동 시간(최대 10^5) * 2
    let right = Math.ceil((a + b) / Math.min(...w)) * 2 * Math.max(...t);
    
    while(left <= right){
        let total = 0, golds = 0, silvers = 0;
        const mid = Math.floor((left + right) / 2);
        
        t.forEach((time, i) => {
            const cnt = Math.floor((mid + time) / (2 * time));    
            const amount = Math.min(cnt * w[i], g[i] + s[i]);
                                     
            total += amount;
            golds += Math.min(amount, g[i]); 
            silvers += Math.min(amount, s[i]);
        });
        
        if(total >= a + b && golds >= a && silvers >= b){
            answer = mid;
            right = mid-1; 
        } else {
            left = mid+1;
        }
    }
    
    return answer;
}
```

##### Review 

```
제한사항
- 0 ≤ a, b ≤ 109
- 1 ≤ g의 길이 = s의 길이 = w의 길이 = t의 길이 = 도시 개수 ≤ 105
    - 0 ≤ g[i], s[i] ≤ 109
    - 1 ≤ w[i] ≤ 102
    - 1 ≤ t[i] ≤ 105
    - a ≤ g의 모든 수의 합
    - b ≤ s의 모든 수의 합
```
