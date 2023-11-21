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
```ts
type HelloWorld = string
```