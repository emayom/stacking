# 14 - First of Array <img src="https://img.shields.io/badge/-easy-7aad0c" alt="easy"/> <img src="https://img.shields.io/badge/-%23array-999" alt="#array"/>

### Question
Implement a generic `First<T>` that takes an Array `T` and returns its first element's type.

For example:

```ts
type arr1 = ['a', 'b', 'c']
type arr2 = [3, 2, 1]

type head1 = First<arr1> // expected to be 'a'
type head2 = First<arr2> // expected to be 3
```

---
### Answer
```ts
type First<T extends unknown[]> = T['length'] extends 0 ? never : T[0];
```
`T['length'] extends 0 ? never : T[0]`
- 가장 원초적인 방법이자 처음 떠오른 확실한 방식으로 `T['length']`를 통해 배열의 길이를 직접 접근하여 처리

    > 같지만 다른 접근 방법!
    ```ts
    T extends { length: 0 } ? never : T[0]
    ```

<br>

```ts
type First<T extends unknown[]> = T extends [infer U, ...infer _] ? U : never;
```

`T extends [infer U, ...infer _] ? U : never;`
- `조건부 타입(Conditional Types)`  
    ```ts
    T extends U ? X : Y
    ```
    자바스크립트의 삼항 연산자(conditional expressions)와 유사하게 동작한다.   
    `extends` 키워드 좌측의 제네릭 타입이 우측의 타입에 할당될 수 있다면 첫번째 분기(the “true” branch)로 그렇지 않다면 이후에 위치한 분기(the “false” branch)의 타입을 가진다.  


- `[infer U, ...infer _]`  
    ```ts
    T extends infer U ? X : Y
    ```
    `infer` 키워드는 TypeScript가 런타임 상황에서 타입을 `추론(Inferring)`할 수 있도록 하고 추론한 값을 `타입 파라미터(type parameter)`에 할당한다. 

    인덱스 0의 타입을 추론하여 타입 파라미터 `U`에 할당하고, 이후의 `_` 경우 더미 파라미터  
    (꼭 `_`일 필요는 없지만? 실제로 사용되지 않는 변수 이름으로, 보통 나머지 부분을 무시하고자 할 때 관례적으로 사용)

    > 비슷하지만 다른 접근 방법!  
    > 아래와 같은 방식에서는 나머지 요소는 `any` 타입의 배열로 처리 
    ```ts
    type First<T extends unknown[]> = T extends [infer U, ...any[]]? U : never;
    ```

- `unknown`  
   어떤 타입이 들어올지 알 수 없을 때 `any` 타입 대신 `unknown` 타입 사용


#### Documents

[TypeScript3.0 - unknown](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#new-unknown-top-type)  
[TypeScript2.8 - Infer](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-8.html#type-inference-in-conditional-types)  
[Inferring Within Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#inferring-within-conditional-types)
