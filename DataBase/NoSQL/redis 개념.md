# Redis란
> 레디스는 고성는 키-밸류 저장소로서 문자열, 리스트, 해시, 셋, 정렬된 셋 형식의 데이터를 지원하는 NoSQL이다.
Redis는 Memcached와 비슷한 캐시 시스템으로서 동일한 기능을 제공하면서 영속성, 다양한 데이터 구조와 같은 부가적인 기능을 지원하고 있다. 레디스는 모든 데이터를 메모리에 저장하고 조회한다. 즉, 인메모리 데이터베이스이다. 이 말만 들으면 Redis에 모든 데이터를 메모리에 저장하는 빠른 DB가 다라고 생각할지도 모른다. 하지만 빠른 성능은 레디스의 특징 중 일부분이다. 다른 인메모리 디비들과의 가장 큰 차이점은 레디스의 다양한 자료구조이다.

<br>

![image](https://user-images.githubusercontent.com/74396651/229419629-be4c3a32-673a-4031-a64f-6b3ccf4126c4.png)

- 이렇게 다양한 자료구조를 지원하게 되면 개발의 편의성이 좋아지고 난이도가 낮아진다는 장점이 있다.
- 예를들어, 어떤 데이터를 정렬을 해야하는 상황이 있을 때, DBMS를 이용한다면 DB에 데이터를 저장하고, 저장된 데이터를 정렬하여 다시 읽어오는 과정은 디스크에 직접 접근을 해야하기 때문에 시간이 더 걸린다는 단점이 있다. 하지만 이 때 In-Memory 데이터베이스인 Redis를 이용하고 레디스에서 제공하는 Sorted-Set이라는 자료구조를 사용하면 더 빠르고 간단하게 데이터를 정렬할 수 있다.

<br>

## Redis 특징

![image](https://user-images.githubusercontent.com/74396651/229419796-26fe1c2f-28a5-4c5a-a923-1f4b814ae567.png)

> NoSQL로서 Key-Value 타입의 저장소인 레디스(Redis, Remote Dictionary Server)의 주요 특징은 아래와 같다.

- 영속성을 지원하는 인메모리 데이터 저장소
- 읽기 성능 증대를 위한 서버 측 복제를 지원
- 쓰기 성능 증대를 위한 클라이언트 측 샤딩(Sharding) 지원
  - Sharding이란 파티셔닝과 동의어이다.
- 다양한 서비스에서 사용되며 검증된 기술
- 문자열, 리스트, 해시, 셋, 정렬된 셋과 같은 다양한 데이터형을 지원. 메모리 저장소임에도 불구하고 많은 데이터형을 지원하므로 다양한 기능을 구현

<br>

## Redis 영속성
> 레디스는 지속성을 보장하기 위해 데이터를 DISK에 저장할 수 있습니다. 서버가 내려가더라도 DISK에 저장된 데이터를 읽어서 메모리에 로딩한다.

Redis는 데이터를 DISK에 저장하는 방식은 크게 두 가지 방식이 있다.

- RDB(Snapshotting) 방식
  - 순간적으로 메모리에 있는 내용을 DISK에 전체를 옮겨 담는 방식
- AOF (Append On File) 방식
   - Redis의 모든 write/update 연산 자체를 모두 log 파일에 기록하는 형태

<br>

## Redis 구조
- Redis Topology
  - Redis는 Master-Slave 형태로 데이터를 복제해서 운영할 수 있다.
  - Master-Slave 간 복제는 Non-Blocking 상태로 이루어진다.
- Redis Sharding
  - Redis에서 데이터를 샤딩하여 Read 성능을 높일 수 있다.
- Rdeis Cluster
  - Redis는 클러스터링을 지원하기에 실무에서는 주로 클러스터로 묶어서 가용성 및 안정성 있는 캐시 매니저로 사용하고 있다.

<br>

## Redis 스키마
사용자의 이메일, 닉네임, 최근 로그인 시간을 저장해보자.
- user:userId:email:polite159@gmail.com(문자열)
- user:userId:nickname:polite159(문자열)
- user:userId:lastLogin:2023-04-03(문자열)

- 스키마를 활용하면 사용자 아이디에 해당하는 userId만 알아도 연결된 데이터인 email, nickname, lastLogin도 알 수 있게 된다.








   
   
   
