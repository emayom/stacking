# Number.MAX_SAFE_INTEGER 
```js
const x = Number.MAX_SAFE_INTEGER + 1;
const y = Number.MAX_SAFE_INTEGER + 2;

console.log(Number.MAX_SAFE_INTEGER);   // 9007199254740991
console.log(x === y);   // true
```

자바스크립트에서 **안전한** 최대 정수의 값은 몇일까?  
여기서의 안전함이란 정수를 정확하고 올바르게 비교할 수 있음을 의미한다. 

ECMAScript는 `IEEE 754`에 기술된 배정밀도 부동소숫점 형식 숫자 체계를 사용한다.  
따라서 -(2<sup>53</sup>- 1)과 2<sup>53</sup> - 1 사이의 수만 안전하게 표현할 수 있다. 이 범위를 벗어나면, JavaScript는 더 이상 정수를 안전하게 표시할 수 없다. 

원시 자료형 `Number`로 사용 가능한 최대 정수 값은 Number의 정적 속성(Static properties) [Number.MAX_SAFE_INTEGER](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)을 통해 확인할 수 있으며, 전달된 정수의 값이 안전한 값인지 확인하기 위해서는 [Number.isSafeInteger()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number/isSafeInteger) 매서드를 사용하여 확인할 수 있다. 


만약 `Number` 자료형의 최댓값인 2<sup>53</sup> - 1. 즉, `9007199254740991` 보다 큰 정수 숫자를 표현해야한다면 [`BigInt`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/BigInt)를 사용할 수 있다. 


```js
const theBiggestInt = 9007199254740991n;

const alsoHuge = BigInt(9007199254740991); // 9007199254740991n
```

유스케이스로는 암호화 알고리즘 및 해시 함수, 대규모 숫자 처리, 데이터베이스에서 매우 큰 ID나 정수 값을 다룰 때 등이 있다. 
