# 898 - Includes <img src="https://img.shields.io/badge/-easy-7aad0c" alt="easy"/> <img src="https://img.shields.io/badge/-%23array-999" alt="#array"/>

### Question
Implement the JavaScript `Array.includes` function in the type system. A type takes the two arguments. The output should be a boolean `true` or `false`.

For example:

```ts
type isPillarMen = Includes<['Kars', 'Esidisi', 'Wamuu', 'Santana'], 'Dio'> // expected to be `false`
```

---
### Answer
```ts
type Includes<T extends readonly any[], U> = U extends T[number] ? true : false;
```
- `U extends T[number]`
    - T라는 Tuple 타입에서 각 요소에 대한 Tuple 인덱스 접근( `T[number]` )을 통해 유니온 타입으로 변환하여 확인한다.  
      
      기본적이고 간단하기에 가장 먼저 떠오른 방법이다.  
      문제는 이렇게 작성할 경우,
      - primitive 타입일 경우 `boolean` 타입에서 
      - non-primitive 타입일 경우 모든 상황에서 정확한 비교를 보장하지 않는다. 
        - 특히 `[1 | 2]`와 같은 튜플이 들어올 경우에도 `1 | 2`와 같이 예상과 다르게 변환된다. 

<br/>

```ts
type Includes<T extends readonly any[], U> = T extends [infer F, ...infer R]
  ? Equal<F, U> extends true
    ? true
    : Includes<R, U>
  : false;
```
> `Equal`은 `@type-challenges/utils`에 포함된 유틸리티 타입이다.   

- `T extends [infer F, ...infer R]? ... : ...`
    - 조건부 타입과 `infer` 키워드를 통해 첫 번째 요소의 타입 추론 

- `Equal<F, U> extends true`
    - 추론된 `F` 타입과 제네릭 `U` 타입의 정확한 비교가 필요하다 내부적으로 제공된 `Equal` 타입을 활용할 수 있다.
    
- `Equal<F, U> extends true ? true : Includes<R, U>`    
    - `Equal` 반환 타입이 `extends true`라면 비교를 멈추고
    - 아니라면 나머지 튜플 `R`의 추론을 재귀적으로 이어나간다. 
