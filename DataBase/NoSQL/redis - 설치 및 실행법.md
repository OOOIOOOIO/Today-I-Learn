# Redis 설치 및 


## 설치
- brew install redis (Mac Redis 설치)

## 실행
- Redis Server 실행 명령어
  - redis-server

<img width="569" alt="image" src="https://user-images.githubusercontent.com/74396651/231169862-450cab49-7f2d-4b15-b42c-8b653ffc4161.png">

- Redis Client 접속 명령어
  - redis-cli

## 종료
- Redis Client 종료 명령어
  - quit
- Redis Server 종료 명령어
  - shutdown
    - 그냥 shutdown 하면 disk에 저장됨
    - shutdown nosave 해야 저장이 안된다.

### 그냥 shutdown
<img width="565" alt="image" src="https://user-images.githubusercontent.com/74396651/231170077-98464d2f-564a-4a43-9cab-b30186a560a6.png">

### shutdown nosave
<img width="563" alt="image" src="https://user-images.githubusercontent.com/74396651/231170247-1fdca63e-75ee-4aa0-9865-e7bd840de82e.png">

## mac 명령어(참고)
brew services start redis   (Redis 서비스 실행)
brew services stop redis    (Redis 서비스 중지)
brew services restart redis (Redis 서비스 재시작)

## 모든 key 삭제하기
- flushAll 

<hr>

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









