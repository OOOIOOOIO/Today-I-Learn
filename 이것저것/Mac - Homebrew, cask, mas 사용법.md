# 개요
- Homebrew(Formulae) : 개발관련 패키지 설치환경 구성
   - java, awscli, curl, git, gradle, maven, mysql, node ... cask, mas
- cask : 웹사이트에서 받을 수 있는 어플리케이션 설치환경 구성
   - 크롬, IntelliJ, java(openJdk) 등...
- mas : 앱스토어에서 받을 수 있는 어플리케이션 설치환경 구성
   - 카카오톡, 슬랙, 마그넷 등...

# Homebrew
> Homebrew는 MacOS용 패키지 관리자이다! 터미널에서 명령어를 작성하여 자신이 필요한 프로그램을 설치, 삭제, 업데이트를 손쉽게 관리할 수 있다.(yum, apt-get과 같다고 생각하면 편하다!)

<br>
<hr>
<br>

# 설치법
1. 터미널 열기
2. 아래 명령어 실행하기(command + c = 복사) 혹은 [홈페이지](https://brew.sh/index_ko)로 가서 복사하여 실행
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
3.쭉 뭐가 실행되고 "Press RETURN to continue or any other key to abort"가 나오면
"return" 키를 눌러준다.
4. 이후 "Password"를 입력하라고 나오는데, 이 때 본인의 맥 비밀번호를 작성한 후 "return"을 누르면 된다.
5. 아무 Error 없이 "Installation successful!"이 노출된다면 다운로드에 성공한 것이다. 
6. 이후 brew 명령어를 사용하려할 때 Path 에러가 난다면 다음과 같이 해결하자
```
1. /opt/homebrew/bin/brew doctor

2. echo 'export PATH="/opt/homebrew/bin:$PATH"' >> ~/.zshrc

3. 터미널 재시작

4. /Users/ksh(내 루트 폴더)/.zshrc 접속

5. 
export HOME_BREW="/opt/homebrew/bin"
export PATH=$PATH:$HOME_BREW

로 수정(사실 안해도 잘 돌아갔음)

6. 터미널 재시작 후 brew config로 확인

```

<br>
<hr>
<br>

# cask 설치
1. 터미널에 brew instal cask 실행
2. brew list 실행 -> 목록에 cask가 있다면 성공!

# mas 설치
1. 터미넬어 brew install mas 실행
2. brew list 실행 -> 목록에 mas가 있다면 성공!

<br>
<hr>
<br>

# 크롬 설치해보기
1. brew search chorme
2. 리스트에 google-chrome이 찾기
3. brew install --cask google-chorme 실행하여 설치
4. "google-chrome was successfully installed!"가 나오면 성공
5. chrome은 application이라 Applications에 들어감

# 카카오톡 설치해보기
1. mas search kakaotalk
2. kakaotalk에 맞는 번호 확인
3. mas install 번호 실행
4. 근데 카톡은 intelld이라 R~뭐시기 깔아야함

<br>
<hr>
<br>
<br>
<br>


[완전 참고](https://velog.io/@franc/Homebrew%EB%A1%9C-%EB%82%98%EB%A7%8C%EC%9D%98-Mac-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0)

<br>

[Path 오류](https://cloudest.oopy.io/posting/043)

















