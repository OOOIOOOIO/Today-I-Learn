# MySQl 접속 및 사용자 추가, 데이터 베이스 추가

- ### 접속
   - mysql -u root -p
   - mysql -u 사용자 -p

- ### 사용자 목록 보기
   - use mysql;
   - select host, user, plugin from user;

- ### 사용자 추가
   - create  user 사용자ID@호스트(localhost) identified by '비밀번호'; 
   - create  user 사용자ID@% identified by '비밀번호'; --> 기존 사용자의 외부에서 접근을 허용

- ### 사용자 삭제
   - delete from user where user ='사용자ID';

- ### DataBase 목록 보기
   - show databases;
   
- ### DataBase 생성
   - create database DB명;

- ### DataBase 삭제
   - drop database DB명;

- ### DataBase 사용
   - user databse명;

<br>
<hr>
<br>

# 사용자 권한 부여

- MySQL은 사용자 이름, 비밀번호, 접속 호스트로 여러분을 인증한다. 
- MySQL은 로그인을 시도하는 위치가 어디인가 하는 것도 인증의 일부로 간주한다.
- MySQL 에서 사용자 계정을 추가하고 권한을 추가하거나 제거하는 데 GRANT 와 REVOKE 명령을 사용하기를 권장한다. 
- 사용자에게 허가된 것을 확인하려면 SHOW GRANTS 를 사용한다.
- 모든 원격지에서 접속 권한 추가 host에 '200.100.%' 로 하면 IP주소가 200.100.X.X 로 시작되는 모든 IP에서 원격 접속을 허용한다.
- host에 '200.100.100.50' 으로 하면 IP주소가 200.100.100.50 인 곳에서만 원격 접속을 허용한다.

<br>
- ### 계정이 존재한다면 identified by X
- ### 계정이 이미 존재 하는데 'identified by '비밀번호' 부분을 추가하면 비밀번호가 변경된다
   - GRANT ALL PRIVILEGES ON DB명.테이블 TO 계정아이디@host IDENTIFIED BY '비밀번호';
   - GRANT ALL privileges ON DB명.* TO 계정아이디@locahost IDENTIFIED BY '비밀번호';
   - GRANT ALL privileges ON DB명.* TO 계정아이디@'%' IDENTIFIED BY '비밀번호';
   - grant all privileges on DB명.* to userid@'%' identified by '비밀번호' ; 


- ### user 에게 test 데이터베이스 모든 테이블에 대한 권한 부여 및 비밀번호 변경
  - grant all privileges on test.* to userid@localhost identified by '비밀번호';

- ### user 에게 test 데이터베이스 모든 테이블에 select, insert, update 권한 부여
   - grant select, insert, update on test.* to user@localhost identified by '비밀번호';

- ### user 에게 test 데이터베이스 모든 테이블에 select, insert, update 권한 부여
   - grant select, insert, update on test.* to user@localhost;   -- 패스워드는 변경없이 권한만 부여하는 경우

- ### user 에게 모든 데이터베이스 모든 테이블에 권한 부여// 전역 권한은 모두 광범위한 보안문제가 수반되므로 권한을 허용하는 경우 신중해야 함
   - grant all privileges on *.* to user@localhost identified by '비밀번호' with grant option;

- ### 변경된 내용을 메모리에 반영(권한 적용)
   - flush privileges;     

<hr>

# 사용자 권한 확인
- show grants for 사용자Id@localhost or % or 특정 ip

# 사용자 권환 제거 및 계정 삭제
- ### 모든 권한 삭제
   - revoke all on DB명.테이블명 from 사용자ID;

- ### 사용자 계정 삭제
   - drop user 사용자ID@호스트 or %;

<br>
<hr>
<br>


## cmd 창에서 사용자와 db 만들고 workbench로 가서 connection 생성해주면 된다
