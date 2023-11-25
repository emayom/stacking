# 3060 - Unshift <img src="https://img.shields.io/badge/-easy-7aad0c" alt="easy"/> <img src="https://img.shields.io/badge/-%23array-999" alt="#array"/>

### Question
Implement the type version of ```Array.unshift```

For example:

```typescript
type Result = Unshift<[1, 2], 0> // [0, 1, 2,]
```

---
### Answer
```ts
type Unshift<T extends readonly unknown[], U> = [U, ...T];
```
`<T extends readonly unknown[], U>`
- `extends`로 제네릭 타입 파라미터 제한
- `readonly`로 제네릭 타입 파라미터가 배열이나 튜플이며, immutable한지 

`[U, ...T]`
- `spread 연산자`를 활용하여 두 제네릭 타입을 `얕은 복사(shallow copy)`하여 다른 배열 안에 리턴 
- TypeScript 4.0 부터 튜플에서도 `spread 연산자`를 사용할 수 있다. (`가변 인자 튜플(Variadic Tuple Types)`)

#### Documents
[Spread](https://www.typescriptlang.org/docs/handbook/variable-declarations.html#spread)
[TypeScript 4.0 - Variadic Tuple Types](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#variadic-tuple-types)