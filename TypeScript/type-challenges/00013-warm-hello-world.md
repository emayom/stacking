# 13 - Hello World <img src="https://img.shields.io/badge/-warm--up-teal" alt="warm-up"/>

```ts
// expected to be string
type HelloWorld = any
```
```ts
// you should make this work
type test = Expect<Equal<HelloWorld, string>>
```

---
### Answer
```ts
type HelloWorld = string
```

#### Documents
[The primitives: string, number, and boolean](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#the-primitives-string-number-and-boolean)