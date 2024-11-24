---
title: "2022 KAKAO BLIND RECRUITMENT - k진수에서 소수 개수 구하기"
category: "Algorithms"
tags: ["Algorithms", "Implementation", "String", "2022 KAKAO BLIND RECRUITMENT"]
date: 2024-11-23
last_modified_at: 2024-11-23
---

# k진수에서 소수 개수 구하기

<img src="https://img.shields.io/badge/-2022 KAKAO BLIND RECRUITMENT-gold" alt="2022 KAKAO BLIND RECRUITMENT"/> <img src="https://img.shields.io/badge/-Level 2-green" alt="Level 2"/> <img src="https://img.shields.io/badge/-String-dimgray" alt="String"/> 

- [문제 풀러 가기](https://school.programmers.co.kr/learn/courses/30/lessons/92335)

### 풀이 1: 제곱근을 활용한 소수 판별법

```js
function solution(n, k) {
    function isPrimeNumber(n){
        if(n < 2) return false;
        
        let divisor = Math.floor(Math.sqrt(n));
        
        while(divisor > 1){
            if(n % divisor === 0) return false;
            divisor--;
        }
        
        return true;
    }

    const converted = n.toString(k);
    const prime_numbers = converted.split('0').filter(isPrimeNumber);

    return prime_numbers.length;
}
```


### 풀이 2: 에라토스테네스의 체 → 88.1 / 100.0 (테스트 1 실패 ❌)

```js
function solution(n, k) {
    const converted = n.toString(k);
    const sqrt = Math.floor(Math.sqrt(n));
    
    const prime_array = new Array(n + 1).fill(true).fill(false, 0, 2);
    
    for(let i = 0; i <= sqrt; i++){
        if(prime_array[i]){
            for(let j = i * i; j <= n; j += i) {
                prime_array[j] = false;
            } 
        }
    }

    return converted.split(0).filter(n => prime_array[n]).length;
}
```

### 풀이 3: 에라토스테네스의 체 + 제곱근을 활용한 소수 판별법

```js
function solution(n, k) {
    const converted = n.toString(k);
    const sqrt = Math.floor(Math.sqrt(n));
    
    // 에라토스테네스의 체
    const prime_array = new Array(n + 1).fill(true).fill(false, 0, 2);
    
    for(let i = 0; i <= sqrt; i++){
        if(prime_array[i]){
            for(let j = i * i; j <= n; j += i) {
                prime_array[j] = false;
            } 
        }
    }
    
    // 제곱근을 활용한 소수 판별법
    function isPrimeNumber(n){
        if(n < 2) return false;
        
        const sqrt = Math.floor(Math.sqrt(n));

        for(let i = 2; i <= sqrt; i++) {
            if(n % i === 0) return false;
        }
        
        return true;
    }

    return converted.split('0')
                    .filter(v => parseInt(v, 10) <= n ? prime_array[v] : isPrimeNumber(v))
                    .length;
}
```

[[참고] Algorithms/Basic/소수 판별법](../../Basic/소수-판별법.md)
