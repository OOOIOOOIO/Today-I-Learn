# Git

## Git
- 버전관리(여러 파일을 하나의 버전으로 묶어 관리하는 것) 시스템의 한 종류

<br>

## 버전관리 시스템의 종류
- 클라이언트 - 서버 
   - CVS, SVN

-분산 모델
   - 하나의 중앙 서버가 존재하지만 여러 클라이언트들은 각자의 컴퓨터 저장소에 전체 사본을 가지고 와서 작업하는 방식
   - git

<br>

## git의 장점
- 동시에 작업하는 사람들과 소스코드를 주고받을 필요가 없다.
- 같은 파일을 여러명이 동시에 병렬 개발을 할 수 있다.
- 변동 과정을 체계적으로 관리할 수 있고, 언제든지 지난 시점의 버전으로 되돌릴 수 있다.
- 인터넷이 연결되지 않은 곳에서도 개발을 진행할 수 있다.
- 중앙 서버의 데이터가 유실되어도 쉽게 다시 복구할 수 있다.

<br>

## git 시작하기

```

      구글에 git 설치 검색 --> https://git-scm.com/ --> 좌측에 Downloads
      --> 운영체제에 맞는것 다운로드(setup) --> 기본 설정으로 설치(무지성 다음) 
      --> cmd 켜서 git 명령어 실행 시 알수없는 메세지들 나오면 성공

```

<br>

## github
-git으로 버전관리한 코드를 올릴 수 있는 클라우드 서비스이다. 단순한 저장만 하는것이 아니라 유저들과 함께 코드를 공유하고 온라인으로 하나의 프로그램을 같이 제작할 수 있게 만들어준다.

<br>

## Git Bash 명령어

- 현재 위치 확인하기
   - pwd

- 프로젝트 폴더 내에 무엇이 있는지
   - dir

- 프로젝트 폴더 내에 로컬 저장소 생성
   - git init

- 프로젝트 폴더 내 상태 보기
   - git status


- github 저장소 만들기
   - 왼쪽 메뉴의 Create Repository 클릭

- 로컬 저장소에 github 저장소 주소 설정하기
   - git remote add origin https://github.com/깃허브아이디/레포지토리이름.git


- 현재 저장소 주소 확인하기
   - git remote -v


- git에 버전 관리할 파일을 선택해서 add(stage에 올림)
   - git add 파일명
   - git add . : 모든 파일 올리기

- 하나의 버전으로 만들어서 관리(commit)
   - git commit -m "커밋할 메세지"

```      
	※ commit 에러 발생시
		Author identity unknown
		*** Please tell me who you are.
		Run
		git config --global user.email "you@example.com"
		git config --global user.name "Your Name"
		to set your account's default identity.
		Omit --global to set the identity only in this repository.
		fatal: unable to auto-detect email address
		(got 'admin@컴퓨터이름.(none)')

	※해결 방법
		git config --global user.email "깃허브이메일주소"
		git config --global user.name "깃허브이름"
```


- 만든 버전(커밋)을 github에 올리기
   - git push -u origin 브랜치이름
   - git push -u origin master 또는 git push -u origin main

- github에 올라와 있는 파일 전부 내려받기
   - git clone 깃허브주소

=========================================================================

# Staging 뭐시기 공부해서 다시 정리하기

- commit 취소하기 
git reset : 전체 add 파일 취소
git reset HEAD 파일명 : 특정 add 파일 취소
git reset HEAD^^^^^ : "^" 숫자 만큼 최신 커밋 취소


- 기존에 파일이 있는 경우 업데이트 된 것을 받아오기
git pull

- branch 확인하기
git branck

- branck 생성하기
git branck 생성할 브랜치

- branch 변경하기
git checkout 생성한 브랜치




=========================================================================

# Pull Request와 Merge

commit을 한다고 최종 코드가 수정되는 것은 아닙니다.
개인이 commit을 했으면, 관리자가 이 코드를 리뷰하고 바꿀것이 있으면 수정해달라고 다시 요청해야하기 때문입니다. 


1) Pull Request 발행 (Review 의뢰자)

github에 접속 후, 원격저장소에 들어가서 해당 commit의 pull request 버튼을 누르면 Reviewer에게 풀리퀘스트 메시지 전송



2) Review & Comment (Review 수행자)

리뷰 후 comment 할 것이 있으면 comment 버튼 클릭



3) Comment 대응 (Review 수행자)

local에서 코드 수정 후 원래와 같은 방식으로 commit 수행

$ git add .

$ git commit -m "커밋 메시지"

$ git push



4) Review 및 병합 (Review 수행자)

리뷰 후 최종 결과 만족 시 병합(merge) → github에서 pull request merge 버튼 클릭







