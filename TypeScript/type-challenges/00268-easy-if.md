# 268 - If <img src="https://img.shields.io/badge/-easy-7aad0c" alt="easy"/> <img src="https://img.shields.io/badge/-%23utils-999" alt="#utils"/>

### Question
Implement the util type `If<C, T, F>` which accepts condition `C`, a truthy value `T`, and a falsy value `F`. `C` is expected to be either `true` or `false` while `T` and `F` can be any type.

For example:

```ts
type A = If<true, 'a', 'b'>  // expected to be 'a'
type B = If<false, 'a', 'b'> // expected to be 'b'
```

---
### Answer
```ts
type If<C extends boolean, T, F> = C extends true ? T : F;
```

`extends true`
- 조건부 타입에서 `C`가 true에 할당이 가능하다면 `T`, 아니라면 `F`를 리턴하도록 활용 
