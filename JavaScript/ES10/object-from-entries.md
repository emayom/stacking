---
last_modified_at: '2025-01-20T16:20:31.999Z'
date: '2025-01-20T16:20:31.999Z'
---
<img src="https://img.shields.io/badge/ES10-F7DF1E?style=for-the-badge&logoColor=#1f2328"> 

# Object.fromEntries() 
```js
Object.fromEntries(iterable);
```
**Object.fromEntries()** 는 ES10<sup style="color: #656D76">ES2019</sup>에 소개된 기능으로 파라미터로 받은 `key-value` 쌍의 목록으로 부터 새로운 객체를 리턴한다. 

<br>

## Object.fromEntries() 활용하기 👌
**Object.fromEntries()** 는 `Map`을 `Object`로, `Array`를 `Object`로 변환하거나 `Object` 변환이 필요할 때 유용하게 사용할 수 있다.  
개인적으로는 **Object.fromEntries()** 는 `Object` 변환에서 활용도 높게 사용할 수 있을 것 같다! 

- [Map을 Object로](#map을-object로)
- [Array를 Object로](#array를-object로)
- [Object 변환](#object-변환) :white_check_mark:

<br>

### Map을 Object로 
```js
const map = new Map([
  ["foo", "bar"],
  ["baz", 42],
]);

// ✅ Convert Map to Object
const obj = Object.fromEntries(map);
console.log(obj); // 👉️ { foo: "bar", baz: 42 }

// ✅ Convert Object to Map
const newMap = new Map(Object.entries(obj));
console.log(newMap); // 👉️ { 'foo' => 'bar', 'baz' => 42 }
```

### Array를 Object로 
```js
const arr = [
  ["0", "a"],
  ["1", "b"],
  ["2", "c"],
];

// ✅ Convert Array to Object
const obj = Object.fromEntries(arr);
console.log(obj); // 👉️ { 0: "a", 1: "b", 2: "c" }

// ❌ 
const failed = Object.fromEntries(["0", "a"]);
```

**Object.fromEntries()** 를 활용하여 배열을 객체로 변환하기 위해서는 `key-value` 쌍을 가지는 2차원 배열을 만족해야 한다.  
2차원 배열을 만족한다면, 아래와 같이 내부 배열의 길이가 길어지거나 짧아져도 오류를 발생시키지 않는다. 

```js
const arr = [
  ["0", "a", "b", "c"],
  ["1", "b", "c"],
  ["2"],
];

const obj = Object.fromEntries(arr);
console.log(obj); // 👉️ {0: 'a', 1: 'b', 2: undefined}
```

### Object 변환 
```js
const object1 = { a: 1, b: 2, c: 3 };

const object2 = Object.fromEntries(
  Object.entries(object1).map(([key, val]) => [key, val * 2]),
);

console.log(object2); // 👉️ { a: 2, b: 4, c: 6 }
```

**Object.fromEntries()** & **Object.entries()** 를 함께 사용하면 `map`, `filter`와 같은 배열 조작 매서드를 사용할 수 있다. 

<br>

## reduce()와 ... 대신 Object.fromEntries() & Object.entries()로 리팩토링하기 
최근 **Object.fromEntries()** & **Object.entries()** 를 가장 효과적으로 사용했던 부분은  
객체에서 `reduce`를 사용하여 변환된 새로운 객체를 리턴하기 위해 흔히 작성하는  

- `initialValue`로 빈 객체(`{}`)를 넘겨주고,  
- `callbackFn` 내부에서 `Spread Operator`를 활용해 이전에 생성된 Object 를 풀어주고 새로운 아이템을 추가하는 `{ ...acc, 생략 }` 와 같은 로직 부분이었다. 

<br>

`reduce()`와 `Spread Operator`를 함께 사용하면 간결하게 객체를 변환하는 로직을 작성할 수 있지만,  
`Spread Operator`는 **Syntax sugar** 라는 사실을 알아둘 필요가 있다.   

> `Spread Operator`는 어떻게 동작할까? 
> 👉️ [TC39 Proposal](https://github.com/tc39/proposal-object-rest-spread/blob/main/Spread.md)

```js
// Shallow Clone (excluding prototype)
let aClone = { ...a };

// Desugars into:
let aClone = Object.assign({}, a);
```

`Spread Operator`는 내부적으로는 `Object.assign({}, ...)`과 동일하게 동작하며  
내부적으로는 `initialValue`로 전달한 객체에 계속 새로운 `key-value`가 추가되는 것이 아닌 키를 순회하며 매번 새로운 객체를 생성하고 있다. 

작은 데이터셋의 경우, 혹은 최신 자바스크립트 엔진의 경우 성능면에서는 차이가 미미할 수 있으나 같은 로직을 작성하더라도 **Object.fromEntries()** & **Object.entries()** 를 활용하여 리팩토링한 코드가 오히려 읽기 좋은 코드처럼 느껴졌다! 
