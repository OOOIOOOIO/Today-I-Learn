# intellij
1. brew install --cask intellij-idea bere

# java(jdk11)
1. brew tap adoptopenjdk/openjdk
2. brew search jdk
3. brew install --cask adoptopenjdk11

# git
1. brew install git
2. git --version
3. brew info git

## git ssh 등록
1. cat ~/.ssh/id_rsa.pub 실행 -> 없으면 생성해야됨
2. ssh-keygen -> ssh키 생성
3. 비밀번호 생성
4. cd ~./.ssh -> 이동
5. cat id_rsa.pub -> 파일 읽기
6. 위에서 읽은 파일 복사
7. github 홈페이지 이됭
8. Settings 들어가기
9. SSH and GPG Keys 클릭
10. New SSH Key 클릭
11. 복사한 키 넣고 저장
12. 끝!
