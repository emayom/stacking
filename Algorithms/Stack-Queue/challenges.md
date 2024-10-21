#### TOC
1. [뒤에 있는 큰 수 찾기](#뒤에-있는-큰-수-찾기)
1. [올바른 괄호](#올바른-괄호)
1. [주식가격](#주식가격)
1. [다리를 지나는 트럭](#다리를-지나는-트럭)

## [뒤에 있는 큰 수 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/154539)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> 
<img src="https://img.shields.io/badge/-Stack-lightgray" alt="Stack"/> 

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
    const stack = [];
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

## [올바른 괄호](https://school.programmers.co.kr/learn/courses/30/lessons/12909)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> 
<img src="https://img.shields.io/badge/-Stack-lightgray" alt="Stack"/> 

```js
function solution(s){
    if(s.startsWith(")")) return false;
    
    const stack = [];
    
    for(const c of s){
        c === '(' ? stack.push(null) : stack.length && stack.pop();
    }
    
    return stack.length === 0;
}
```

## [주식가격](https://school.programmers.co.kr/learn/courses/30/lessons/42584)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> 
<img src="https://img.shields.io/badge/-Stack-lightgray" alt="Stack"/> 

```js
function solution(prices) {
    const stack = [];
    const answer = Array.from({ length: prices.length }, (_, i) => prices.length -1 - i);
    
    prices.forEach((price, i) => {
        while(stack.length && prices[stack.at(-1)] > price){
            const last = stack.pop();
            answer[last] = i - last;
        }
    
        stack.push(i);
    })
    
    return answer;
}
```

## [다리를 지나는 트럭](https://school.programmers.co.kr/learn/courses/30/lessons/42583)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> 
<img src="https://img.shields.io/badge/-Queue-blue" alt="Queue"/> 

```js
// 배열 기반 큐 모방, shift() 회피 
function solution(bridge_length, weight, truck_weights) {
    const queue = [];
    
    const calcNextWeight = (array, begin) => {   
        let acc = 0;
        let n = (begin < 0)? Math.max(array.length + begin, 0) : begin;
   
        for(let i = n; i < array.length; i++){
            acc += array[i];
        }
  
        return acc;
    }

    let i = 0;
    
    while(true){        
        const next = truck_weights[i] || 0;
        const acc = calcNextWeight(queue, -(bridge_length-1)) + next;
        
        if(acc > weight){
            queue.push(0);
            continue;   
        }
        
        i++;  
        queue.push(next);
        
        if(acc === 0) return queue.length;
    }
}

// 큐(Queue) 자료구조 활용 
class Queue {
    constructor(size){
       this.value = new Array(size).fill(0); 
    }
    
    enqueue(value){
        this.value.push(value);
    }
    
    dequeue(){
        this.value.shift();
    }
}

function solution(bridge_length, weight, truck_weights) {
    const q = new Queue(bridge_length);
    
    const calcNextWeight = () => q.value.reduce((acc, current, i) => {
        if(i === 0) return acc;
        return acc += current;
    }, 0);
    
    
    return truck_weights.reduce((time, truck) => {   
        while(calcNextWeight() + truck > weight){
            time++;
            q.dequeue();
            q.enqueue(0);
        }
        
        time++;
        q.dequeue();
        q.enqueue(truck);
        
        return time;
    }, 0) + bridge_length;
}

// 원형 큐(Circular Queue) 자료구조 활용 
class CircularQueue {    
    constructor(size = 10){
        this.queue = new Array(size+1).fill(0); 
        this.size = size+1;
        this.front = 0;
        this.rear = 0;
    }
    
    isFull(){
        return this.front === (this.rear+1) % this.size;
    }
    
    isEmpty(){
        return this.front === this.rear;
    }
    
    peek(){
        if(!this.isEmpty()){            
            return this.queue[(this.front + 1) % this.size];  
        }
    }
    
    enqueue(value){
        if (this.isFull()) {
            return 0;
        }
        
        this.rear = (this.rear + 1) % this.size;
        this.queue[this.rear] = value;
        return 1;
    }
    
    dequeue(){
        if(!this.isEmpty()){
            this.front = (this.front + 1) % this.size;
        
            return this.queue[this.front];   
        }
    }
}

function solution(bridge_length, weight, truck_weights) {
    const cq = new CircularQueue(bridge_length);
    
    for(let i = 0; i < bridge_length; i++){
        cq.enqueue(0);
    }

    let current = 0;
    
    return truck_weights.reduce((time, truck) => {
        while(current - (cq.peek() || 0) + truck > weight){
            time++;
            current -= (cq.dequeue() || 0)
            cq.enqueue(0); 
        }
        
        time++;
        current -= (cq.dequeue() || 0);
        current += truck;
        cq.enqueue(truck);
        
        return time;
    }, 0) + bridge_length;
}
```

##### Review 

```
제한 조건
- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.
```
