# Git 특강 2일차



#### 01.로컬 저장소와 원격 저장소 연결 ####



1. `git remote`

- 로컬 저장소에 `원격` 저장소를 등록, 조회, 삭제 할 수 있는 명령어

형식: `git remote add <이름> <주소>`



2. `git remote -v`

- 원격 저장소 조회

  

3. `git remote rm <이름>`

- 원격 저장소 연결 삭제



---



#### 02. 원격 저장소에 업로드 ####



1. 로컬 저장소에서 커밋 생성

- git status
- git add day1.md
- git commit -m "Upload day1"
- git log



2. 로컬 저장소의 커밋 원격 저장소에 업로드

   `git push <저장소 이름> <브랜치 이름>`

* -u옵션 (ex. git push -u origin master)

: 이후에 git push라고만 작성해도 push됨
