#### TOC
1. [더 맵게](#더-맵게)

## [더 맵게](https://school.programmers.co.kr/learn/courses/30/lessons/42626)

<img src="https://img.shields.io/badge/-프로그래머스-1e2a3c" alt="프로그래머스"/> <img src="https://img.shields.io/badge/-Level 2-green" alt="Level 2"/> <img src="https://img.shields.io/badge/-Heap-rosybrown" alt="Heap"/> 

```js
class MinHeap {
    constructor(array){    
        this.value = [];
        
        if(Array.isArray(array)){
             array.forEach(value => this.insert(value));
        }
    }
    
    #swap(idx1, idx2){
       [this.value[idx1], this.value[idx2]] = [this.value[idx2], this.value[idx1]];
    }
    
    #bubbleUp(idx){
        if(idx === 0) return;
        
        const parent_idx = Math.floor((idx-1)/2);
        
        if(this.value[parent_idx] > this.value[idx]){
            this.#swap(parent_idx, idx);
            this.#bubbleUp(parent_idx);
        }
    }
    
    #bubbleDown(idx){
        if(idx === this.value.length-1) return;
        
        const l_idx = (2*idx)+1;
        const r_idx = (2*idx)+2;
        
        const parent = this.value[idx];
        const l_child = this.value[l_idx];
        const r_child = this.value[r_idx];
        
        const min = Math.min(...[parent, l_child, r_child].filter(Boolean));
        const min_idx = min === parent 
                            ? idx 
                            : min === l_child ? l_idx : r_idx;
        
        if(min_idx !== idx){
            this.#swap(idx, min_idx);
            this.#bubbleDown(min_idx);
        }
    }
    
    peek(){
        return this.value[0] || null;
    }
    
    insert(value){        
        this.value.push(value);
        this.#bubbleUp(this.value.length-1);
    }
    
    extractMin(){
        if(!this.value.length) return null;
        if(this.value.length === 1) return this.value.pop();

        const min = this.value[0];
        
        this.#swap(0, this.value.length-1);
        this.value.pop();
        this.#bubbleDown(0);
        
        return min;
    }
}

function solution(scoville, K) {
    const heap = new MinHeap(scoville);
    
    let i = 0;
     
    while(heap.peek() < K){
        const min = heap.extractMin();
        const next = heap.extractMin();
        
        if(next === null){
            return -1;
        } else {   
            i++;
            heap.insert(min + (next*2));  
        }
    }
    
    return i;
}
```

##### Review 

```
제한 사항
- scoville의 길이는 2 이상 1,000,000 이하입니다.
- K는 0 이상 1,000,000,000 이하입니다.
- scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.
```

제한 사항에 따르면 입력 배열(`scoville`)의 길이는 최대 1,000,000이며, 입력 배열을 모두 순회하고도 스코빌 지수 `K`를 만족시키지 못할 경우도 존재한다. 따라서 제한된 시간 내에 문제를 해결하기 위해서는 `solution` 함수가 O(n log n) 이하의 시간 복잡도를 가져야 한다.

문제에서 요구하는 `모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞은 횟수`를 구하기 위해서는 입력 배열(`scoville`)을 반복적으로 탐색하면서 가장 낮은 두 수를 찾아 연산한 결과 값을 다시 배열에 포함해야 하며, 이를 조건에 부합할 때까지 반복해야 한다.

이때, O(n log n) 이하의 알고리즘으로 작성하려면 입력 배열(`scoville`)을 탐색하는 반복문 내부에서 **최소값을 추출하고 배열 수정하는 작업**이 O(log n)의 시간 복잡도를 보장해야 한다.  

만일 정렬과 이진 탐색(Binary Search)을 활용하여 풀이할 경우, O(log n)의 시간 복잡도로 삽입 위치를 탐색할 수 있지만, 이후 배열에 새로운 요소를 삽입할 때 나머지 요소들을 이동하는 과정에서 기존 배열의 모든 요소를 복사하며 O(n)의 시간 복잡도가 발생되어 적절하지 않다. 

따라서, 이 경우 **최소 힙**의 특성을 활용하면, 매번 정렬하지 않고도 최솟값을 O(log n)의 시간 복잡도로 추출할 수 있으며, 다시 새로운 값을 삽입하는 과정도 O(log n)의 복잡도로 처리할 수 있다.
