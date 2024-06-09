# 2759 - RequiredByKeys <img src="https://img.shields.io/badge/-medium-d9901a" alt="medium"/> <img src="https://img.shields.io/badge/-%23object-999" alt="#object"/>

### Question
Implement a generic `RequiredByKeys<T,  K>` which takes two type argument `T` and `K`.

`K` specify the set of properties of `T` that should set to be required. When `K` is not provided, it should make all properties required just like the normal `Required<T>`.

For example

```typescript
interface User {
  name?: string
  age?: number
  address?: string
}
```
---
### Answer
```ts
type RequiredByKeys<T, K extends keyof T = keyof T> = Omit<T & Required<Pick<T, K>>, never>;
```

- `K extends keyof T = keyof T`
  - `extends keyof T`
    - subset 
    - `key of`를 활용한 제네릭의 제한   

  - `= keyof T`
    - `keyof T`를 기본 타입 파라미터로 지정 `K` 타입이 명시되지 않았을 때 기본적으로 `T` 타입의 모든 속성을 포함 
    - 제네릭 `K` 타입의 기본 타입 파라미터를 명시하지 않을 경우 `RequiredByKeys<User>`와같이 유연하게 사용할 수 없음

      > 문제에서는 테스트 케이스로 `Expect<Equal<RequiredByKeys<User>, Required<User>>>`를 요구하고 있지만,   
      > 내장된 TypeScript 유틸리티 타입 `Required<Type>` 활용을 유도하기 위한 목적의 기본 타입 파라미터의 생략도 좋은 선택일 수 있다.

- `Required<Pick<T, K>`
  - `Required<Type>`을 활용하여 선택된 일부 속성들을 필수로 set 

- `Omit<T & Required<Pick<T, K>>, never>` 
  - `T & Required<Pick<T, K>>`와 같이 교차 연산자(&)만을 사용하여 리턴할 경우 내부적으로 동일한 타입으로 유추하지 않는다.  
