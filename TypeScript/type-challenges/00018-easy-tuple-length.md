# 18 - Length of Tuple <img src="https://img.shields.io/badge/-easy-7aad0c" alt="easy"/> <img src="https://img.shields.io/badge/-%23tuple-999" alt="#tuple"/>

### Question
For given a tuple, you need create a generic `Length`, pick the length of the tuple

For example:

```ts
type tesla = ['tesla', 'model 3', 'model X', 'model Y']
type spaceX = ['FALCON 9', 'FALCON HEAVY', 'DRAGON', 'STARSHIP', 'HUMAN SPACEFLIGHT']

type teslaLength = Length<tesla>  // expected 4
type spaceXLength = Length<spaceX> // expected 5
```

---
### Answer
```ts
type Length<T extends readonly unknown[]> = T['length'];
```

`<T extends readonly unknown[]>`  
- `extends`로 제네릭 타입 파라미터 제한
- `readonly`로 제네릭 타입 파라미터가 배열이나 튜플이며, immutable한지 

`T['length']`
- `length` 프로퍼티를 통해 해당 타입의 길이를 확인

<br>

#### +) Const Assertions
> 타입 스크립트에서는 변수 `const` 선언과`let` 선언의 타입 추론이 다르다.  
> 하지만, `let` 키워드를 사용하더라도 `as` 키워드를 통해 컴파일러가 가진 정보를 무시하고 특정 타입 정보를 강제하는 **타입 단언**<sup style="color: #656D76">Type assertions</sup>이 가능하다.   

배열이나 객체일 경우에는 `const` 선언을 하더라도 타입 추론 범위가 제한되지 않는다. 이때 `as const` 키워드로 **Const Assertions**을 사용할 수 있다. 

- 예제 
    ```ts
    // Type readonly ['tesla', 'model 3', 'model X', 'model Y']
    const tesla = ['tesla', 'model 3', 'model X', 'model Y'] as const; 
    ```
    tesla 변수는 `as const`를 사용하여 배열 리터럴(Array Literal)은 `readonly` Tuple 타입이 된다. 

<br>

#### Documents
[type assertions](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)  
[const assertions](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#const-assertions)
