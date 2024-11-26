---
title: "2018 KAKAO BLIND RECRUITMENT - [3차] n진수 게임"
category: "Algorithms"
tags: ["Algorithms", "Implementation", "String", "2018 KAKAO BLIND RECRUITMENT"]
date: 2024-11-27
last_modified_at: 2024-11-27
---

# [3차] n진수 게임

<img src="https://img.shields.io/badge/-2018 KAKAO BLIND RECRUITMENT-gold" alt="2018 KAKAO BLIND RECRUITMENT"/> <img src="https://img.shields.io/badge/-Level 2-green" alt="Level 2"/> <img src="https://img.shields.io/badge/-String-dimgray" alt="String"/> 

- [문제 풀러 가기](https://school.programmers.co.kr/learn/courses/30/lessons/17687)

### 풀이 1:

```js
function solution(n, t, m, p) {
    let i = 0;
    let answer = '';    // 튜브가 말해야하는 숫자들
    let numbers = '';   // n진법 챔퍼나운 수
    
    while(numbers.length <= m * t){
        numbers += i.toString(n);
        i++;
    }
 
    for(let j = p - 1; j <= m * t - 1; j += m){
        answer += numbers[j];
    }
    
    // ✅ 기수 값(radix)이 10 이상의 값일 때, 9보다 큰 수 → 알파벳 소문자로 표현
    return answer.toUpperCase();
}
```

> [Number.prototype.toString()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number/toString)
> 
> 진수를 나타내는 기수 값(radix) 이 10 이상의 값일 때는, 알파벳의 글자는 9보다 큰 수를 나타냅니다. 예를 들면, 16진수(base 16)는, 알파벳 f 까지 사용하여 표현됩니다.

`toString()` 메소드는 10 이상의 숫자를 큰 수를 소문자 `a-f` 까지의 알파벳으로 표현한다.  
그러나 문제에서는 10 이상의 숫자를 대문자 `A-F`로 표현하도록 요구하므로, 대문자로 변환하는 추가 작업이 필요하다.
