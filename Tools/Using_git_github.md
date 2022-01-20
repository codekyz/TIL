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

- `git commit [-m "commit message"]`
- `git commit [-a]` 수정되거나 삭제한 파일만 commit
- `git reset [--hard, --soft, --mixed 'commit hash code']` : 해당 커밋으로 롤백
- `git reset [--hard]` : 가장 마지막 커밋으로 롤백

- `git remote add origin 'repository url'` : 깃허브와 연동
- `git remote remove` : 연동 끊기
- `git remote [-v]` : 연동 확인

- `git push origin main` : 깃허브 repo 메인 브랜치에 현재 커밋을 넣음
- `git clone 'repository url'` : 깃허브 repo에서 모든 커밋을 로컬로 가져옴
- `git pull origin main` : 서버에서 변경사항이 일어난 것을 로컬로 동기화, 로컬과 서버 상태를 맞춰주기 위해

- `.gitignore` : 커밋 예외사항 설정 파일

# warnning 해결
> warning: LF will be replaced by CRLF in README.md.
운영체제에 따라 개행문자가 달라 경고해주는 것
-> `git config core.autocrlf true`


***맨날 까먹는 git...***