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
