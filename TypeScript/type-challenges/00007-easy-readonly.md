# 7 - Readonly <img src="https://img.shields.io/badge/-easy-7aad0c" alt="easy"/> <img src="https://img.shields.io/badge/-%23built--in-999" alt="#built-in"/> <img src="https://img.shields.io/badge/-%23readonly-999" alt="#readonly"/> <img src="https://img.shields.io/badge/-%23object--keys-999" alt="#object-keys"/>

---
### Question
Implement the built-in `Readonly<T>` generic without using it.  
Constructs a type with all properties of T set to readonly, meaning the properties of the constructed type cannot be reassigned.

For example:

```ts
interface Todo {
  title: string
  description: string
}

const todo: MyReadonly<Todo> = {
  title: "Hey",
  description: "foobar"
}

todo.title = "Hello" // Error: cannot reassign a readonly property
todo.description = "barFoo" // Error: cannot reassign a readonly property
```

---
### Answer
```ts
type MyReadonly<T> = {
  readonly [P in keyof T]: T[P];
}
```

`readonly [P in keyof T]: T[P]`
- `in`, `keyof`로 T 타입을 순회

- `readonly`를 활용하여 T 타입의 모든 속성을 immutable한 읽기 전용 프로퍼티로 지정
    - `const`와 `readonly` 차이점
        - const: (1) 변수 참조를 위한 (2) 변수에 다른 값을 대입/할당할 수 없음  
        - readonly: (1) 속성을 위한 (2) 속성을 엘리어싱을 통해 변경될 수 있음 


#### Documents
[Readonly<Type>](https://www.typescriptlang.org/docs/handbook/utility-types.html#readonlytype)  
[Using a limited set of string literals](https://basarat.gitbook.io/typescript/type-system/index-signatures#using-a-limited-set-of-string-literals)  
[readonly Properties](https://www.typescriptlang.org/docs/handbook/2/objects.html#readonly-properties)

#### lib.es5.d.ts
```ts
/**
 * Make all properties in T readonly
 */
type Readonly<T> = {
    readonly [P in keyof T]: T[P];
};
```