# 4 - Pick <img src="https://img.shields.io/badge/-easy-7aad0c" alt="easy"/> <img src="https://img.shields.io/badge/-%23union-999" alt="#union"/> <img src="https://img.shields.io/badge/-%23built--in-999" alt="#built-in"/></h1>

```ts
// expected to be string
type MyPick<T, K extends T> = any
```
```ts
// you should make this work
type test = Expect<Equal<HelloWorld, string>>
```

---
### Question
Implement the built-in `Pick<T, K>` generic without using it.  
Constructs a type by picking the set of properties `K` from `T`

### Answer
```ts
type MyPick<T, K extends Keyof T> = {
    [P in K]: T[P]
}
```

`extends keyof T` 
- `subset`  
- `key of`를 활용한 제네릭의 제한   


`[P in K]: T[P]`
- `[P in K]` 자바스크립트의 `for...in` 문법과 유사하게 동작   
    `K`를 순회하며 `T[P]`에 해당하는 타입을 값으로 가지는 객체의 키로 정의 


#### Documents
[Pick<Type, Keys>](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)  
[Using Type Parameters in Generic Constraints](https://www.typescriptlang.org/docs/handbook/2/generics.html#using-type-parameters-in-generic-constraints)

#### lib.es5.d.ts
```ts
/**
 * From T, pick a set of properties whose keys are in the union K
 */
type Pick<T, K extends keyof T> = {
    [P in K]: T[P];
};
```