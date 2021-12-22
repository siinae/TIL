



# 01. CLI #

1. `CLI`란?

​	   : Command Line Interface, 터미널을 통해 사용자와 컴퓨터가 상호작용하는 방식



2. CLI와 GUI

   : Graphic User Interface, 그래픽을 통해 사용자와 컴퓨터가 상호 작용하는 방식

   --> 결국, 화면에 나타나는 모습만 다를뿐 CLI와 GUI는 같은 일을 함 

   

3. 명령어

- touch: 파일을 생성
- mkdir: 폴더를 생성
- ls: 현재 작업 중인 디렉토리의 폴더/파일 목록을 보여줌
- mv: 폴더/파일을 다른 폴더 내로 이동 하거나 이름을 변경
- cd: 현재 작업 중인 디렉토리를 변경
- rm: 폴더/파일 지우는 명령어
- start, open: 폴더/파일을 여는 명령어(windows는 start/MAC은 open)



4. 단축키

- 위,아래 방향키 : 과거에 작성했던 명령어 조회
- tab : 폴더/파일 이름 자동 완성
- ctrl + a : 커서가 맨 앞으로 이동
- ctrl + e : 커서가 맨 뒤로 이동
- ctrl + w : 커서가 앞 단어를 삭제
- ctrl + l : 터미널 화면을 깨끗하게 청소 (스크롤 올리면 과거 내역 조회 가능)
- ctrl + insert : 복사
- shift + insert : 붙여넣기







---





# 02. 마크업(Markup) #

- 마크(Mark)로 글의 역할을 정하는 것(일종의 표시)

--> 디자인을 위해 임의대로 역할을 변경할 수 없음 ex. 본문의 내용을 제목으로 표시할 수 없음

- HTML의 'M' = Markup, 즉 HTML은 마크업 언어





---





# 03. 마크다운(Markdown) #



#### 1. 제목 ####  



# 제목 1

## 제목 2

### 제목 3

#### 제목 4

##### 제목 5

###### 제목 6

---

#### 2. 목록 ####

(1) 순서가 없는 목록

- 목록 1
- 목록 2
- 목록 3
- 과일
  - 수박
  - 참외
  - 바나나

(2) 순서가 있는 목록

1. 목록1
2. 목록2
3. 목록3
   1. 목록1
   2. 목록2
      1. 목록2-1

---

#### 3. 강조(스타일링) ####

​		(1) 기울임(이탤릭체): *글자* , _글자_

​		(2) 굵게(볼드체): **글자**, __글자__

​		(3) 취소선: ~~글자~~ 	

---

#### 4. 코드 #### 

(1) 인라인(Inline) 코드(=한줄)

파이썬에서는 `print("Hello World!")` 라고 쓸 수 있습니다.



(2)  블록코드(Block)(=여러줄)

```python
for i in range range(10):
	print(i)
```

---



#### 5. 수평선 ####

-,*,_ 3번 연속 작성

---

***

___





---



#### 6. 표(table) ####

| 동물   | 다리개수 | 종     |
| ------ | -------- | ------ |
| 사자   | 4개      | 포유류 |
| 원숭이 | 2개      | 포유류 |
| 앵무새 | 2개      | 조류   |
|        |          |        |
|        |          |        |

---



#### 7. 문자열 이스케이프(앞에 \붙이기) ####

\`print()\`



---

# 04. 깃(Git) 기초

1. Git을 이용한 버전관리 작성자 등록(한번만)

​		git config --global user.name sinae

​		git config --global user.email o3o9122@naver.com



2. Git 기본명령어

(1) 기본 저장소

- Working Directory(Working Tree)

  : 사용자의 일반적인 작업이 일어나는 곳

- Staging Area(=Index)

​		: 커밋을 위한 파일 및 폴더가 추가되는 곳

- Repository

​		: staging area에 있던 파일 및 폴더의 변경사항(커밋)을 저장하는 곳



(2) `git init`

-현재 작업 중인 디렉토리(폴더)를 Git으로 관리한다는 명령어



(3) `git status`

-Working Directory와 Staging Area에 있는 파일의 현재 상태를 알려주는 명령어

1)Untracked: Git이 관리하지 않는 파일(한번도 Staging Area에 올라간 적 없는 파일)

2)Tracked: Git이 관리하는 파일

​		a. Unmodified: 최신상태

​		b. Modified: 수정되었지만 아직 Staging Area에는 반영하지 않은 상태

​		c. Staged: Staging Area에 올라간 상태



(4)`git add`

- Working Directory -> Staging Area
- Git이 해당 파일을 추적(관리)할 수 있도록 만듦
- Staging Area에 있는 파일부터 버전관리의 대상이 됨
- Untracked, Modified -> Staged 로 상태 변경
- git add . --> 현재 만들어져 있는, 수정한 파일 전부 Staging Area로 올림(=git add --all)
- git add *.txt --> txt파일 전부 , git add *.py --> py파일 전부

​	ex. git add a.txt



(5)`git commit`

- Staging Area -> Commits(버전)
- 커밋 메세지는 현재 변경 사항들을 잘 나타낼 수 있도록 의미 있게 작성하는 것을 권장
- 각각의 커밋은 SHA-1 알고리즘에 의해 반환된 고유의 해시 값을 ID로 가짐

ex. git commit -m "first commit"



(6)`git log`

- 현재 Git이 관리하는 파일의 상태
- 커밋의 내역(ID, 작성자, 시간, 메세지 등)을 조회할 수 있는 명령어-->노란색 알파벳+숫자
- 옵션

  - --oneline: 커밋 내역을 한 줄로 축약해서 보여줌
  - --graph: 브랜치와 머지 내역을 그래프로 보여줌
  - --all: 현재 브랜치를 포함한 모든 브랜치 내역 보여줌
  - --reverse: 커밋 내역의 순서를 반대로 보여줌(최신이 가장 아래)
  - -p: 파일의 변경 내용도 같이 보여줌
  - -2: 원하는 갯수 만큼의 내역을 보여줌(2말고 임의의 숫자 사용 가능)




---



**## Git 기초 실습 - 문제풀기** 





\> 아래에 있는 각각의 문제에 대해 답과 이유를 작성하시오.

\> 한 문제를 풀 때 마다 커밋을 저장하시오. 커밋 메시지는 "solve 문제번호 problem"의 형태로 저장하시오.





\1. Git과 Github는 같다. (맞으면 O, 틀리면 X)



  \- 답 : x

  \- 이유 : Git은 로컬에서 버전관리를 하고, Github는 그 버전을 올리는 리모트(원격) 저장소이니까요.



  



\2. 터미널 명령어 `cd .`은 현재 위치의 부모 폴더로 이동하라는 의미이다. (맞으면 O, 틀리면 X)



  \- 답 : x

  \- 이유 : cd . 은 현재로 이동하라는 의미(변화x), 부모 폴더로 이동하라는 명령어는 'cd ..'이다





\3. 마크다운 문법에서 글씨의 크기를 키우고 싶다고해서 본문을 제목으로 지정하면 안된다. (맞으면 O, 틀리면 X)

  \- 답 : o

  \- 이유 : 마크다운은 글에 "역할"을 부여한다.  





\4. Git의 3가지 공간에는 Working Directory, Staging Area, Commits이 있다. (맞으면 O, 틀리면 X)

  \- 답 : o

  \- 이유 : Working Directory -> Stage Area -> Commits 





\5. Commit ID는 중복 가능하다. (맞으면 O, 틀리면 X)

  \- 답 : x

  \- 이유 : Commit ID는 SHA1 알고리즘을 통한 해시값 --> 고유하다. 절대 겹치지 않음 



