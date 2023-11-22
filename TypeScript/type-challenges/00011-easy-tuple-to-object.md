# 11 - Tuple to Object <img src="https://img.shields.io/badge/-easy-7aad0c" alt="easy"/> <img src="https://img.shields.io/badge/-%23object--keys-999" alt="#object-keys"/>

### Question
Given an array, transform it into an object type and the key/value must be in the provided array.

For example:

```ts
const tuple = ['tesla', 'model 3', 'model X', 'model Y'] as const

type result = TupleToObject<typeof tuple> // expected { 'tesla': 'tesla', 'model 3': 'model 3', 'model X': 'model X', 'model Y': 'model Y'}
```

---
### Answer
```ts
type TupleType = string | number | symbol;

type TupleToObject<T extends readonly TupleType[]> = {
  [K in T[number]]: K;
}
```

```ts
type TupleToObject<T extends readonly (string | number | symbol)[]> = {
  [K in T[number]]: K;
}
```

`TupleType[]` or `(string | number | symbol)[]`  
> [Issues#30496](https://github.com/type-challenges/type-challenges/issues/30496#issuecomment-1822119104)    
> 이슈 탭을 구경하다 우연히 같은 궁금증을 가지신 분을 발견하여 답변도 조심스럽게 공유도 드려보았다 🤭  

- 제네릭을 `union` 타입으로 지정한다. `any[]` 타입으로 지정할 경우 테스트 코드는 통과하지만 `// @ts-expect-error` 주석에서 `red squiggle`이 발생하기 때문에 제네릭 타입 지정 필요!   
     

`{ [K in T[number]]: K }`  
- T라는 Tuple 타입에서 각 요소에 대한 Tuple 인덱스 접근( `T[number]` )을 통해 `T[number]`를 프로퍼티 키이자 값으로 가지는 새로운 객체를 생성하는 **Mapped Type**

#### Documents
[Tuple Types](https://www.typescriptlang.org/docs/handbook/2/objects.html#tuple-types)  
[// @ts-expect-error Comments](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-9.html#-ts-expect-error-comments)  
[Index Signatures](https://www.typescriptlang.org/docs/handbook/2/objects.html#index-signatures)
