# 동적 계획법(Dynamic Programming, DP)
> 일반적인 프로그래밍 분야에서의 동적(Dynamic)과는 그 의미가 다르다. 

동적 계획법은 복잡한 문제를 여러 개의 작은 하위 문제로 나누어 해결하는 알고리즘 설계 기법의 한 갈래로,  
**각 하위 문제의 계산 결과를 저장하고, 동일한 부분 문제가 반복될 때 그 값을 재사용함으로써 전체 문제의 수행 시간을 단축**시킨다. 

특히, **최적화 문제**(조건을 만족하는 여러 해 중 최적의 해를 찾는 문제)에서 완전 탐색이나 DFS/BFS와 같은 방법을 사용할 경우 **불필요한 중복된 연산**이 발생할 수 있는데, 이때 동적 계획법을 사용하면 메모리를 적절히 활용하여 중복 계산을 방지하고, 수행 시간을 크게 단축시켜 문제를 효율적으로 해결할 수 있다.

#### 동적 계획법 특징 
- 분할정복(Divide and Conquer) + 중복 계산 최소화  
    - Memoization 방식 
    - Tabulation 방식 

## 동적 계획법의 구현
- 하향식(Top-Down) 접근법
- 상향식(Bottom-Up) 접근법

### 하향식(Top-Down) 접근법 (Memoization 방식)

하향식 접근법은 문제를 해결하기 위해 **상위 문제에서 시작해서 하위 문제로 내려가며 해결**하는 방식으로, **재귀**를 사용하여 구현한다.  
계산된 결과는 **메모이제이션(Memoization)** 기법을 사용하여 저장하고, 저장된 결과는 이후 중복 계산을 방지하기 위해 참조된다.

```js
function fibonacci(n, memo = []) {
    if (n < 2) return memo[n] = n;
    if (memo[n]) return memo[n]; // ✅ Memoization
    
    return memo[n] = fibonacci(n-1, memo) + fibonacci(n-2, memo);
}
```

### 상향식(Bottom-Up) 접근법 (Tabulation 방식) 
> Tabulation 방식이라고 부르는 이유는 반복을 통해 테이블의 처음부터 마지막까지 채우는 과정을 “table-filling” 이라고 부르기 때문이다.

상향식 접근법은 문제를 해결하기 위해 **하위 문제부터 차례대로 해결하며 점차 상위 문제를 해결**하는 방식으로, **반복문**을 사용하여 구현한다.  
계산된 결과는 **테뷸레이션(Tabulation)** 기법을 사용하여 테이블에 저장되며, 중복 계산을 방지하며 상위 문제를 해결하는 데 참조된다.

```js
function fibonacci(n) {
    const table = new Array(n+1).fill(0);
    
    table[1] = 1;
    
    for (let i = 2; i <= n; i++) {
		table[i] = table[i-1] + table[i-2];
	}
    
    return table[n];
}
```
