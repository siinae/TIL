# 01.로컬 저장소와 원격 저장소 연결 #



1. `git remote`

- 로컬 저장소에 `원격` 저장소를 등록, 조회, 삭제 할 수 있는 명령어

형식: `git remote add <이름> <주소>`



2. `git remote -v`

- 원격 저장소 조회

  

3. `git remote rm <이름>`

- 원격 저장소 연결 삭제



---



# 02. 원격 저장소에 업로드 #



1. 로컬 저장소에서 커밋 생성

- git status
- git add day1.md
- git commit -m "Upload day1"
- git log



2. 로컬 저장소의 커밋 원격 저장소에 업로드

   `git push <저장소 이름> <브랜치 이름>`

* -u옵션 (ex. git push -u origin master)

: 이후에 git push라고만 작성해도 push됨





---



# 03. .gitignore #

: 특정 파일 혹은 폴더에 대해 Git이 버전 관리를 하지 못하도록 지정하는 것



1. gitignore에 작성하는 목록

- 민감한 개인정보가 담긴 파일(전화번호, 계좌번호, 각종 비밀번호, API KEY 등)
- OS (운영체제) 에서 활용되는 파일
- IDE 혹은 Text editor(vscode) 등에서 활용되는 파일
- 개발 언어 혹은 프레임워크(django)에서 사용되는 파일



2. 작성 시 주의사항

- 반드시 ".gitignore"로 작성, 앞의 .은 숨김 파일을 의미
- .gitignore 파일은 .git폴더와 동일한 위치에 생성
- 제외하고 싶은 파일은 반드시 **git add 전에** .gitignore에 작성



3. .gitignore 쉽게 작성하기

- gitignore.io 사이트 이용



---



# 04. clone, pull #

1. git clone

- 원격 저장소의 커밋 내역을 모두 가져와 로컬 저장소를 생성하는 명령어
- 원격 저장소를 통째로 복제해 컴퓨터에 옮길 수 있음
- `git clone <원격 저장소 주소>`

- git clone을 통해 생성된 로컬 저장소는 `git init`과 `git remote add`가 이미 수행되어 있음



2. git pull

- 원격 저장소의 변경 사항을 가져와서, 로컬 저장소를 업데이트하는 명령어
- 로컬 저장소와 원격 저장소의 내용이 완전히 일치하면 git pull을 해도 변화가 일어나지 않음
- `git pull <저장소 이름> <브랜치 이름>`











