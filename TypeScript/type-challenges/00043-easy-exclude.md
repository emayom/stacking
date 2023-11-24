# 43 - Exclude <img src="https://img.shields.io/badge/-easy-7aad0c" alt="easy"/> <img src="https://img.shields.io/badge/-%23built--in-999" alt="#built-in"/> <img src="https://img.shields.io/badge/-%23union-999" alt="#union"/>

### Question
Implement the built-in `Exclude<T, U>`

> Exclude from `T` those types that are assignable to `U`

For example:

```ts
type Result = MyExclude<'a' | 'b' | 'c', 'a'> // 'b' | 'c'
```

---
### Answer
```ts
type MyExclude<T, U> = T extends U ? never : T;
```

`T extends U? never : T` 
- `분산 조건부 타입(Distributive Conditional Types)`  

    조건부 타입(conditional types)은 아래와 같은 형태를 가진다. 
    ```ts
     SomeType extends OtherType ? TrueType : FalseType;
    ```
    조건부 타입의 제네릭 타입에 유니온 타입을 넘기면, 분산되어 각 유니온 멤버 타입에게 매핑되어 적용되며,
    **분산 조건부 타입(Distributive Conditional Types)** 으로 사용된다.  

    만약 분산되지 않기를 원한다면 `extends` 양 옆의 파라미터에 `[](square brackets)`을 감싸서 방지할 수 있다. 
    ```ts
    [Type] extends [any] ? Type[] : never;
    ```

- `never`  
    위의 코드에서 조건에 부합될 경우 해당 유니온 멤버 타입을 `never`로 매핑하게 되는데, `never`로 매핑된 타입은 유니온 타입 내에서 무시되어 결과에서 제외된다. 

#### Documents
[Distributive Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#distributive-conditional-types)

#### lib.es5.d.ts
```ts
/**
 * Exclude from T those types that are assignable to U
 */
type Exclude<T, U> = T extends U ? never : T;
```