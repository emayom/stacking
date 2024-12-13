---
last_modified_at: '2024-12-13T06:19:47.141Z'
date: '2024-12-13T06:18:24.562Z'
---
# Git Config File Sections

## [core]
### core.quotepath `boolean`
- Default: `true`

한글처럼 큰 바이트를 문자의 이스케이프 처리 방식을 설정하는 옵션  
설정은 **경로 출력**에만 영향을 미치며, 내부적으로 파일을 다룰 때는 여전히 UTF-8 인코딩이 사용된다. 

- `true`: 한글이나 비 ASCII 문자는 각각의 유니코드 문자에 해당하는 **[이스케이프 시퀀스](https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%8A%A4%EC%BC%80%EC%9D%B4%ED%94%84_%EC%8B%9C%ED%80%80%EC%8A%A4)로 변환되어 출력**한다. 

- `false`: 한글이나 비 ASCII 문자가 포함된 경로를 이스케이프하지 않고 원본 그대로 출력한다.  

```sh
git config --global core.quotepath false
```

## [user]

## [pull]
### pull.rebase `boolean`
- Default: `false`
