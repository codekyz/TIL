# git config

- `git config --global "user.name"`
- `git config --global "user.email"`
- `git config --list`

# cmd

- `cd` : change directory
- `dir` Windows / `ls` Mac
- `q` : exit git log

# git

- `git init` : .git 폴더 생성, 해당 폴더 내부의 폴더와 파일들을 형상관리 하겠다는 선언
- `git status` : 해당 폴더 내의 형상관리 상태 정보
- `git add [.]` : staging, 일부 파일만 스테이징 할 때 이름이 변경되거나 삭제된 파일은 누락됨
- `git add [-u]` : 수정되거나 삭제된 파일 반영
- `git mv (oldname) (newname)` : 로컬과 저장소에서 파일명 변경, 변경시점에서 커밋하기

---

- `git commit [-m "commit message"]`
- `git commit [-a]` 수정되거나 삭제한 파일만 commit
- `git reset [--hard, --soft, --mixed 'commit hash code']` : 해당 커밋으로 롤백
- `git reset [--hard]` : 가장 마지막 커밋으로 롤백

---

- `git remote add origin 'repository url'` : 깃허브와 연동
- `git remote remove` : 연동 끊기
- `git remote [-v]` : 연동 확인

---

- `git push origin main` : 깃허브 repo 메인 브랜치에 현재 커밋을 넣음
- `git clone 'repository url'` : 깃허브 repo에서 모든 커밋을 로컬로 가져옴
- `git pull origin main` : 서버에서 변경사항이 일어난 것을 로컬로 동기화, 로컬과 서버 상태를 맞춰주기 위해

---

- `git branch` : 현재 브랜치 확인
- `git branch 'branch name'` : 브랜치 생성
- `git checkout 'branch name'` : 브랜치 이동
- `git merge 'baranch name'` : 현재 브랜치에 해당 브랜치를 합침

---

- `.gitignore` : 커밋 예외사항 설정 파일

---

- `git stash [save "message"]` : 변경 사항을 임시저장(WIP)하고 변경사항은 사라짐(추가된 파일은 저장불가)
- `git stash list` : 저장된 목록 조회
- `git stash show [-p]` : 저장된 내용 조회
- `git stash pop [stash@{index}]` : 저장된 stash를 목록에서 추출(추출 후 사라짐)
- `git stash apply [stash@{index}]` : 저장된 stash를 목록에서 불러옴(사라지지않음)
- `git stash drop [stash@{index}]` : 저장된 stash를 목록에서 삭제
- `git stash clear` : 저장된 stash 목록을 삭제

## cherryPick

- 망해서 돌아가야 하는데 필요한 것들은 살리고 싶을 때
- `git cherry-pick 'commit hash code'[..'commit hash code']` : 해당 커밋을 가져와서 지금 내 브랜치에 커밋

## conflict

- merge할 때 충돌이 나는 경우
- git은 3 way merge를 수행함

## rebase

- merge와의 차이 : 커밋 히스토리가 다름
- 공통의 base를 가진 두 개의 branch에서 하나의 branch의 base를 다른 branch의 최신 커밋으로 branch의 base를 옮기는 작업
  _아직은 잘 모르겠다_

# 브랜치 전략 git-flow

- 크게 다섯가지의 브랜치를 만들어서 개발을 운용하는 방법
- `Main(Master)` : 사용자가 접하는 버전(무조건 안정적)
- `Develop` : 개발용 브랜치(개발할 때 pull 받아오는 곳이자 feature 브랜치를 따오는 곳)
- `Release` : 배포용 브랜치(개발 브랜치에서 따와서 테스트를 하고 버그 수정만 함) **꼭 Develop과 Main에 merge 해줘야함**
- `Feature` : 기능개발용 브랜치(하다 망하면 버려도 되는 곳, 독립공간)
- `Hotfix` : 급하게 수정되어야 하는 이슈(버그/기능) **꼭 Develop과 Main에 merge 해줘야함**

# warnning 해결

> warning: LF will be replaced by CRLF in README.md.
> 운영체제에 따라 개행문자가 달라 경고해주는 것
> -> `git config core.autocrlf true`

**_맨날 까먹는 git..._**
