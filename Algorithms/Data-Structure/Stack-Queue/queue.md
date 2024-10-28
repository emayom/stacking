# 큐(Queue)

## 선형 큐(Linear Queue) 구현
```js
class Node {
    constructor(value){
        this.value = value;
        this.next = null;
    }
}

class Queue {
    constructor(size){
        this.front = 0;
        this.rear = 0;
        this.size = 0;
    }

    isEmpty(){
        return !this.front && !this.size;
    }

    #isEqual(node1, node2){
        if(!(node1 instanceof Node) || !(node2 instanceof Node)) return false;

        // temp 
        const nodeToString = (object) => Object.entries(object).toString();
        
        return nodeToString(node1) === nodeToString(node2);
    }
    
    enqueue(value){
        const node = new Node(value);

        if(this.isEmpty()){
            this.front = node;
            this.rear = node;
        } else {
            this.rear.next = node;
            this.rear = node;
        }

        return ++this.size;
    }
    
    dequeue(){
        if(this.isEmpty()) return;

        const { next, value } = this.front;

        if(this.#isEqual(this.front, this.rear)){
            this.rear = null;
        }

        this.front = next;
        this.size--;

        return value;
    }
}
```
