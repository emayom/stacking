---
title: 프로그래머스 - JadenCase 문자열 만들기
category: Algorithms
tags:
  - Algorithms
  - Implementation
  - String
last_modified_at: '2024-12-23T18:55:54.725Z'
date: '2024-12-23T18:55:54.725Z'
---

# JadenCase 문자열 만들기

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Level 2-green" alt="Level 2"/> <img src="https://img.shields.io/badge/-String-dimgray" alt="String"/> 

- [문제 풀러 가기](https://school.programmers.co.kr/learn/courses/30/lessons/12951)

### 풀이 1: 정규 표현식 

```js
function solution(s) {
    // \b: 단어의 시작 또는 끝을 나타내는 경계
    // \w: 알파벳, 숫자, 밑줄 등으로 구성된 단어 문자
    const re = /\b\w/g;

    return s.toLowerCase()
            .replace(re, char => char.toUpperCase());
}
```

#### 응용: 모든 단어의 마지막 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열

```js
function solution(s) {
    // \b: 단어의 시작 또는 끝을 나타내는 경계
    // \w: 알파벳, 숫자, 밑줄 등으로 구성된 단어 문자
    const re = /\w\b/g;

    // 혹은 
    // (?=\b): 긍정형 전방탐색(positive lookahead)
    // const re = /\w(?=\b)/g;

    return s.toLowerCase()
            .replace(re, char => char.toUpperCase());
}
```

### 풀이 2: 스택 활용 
```js
function solution(s) {
    s = s.toLowerCase();

    const stack = [];
    const space = ' ';
    
    for(let i = 0; i < s.length; i++){
        let char = s[i];
        
        if(!stack.length || stack.at(-1) === space && char !== space){
            char = char.toUpperCase();
        } 
        
        stack.push(char);
    }
    
    return stack.join('');
}
```
