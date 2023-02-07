# 팀 개발을 위한 Git GitHub 시작하기 필기 - CLI

### git status - Git 저장소의 상태를 알려주는 명령
- 워킹 트리가 아닌 폴더에서 사용시 오류가 발생한다.
- -s옵션을 사용하면 짧게 요약이 가능하고, 변경 파일이 많으면 유용하다.

### git init : .git 폴더를 생성한다.

### 작업폴더안은 로컬 저장소(.git)와 워킹트리로 구성되어있음 (작업폴더 - 로컬저장소 = 워킹트리)

## Git 옵션
- 지역 옵션 : 현재 Git 저장소에서만 유효한 옵션이다 (local)
- 전역 옵션 : 현재 사용자를 위한 옵션이다.(global)
- 시스템 환경 옵션 : PC 전체의 사용자를 위한 옵션(system)

### git pull : 원격 저장소의 변경 사항을 워킹 트리에 반영한다 (git fetch 기능 + git merge 기능)

### git fetch [원격 저장소 별명] [브랜치 이름] : 원격 저장소의 브랜치와 커밋들을 로컬 저장소와 동기화 시킨다. 옵션 생략시 모든 원격 저장소에서 모든 브랜치를 가져온다.

### git merge 브랜치 이름 : 지정한 브랜치의 커밋들을 현재 브랜치 및 워킹트리에 반영한다.

## 파일을 stage영역에서 unsaged 영역으로 내리는 명령
- git rm --cached 파일명 
- git reset(default 옵션은 mixed 이므로  파일이 unstaged 상태로 변경됨)

### git log : 현재 브랜치의 커밋 이력을 보는 명령
- 옵션 
  - n<숫자> : 전체 커밋 중 최신 n개의 명령을 보여줌
  - oneline : 커밋 메세지를 한줄로 표기
  - graph : 커밋 옆 브랜치의 흐름을 그래프로 보여줌
  - decorate : 브랜치와 태그등의 참조를 간결하게 표시
  - all : all 옵션이 없는 경우, HEAD와 관계없는 옵션은 보여주지 않는다.

### upstream 브랜치 : 로컬 저장소와 연결된 원격저장소 (관례상 upstream)
### HEAD 브랜치 : 현재 작업중인 브랜치 혹은 커밋

## 브랜치 명령어
- git branch [-v] : 로컬 저장소의 브랜치 목록을 보는 명령으로 -v가 붙으면 마지막 커밋도 함께 표시한다.
- git branch [-f] 브랜치 이름 [커밋 체크섬] : 새로운 브랜치를 생성한다. 커밋 체크섬이 없으면 HEAD부터 생성한다. -f옵션은 이미 있는 브랜치를 다른 커밋으로 옮기고 싶은 경우 사용한다. 
- git branch -r[v] : 원격 저장소에 있는 브랜치 확인시 사용한다. 마찬가지로 -v가 붙으면 커밋을 요약한다. 
- git branch -d 브랜치 이름 : 특정 브랜치를 삭제한다. HEAD나 병합이 되지 않은 브랜치는 삭제가 불가능하다.
- git branch -D 브랜치 이름 : 강제로 브랜치를 삭제한다. 조심해서 사용해야함
- git checkout 브랜치 이름 : 특정 브랜치로 체크아웃 한다.
- git checkout -b 브랜치 이름 커밋 체크섬 : 특정 커밋에서 브런치 생성 후 체크아웃까지 한다.
- git merge 대상 브랜치 : 현재 브랜치와 대상 브랜치를 병합하는 경우 사용한다. 대부분 병합 커밋이 새로 생긴다.
- git rebase 대상 브랜치 : 내 브랜치 커밋을 대상 브랜치에 재배치한다. 원격 저장소에서는 사용하면 안된다.

### git reset --hard를 사용하기 위해선 커밋 체크섬을 알아야 하지만, HEAD를 통해 대체 가능
- HEAD~숫자 : n번째 윗쪽 조상(~는 부모 커밋, ~2는 할아버지 커밋)
- HEAD^숫자 : 병합 커밋처럼 둘 이상의 부모 중 ^2는 2번째 부모로 선택한다.

### 빨리감기 병합이 가능한 상황에서 rebase 시, 빨리감기 병합이 진행된다.

### 태깅
- git tag -a -m 메세지  태그이름  [브랜치 또는 체크섬] : -a를 통해 주석이 있는 태그를 생성한다. 옵션 생략시 HEAD에 태그를 생성한다.
- git push 원격저장소별명 태그이름 : 원격저장소에 만들어둔 태그를 업로드 한다.

## 버그처리 시나리오
- 1. 오류가 없는 버전으로 롤백한다.
- 2. master 브랜치로부터 hotfix(버그 수정) 브랜치를 생성한다.
- 3. 소스코드를 수정하고 테스트를 한다.
- 4. master 브랜치로 병합 및 배포를 진행한다.
- 5. 개발중인 브랜치에도 병합을 한다 (충돌 발생 확률 높음)

### rebase를 잘못 사용하면 꼬일 수 있기 때문에 원격 저장소에 푸시한 브랜치는 rebase를 하지 않아야 한다.
### 임시 브랜치를 활용하여 안전한 작업을 할 수 있다.

