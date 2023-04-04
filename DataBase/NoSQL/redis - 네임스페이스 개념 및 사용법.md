# Namespace
Redis의 네임스페이스란 Database를 말한다. 쉽게 말해 MySQL은 하나의 클러스터 안에 여러개의 DataBase를 생성하여 용도를 나눠 사용할 수 있듯이 Redis는 네임스페이스를 나눠 Database를 구분한다. 네임스페이스는 숫자로 구분되며, 설치되면 접속해서 사용할 수 있는 디폴트 네임스페이스는 0이다.

<br>

## Select 명령으로 네임스페이스 선택
Select 명령으로 네임스페이스를 선택할 수 있으며 Prompt 끝에 [숫자]로 표시된다.
<img width="230" alt="image" src="https://user-images.githubusercontent.com/74396651/229717481-09a7e7b5-71fa-4fe3-be0c-97d0822ee496.png">

<br>

## Move 명령으로 키 값을 다른 네임스페이스로 이동
- 2번 네임스페이스에 {kim : seongho} 삽입
<img width="230" alt="image" src="https://user-images.githubusercontent.com/74396651/229717911-97747eac-95e3-4d0a-a85e-cb35cfaa07fa.png">

- 1번 네임스페이스로 kim 이등
- 성공시 1 반환
<img width="255" alt="image" src="https://user-images.githubusercontent.com/74396651/229718135-035badea-12a6-4ddc-8105-21f968af8c20.png">

<br>

## Expiry로 만료시간 지정
Redis는 빠른 액세스가 필요한 데이터 캐시에 많이 사용하기 때문에, 특정시간이 경과 되면 Expiry가 된 Key-Value 데이터를 Redis가 자동으로 삭제하여 전체 Key Set이 무한히 커지는 것을 방지합니다. 200GB가 넘어가면 장애가 난다는 이야기도 있습니다.

<img width="270" alt="image" src="https://user-images.githubusercontent.com/74396651/229736301-59c16cf9-7d3c-4335-b4aa-97feba3d6747.png">

### SETEX를 통해 한번에 설정

<img width="297" alt="image" src="https://user-images.githubusercontent.com/74396651/229736601-8110ab60-b583-44a2-88d7-4d08a13f3771.png">

### TTL 명령으로 생존시간 확인
<img width="314" alt="image" src="https://user-images.githubusercontent.com/74396651/229736753-9d18e064-8305-4329-8741-79a48a2bcccd.png">

<br>

## 그 외 명령어
- RENAME : key의 이름을 변경
- TYPE : key의 타입을 판단
- DEL : key-value 삭제
- FLUSHDB : 현재 네임스페이스의 모든 key를 삭제
- FLUSHALL : 현재 redis안의 모든 key를 삭제






