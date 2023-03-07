# 설치
1. brew install mysql
2. mysql.server start
3. mysql_secure_installation
4. 순서대로 아래 질문이 나오면
```
비밀번호 복잡도 검사 과정 (n)
비밀번호 입력 & 확인
익명 사용자 삭제 (y)
원격 접속 허용하지 않을 것인가? (y)
test DB 삭제 (n)
previlege 테이블을 다시 로드할 것인지 (y)

설정을 마치면 All done! 메세지가 출력됩니다.
```

<hr>

# 실행 및 종료법

## 실행
1. mysql.server start
2. mysql -r root -p 비밀번호

<br>

## 종료
1. \q
2. mysql.server stop

<hr>

# 버전 화긴
- mysql -V or mysql --version
