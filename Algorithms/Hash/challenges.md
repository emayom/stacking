[2023 KAKAO BLIND RECRUITMENT - 개인정보 수집 유효기간](https://school.programmers.co.kr/learn/courses/30/lessons/150370)

```js
function solution(today, terms, privacies) {
    const tday = new Date(today).getTime();    
    
    const term_table = new Map(terms.map(term => {
        const [type, exp] = term.split(' ');
        return [type, Number(exp)]
    }));
    
    const exp_list = privacies.map((p, idx)=> {
        const [date, type] = p.split(' ');
        const exp = new Date(date);
        
        exp.setMonth(exp.getMonth() + term_table.get(type));
        exp.setDate(exp.getDate() - 1);
 
        return exp.getTime();
    });

    return exp_list.map((exp, idx) => tday - exp > 0 && idx + 1)
                    .filter(Boolean);
}
```

[프로그래머스 - 전화번호 목록](https://school.programmers.co.kr/learn/courses/30/lessons/42577)

```js
function solution(phone_book) {
    const table = new Map(phone_book.map(number => [number, true]));
    
    return !phone_book.find((number)=> 
                // 불필요한 배열 변환 과정 존재 
                number.split('').find((_, idx) => idx && table.has(number.slice(0, idx)))
            );
}
```

```js
function solution(phone_book) {
    const table = new Map(phone_book.map(number => [number, true]));
    
    return !phone_book.find((number)=> {
        for(let i = 1; i < number.length; i++){
            if(table.has(number.slice(0, i))){
                return true;
            }
        }
        return false;
    });
}
```

##### Review 
```
제한 사항
- phone_book의 길이는 1 이상 1,000,000 이하입니다.
    - 각 전화번호의 길이는 1 이상 20 이하입니다.
    - 같은 전화번호가 중복해서 들어있지 않습니다.
```

`정렬 후 탐색`, `해시 테이블 활용 방식` 모두 풀이가 가능하지만 카테고리가 **해시**인 만큼 해시 테이블을 활용하는 접근 방식을 선택했다. 

접두어를 비교하기 위해 키를 기반으로 많은 접근이 요구되는 상황에서 `Map`의 `has` 메서드를 통해 직관적으로 키에 접근하기 위해 `Map` 객체를 활용하여 해시 테이블을 구현했다. (Map의 경우 내부적으로 해시 테이블로 구현되어 키 기반 데이터 접근이 빠르다. 다만 잦은 갱신이 필요할 경우에는 `Object`와 비교하여 효율적이지 않을 수 있지만, 이 문제에서는 정적인 해시 테이블로 활용되어 크게 문제가 되지않을 것이다.)

해시 테이블을 구현 할 경우 메모리의 사용량이 증가하고, 공간 복잡도가 높아진다는 단점이 있다.  
해당 문제의 제한 사항에 따르면 키의 개수는 1 이상 1,000,000 이하이며 개별 키는 1 이상 20 이하의 문자열로 제한되어 있다.  
값(value) 역시 primitive `boolean` 타입으로 고려하였을 때 메모리 측면에서 큰 부담이 없을 것이라고 판단했다.  

[프로그래머스 - 의상](https://school.programmers.co.kr/learn/courses/30/lessons/42578)

```js
// 1-1. Map - forEach 
function solution(clothes) {
    const table = new Map();
    
    // O(n)
    clothes.forEach(([_, category])=> table.set(category, (table.get(category) || 0)+1));

    let combinations = 1;
    
    // O(k) = O(n)
    table.forEach((count)=> combinations *= (count + 1));
    
    // 아무것도 안 입는 경우 제외 
    return combinations - 1;
}

// 1-2. Map - for...of → O(n)
function solution(clothes) {
    const table = new Map();
    
    clothes.forEach(([name, category])=> table.set(category, (table.get(category) || 0)+1));
    
    let combinations = 1;
    
    for (const value of table.values()) {
        combinations *= (value + 1);
    }
    
    return combinations - 1;
}

// 2. Object 
function solution(clothes) {
    const table = new Object();
    
    clothes.forEach(([_, category])=> table[category] = (table[category] || 0) + 1);
    
    return  Object.values(table).reduce((acc, count)=> acc *= (count + 1), 1) - 1;
}
```

##### Review 

```
제한 사항
- clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
- 코니가 가진 의상의 수는 1개 이상 30개 이하입니다.
- 같은 이름을 가진 의상은 존재하지 않습니다.
- clothes의 모든 원소는 문자열로 이루어져 있습니다.
- 모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '_' 로만 이루어져 있습니다.
```

서로 다른 옷의 **조합의 수**를 return 하도록 출제된 문제인만큼 실제 이루어지는 모든 조합을 메모리에 저장하거나 증명할 필요가 없다. 

제한 사항에 따르면 코니가 가진 의상의 수는 1개 이상 30개 이하이다. 최대 조합 수를 구하기 위해 가능한 많은 종류로 나눌 경우, 각 종류별로 의상이 1개씩 존재하게 된다. 조합에서 해당 종류의 의상을 "입거나 안 입는" 두 가지 경우를 고려하여 계산한 최대 조합의 수는 $2^{30}$으로 만약 모든 종류의 조합을 입출력 예시처럼(`yellow_hat + blue_sunglasses`) 일일이 모든 조합을 메모리에 문자열로 저장할 경우, 시간 복잡도를 고려하지 않더라도 메모리 측면에서의 문제가 발생할 수 있다.

대략적으로 최악을 계산할 경우, 자바스크립트에서 문자열은 페이지의 인코딩 방식과 상관없이 UTF-16 인코딩 방식으로 저장한다. 각 조합을 나태는 문자열의 길이가 최대 40 이라고 가정하면, 각 조합의 크기는 최대 80바이트가 된다. 따라서, 배열이 $2^{30}$ 개의 요소를 모두 80바이트라고 가정할 경우, 총 메모리 사용량은 $2^{30} * 80$, 약 80GB 에 달할 수 있다. ($2^{30}$ 바이트 = 1GB)

모든 풀이의 `solution` 함수는 유사한 의사 코드를 가졌으며, **해시 테이블**을 통해 의상의 종류를 `key`로 종류별 개수를 카운팅했다. 카운팅 해시 테이블을 구성하는 로직에서 O(n), 총 조합의 수를 구하는 로직에서 O(n)의 시간 복잡도를 가지므로 각 풀이의 시간 복잡도는 최종적으로 O(n) 이 된다.

카운팅 과정에서 해시 테이블의 잦은 갱신 필요하다고 생각하여 Object를 사용하는 접근이 적합할 것이라고 예상하였지만 카운팅하려는 `clothes` 배열의 크기가 작기 때문에 큰 차이를 보이지 않았다. 결과적으로 각 풀이의 성능 차이가 크지 않다. 
