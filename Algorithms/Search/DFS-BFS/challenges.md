#### TOC
1. [타겟 넘버](#타겟-넘버)

## [타겟 넘버](https://school.programmers.co.kr/learn/courses/30/lessons/43165)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Level 2-green" alt="Level 2"/> <img src="https://img.shields.io/badge/-DFS-crimson" alt="DFS"/> 

```js
// 1. 이진 재귀 호출 → 모든 경로 탐색 
function solution(numbers, target) {
    let answer = 0;
    
    // O(2^n)
    function dfs(idx = 0, acc = 0){
        if(idx === numbers.length){
            if(acc === target) answer++;
            return; 
        }
        
        dfs(idx + 1, acc + numbers[idx]);   // 더하거나
        dfs(idx + 1, acc - numbers[idx]);   // 빼거나 
    }
    
    dfs();
    
    return answer;
}

// 2. 두 단계의 이진 재귀 호출 → 완전 이진 트리 생성, 각 경로에서 가능한 모든 값 계산
function solution(numbers, target) {
    const answer = [];
    const tree = {};
    
    function buildCBT(node = 0, idx = 0){
        if(idx === numbers.length) return;

        tree[node] = {
            left: numbers[idx],    
            right: -numbers[idx]   
        };

        buildCBT((node*2) + 1, idx + 1);   
        buildCBT((node*2) + 2, idx + 1);   
    }
    
    function dfs(node = 0, acc = 0){
        if(!tree[node]) return answer.push(acc);
        
        const { left, right } = tree[node];
        
        dfs((node*2) + 1, acc + left);  
        dfs((node*2) + 2, acc + right);   
    }
    
    buildCBT();
    dfs();

    return answer.filter(sum => sum === target).length;
}
```

```
제한사항
- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.
```