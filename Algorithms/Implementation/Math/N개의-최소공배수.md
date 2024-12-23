---
title: 프로그래머스 - N개의 최소공배수
category: Algorithms
tags:
  - Algorithms
  - Implementation
  - Math
last_modified_at: '2024-12-23T15:32:15.158Z'
date: '2024-12-23T15:32:15.158Z'
---

# N개의 최소공배수

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Level 2-green" alt="Level 2"/> <img src="https://img.shields.io/badge/-Math-rosybrown" alt="Math"/> 

- [문제 풀러 가기](https://school.programmers.co.kr/learn/courses/30/lessons/12953)

### 풀이 1: 유클리드 호제법

```js
function solution(arr) {
    function gcd(a, b){
        let c;
        while(b){
            c = a % b;
            a = b;
            b = c;
        }
        return a;
    }
    
    function lcm(a, b){
        return (a * b) / gcd(a, b);
    }
    
    // ✅ initialValue를 제공하지 않으면 배열의 첫 번째 요소를 사용
    return arr.reduce((a, b) => lcm(a, b));
}
```

### 풀이 2: 브루트 포스
> - 1 ≤ `arr.length` ≤ 15 
> - 1 ≤ `arr[i]` ≤ 100

```js
function solution(arr) {
    function gcd(a, b){
        let _gcd = 0;

        for(let i = 1; i <= Math.min(a, b); i++){
            if(a % i === 0 && b % i === 0){
                _gcd = i;
            }
        }

        return _gcd;
    }
    
    function lcm(a, b){
        return (a * b) / gcd(a, b);
    }
    
    // 최악의 경우 O(15 * 100)
    return arr.reduce((a, b) => lcm(a, b));
}
```
