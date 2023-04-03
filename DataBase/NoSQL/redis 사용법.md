# Redis 사용법

## 데이터 처리(명령어)
![image](https://user-images.githubusercontent.com/74396651/229422217-0771d082-578a-4132-a2cd-0589567cc33c.png)




## 다운 및 실행
```
brew install redis (Mac Redis 설치)
redis-server (Redis Server 실행)
redis-cli (Redis Client 접속)
quit(Redis Client 종료)

brew services start redis   (Redis 서비스 실행)
brew services stop redis    (Redis 서비스 중지)
brew services restart redis (Redis 서비스 재시작)

flushAll (Redis 모든 Key 삭제)
```
<img width="608" alt="image" src="https://user-images.githubusercontent.com/74396651/229424909-9f703dee-601e-46ea-b943-2174d46fdb06.png">

## info 명령어
info 명령은 레디스가 실행된 이후 각종 통계와 설정 정보를 출력
- Server
  - 실행중인 레디스 서버의 실행 정보 
- Clients
  - 서버와 연결된 클라이언트들의 통계 정보  
- Memory
  - 메모리 사용 정보 및 메모리 통계 정보 
- Persistence
  - 영구저장소와 관련된 저장 정보 
- Stats
  - 명령 수행과 저장된 키에 대한 통계 정보
- Replication
  - 현재 동작 중인 복제 정보
- CPU
  - CPU 사용률 통계 정보
- Keyspace
  - 데이터베이스별로 저장된 키 정보

