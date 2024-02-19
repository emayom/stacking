# git pull 불편하게 사용해 보자.

```shell
git pull [<options>] [<repository> [<refspec>…​]]
```

git pull은 직관적이며 간편한 명령어이다. git pull을 사용하면 원격 저장소의 변경 사항을 가져와서 현재 작업 중인 로컬 브랜치에 쉽게 병합할 수 있다.

**가져와 병합**할 수 있다. git pull은 사실 하나의 작업 단위가 아니다.   
git pull은 페칭(fetching)과 병합(merging)을 함께 수행한다.  

원격 저장소 브랜치의 내용을 검토할 필요가 없다면 git pull은 효율적인 선택지일 수 있지만, 검토가 필요하다면 git fetch 이후 병합 여부를 결정하는 것이 더욱 안전하고 효율적일 수 있다.


> 누군가 원격 저장소의 변경 사항을 **확인**하기 위해 git pull을 사용하고 있다면, git fetch가 있다.

### git pull = git fetch + git merge

git pull은 주어진 파라미터들로 `git fetch`를 실행한 다음  config 옵션, 명령줄의 플래그에 따라 `git rebase` 또는 `git merge`를 실행하여 분기된 브랜치들을 조정한다.

> pull.rebase=false이거나 `--rebase`, `--no-rebase` 플래그가 없다면 기본적으로 merge를 수행한다.

결국 git pull을 `git fetch`와 `git merge`로 분리하여 실행해도 동일한 결과를 얻을 수 있다.  
분리하여 실행했을 때 불편함 대신 아래와 같은 편리함도 얻을 수 있지 않을까?

- 변경 사항을 병합 이전에 확인할 수 있다. 
- 상황과 목적에 따라 적절한 병합 전략을 선택할 수 있다.
- 작업 흐름을 더욱 명확하게 이해하고 관리할 수 있다. 

꼭 git pull 대신 `git fetch` + `git merge`와 같이 사용해야 한다는 것은 아니지만,  
불편하더라도 git pull 이전에 `git fetch`를 통해 origin의 변경 사항을 확인한 후 팀의 선호 방식이나 규칙에 따라 병합을 수행하는 습관을 기르는 것이 좋을 것 같다.
