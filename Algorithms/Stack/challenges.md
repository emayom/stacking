[프로그래머스 - 뒤에 있는 큰 수 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/154539)
```js
// 이중 for문 O(n²) → 실패(시간 초과) ❌
function solution(numbers) {
    const answer = [];
    const len = numbers.length;
    
    for(let i = 0; i < len; i++){
        for(let j = i + 1; j < len; j++){       
            if(numbers[i] < numbers[j]){
                answer.push(numbers[j])
                break;
            }
            
            if(j === len - 1){
                answer.push(-1);
            }   
        }
    }
    
    return [...answer, -1];
}

// 스택 활용 O(n)
function solution(numbers) {
    const answer = new Array(numbers.length).fill(-1);
    
    numbers.forEach((current, idx)=> {
        while(stack.length && numbers[stack.at(-1)] < current){
            answer[stack.pop()] = current;
        }
        
        stack.push(idx);
    });

    return answer;
}
```

##### Review 

```
제한 사항
- 4 ≤ numbers의 길이 ≤ 1,000,000
    - 1 ≤ numbers[i] ≤ 1,000,000
```

단순하게 떠올릴 수 있는 해결 방식은 이중 반복문으로 **뒷 큰수**를 찾기 위해, 각 원소에 대해 뒤에 있는 모든 원소들을 순차적으로 확인하는 `Brute Force` 방식이다. 하지만 이 경우 O(n²) 시간 복잡도로 배열의 길이가 최대 1,000,000까지 주어지는 `numbers` 배열에서는 1,000,000²(1조)번의 연산을 수행하게 되며 시간 초과가 발생할 가능성이 크다. 

첫번째 풀이에서 이중 반복문을 사용한 이유는 각 원소(`numbers[i]`)와 그 이후 원소들(`numbers[j]`)을 구분하여 이전 값과 순차적으로 비교하기 위함이지만, 불필요한 중복 비교가 발생한다. 이 경우 **스택 자료 구조**를 사용하면 원소를 순차적으로 처리하면서도, 이전에 처리된 값들과 효율적으로 비교할 수 있어 동일한 목적을 달성하면서도 시간 복잡도는 O(n)으로 개선할 수 있다.  

##### 관련 문제 
- [백준 - 오큰수](https://www.acmicpc.net/problem/17298)
- [백준 - 히스토그램에서 가장 큰 직사각형](https://www.acmicpc.net/problem/6549)
