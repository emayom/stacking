# 533 - Concat <img src="https://img.shields.io/badge/-easy-7aad0c" alt="easy"/> <img src="https://img.shields.io/badge/-%23array-999" alt="#array"/>

### Question
Implement the JavaScript `Array.concat` function in the type system. A type takes the two arguments. The output should be a new array that includes inputs in ltr order

For example:

```ts
type Result = Concat<[1], [2]> // expected to be [1, 2]
```

---
### Answer
```ts
type Concat<T extends readonly unknown[], U extends readonly unknown[]> = [...T, ...U]
```

`<T extends readonly unknown[], U extends readonly unknown[]>`  
- `extends`로 제네릭 타입 파라미터 제한
- `readonly`로 제네릭 타입 파라미터가 배열이나 튜플이며, immutable한지 

`[...T, ...U]`
- `spread operator`를 활용하여 두 제네릭 타입을 `얕은 복사(shallow copy)`하여 다른 배열 안에 리턴 

#### Documents
[Spread](https://www.typescriptlang.org/docs/handbook/variable-declarations.html#spread)
