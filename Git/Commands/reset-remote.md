---
title: git reset/remote
category: Git
tags:
  - Git
  - Commands
date: 2023-11-17T00:00:00.000Z
last_modified_at: '2024-12-13T06:15:18.860Z'
---

# :rewind: git 원격 저장소 초기화 

현재 디렉토리의 `.git` 디렉토리 삭제 
```bash
rm -rf ./.git
```

현재 디렉토리를 Git 레포지토리로 (다시 `.git` 디렉토리 초기화)
```bash
git init
```

커밋 
```bash
git add .
git commit -m "Initial commit"
```

`remote` 추가 
```bash
git remote add [name] [URL]
```

원격 브랜치에 업로드합니다.
> `--force` 옵션은 기존 커밋을 삭제하거나 덮어쓰니 주의!
```bash
git push --force --set-upstream origin main
```
