# 제네릭(Generics)

#### 제네릭이 필요한 이유는 뭘까?
- 유연성
- 타입 안정성 

#### 타입스크립트의 추론(infer) 
**As-Is**
```ts
// 배열의 맨 앞에 요소를 추가한 새로운 배열을 리턴하는 함수 
function insertAtBeginning(array: any[], value: any){
    return [value, ...array];
}

const demoArray = [1, 2, 3];

const updatedArray = insertAtBeginning(demoArray, -1);

updatedArray[0].split(''); // any[]로 추론되어 타입스크립트는 오류 표시 X
```

**To-Be**
```ts
// 배열의 맨 앞에 요소를 추가한 새로운 배열을 리턴하는 함수 
function insertAtBeginning<T>(array: T[], value: T){
    return [value, ...array];
}
const demoArray = [1, 2, 3];

const updatedArray = insertAtBeginning(demoArray, -1); // number[], number로 추론  

updatedArray[0].split(''); // 타입스크립트는 오류 표시 
```
`제네릭`의 추가로 **배열의 구성 요소들의 타입**과 **새로 추가할 요소의 타입**이 같아야 함도 함께 명시할 수 있었다. 

<br>

```ts
let numbers: Array<number> = [1, 2, 3];

let numbers: number[] = [1, 2, 3];  // 문법적 설탕(Syntax Sugar)
```

#### 유니온의 한계  
```ts
function insertAtBeginning(array: (string | number)[], value: string | number){
    return [value, ...array];
}

const updatedArray = insertAtBeginning(demoArray, '-1'); // 타입스크립트는 오류 표시 X
```

```ts
// x, y를 arguments로 받아 더한 값을 리턴하는 함수 (x, y는 같은 타입을 가진다.)
function add(x: string | number, y: string | number): string | number {
    return x + y;
}

add(1,'2'); // 타입스크립트는 오류 표시 X

// 위의 문제를 해결하기 위해서는 `함수 오버로딩`이 필요하다. 
function add(x: string, y: string): string;
function add(x: number, y: number): number;
function add(x: any, y: any) {
   return x + y;
}

add(1,'2'); // No overload matches this call.

// 제네릭을 사용하면
function add<T>(x: T, y: T): T{
    return x + y;
}

add<number>(1,2);
add<string>('hello','world');
```


#### type에서의 제네릭
```ts
type JobRun<T> = {
    job: T;
    state: "queued" | "running" | "completed";
    onCompleted: (cb: (job: T) => void) => void;
}
```