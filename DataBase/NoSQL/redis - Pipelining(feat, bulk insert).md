# Redis
Redis는 고성능 key-value Store지만 Redis는 client-server 모델과 요청/응답 프로토콜을 사용하는 TCP 서버이다. 일반적으로 요청이 다음 단계를 통해 수행된다.
- 클라이언트는 서버에 쿼리를 보내고 일반적인 차단 방식으로 소켓에서 서브 응답을 읽는다.
- 서버는 명령을 처리하고 클라이언트에게 응답을 다시 보낸다.

### 명령 시퀀스
<img width="218" alt="image" src="https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/0d1e1117-89a3-4c63-9ee9-c4c436fc698d">

클라이언트와 서버는 네트워크 링크를 통해 연결된다. 이러한 링크는 매우 빠르거나(루프백 인터페이스) 매우 느릴 수 있다.(두 호스트 사이에 많은 홉이 있는 인터넷을 통해 설정된 연결). 네트워크 대기 시간이 무엇이든 패킷이 클라이언트에서 서버로 이동하고 응답을 전달하기 위해 서버에서 클라이언트로 다시 이동하는 데는 시간이 걸린다.

이 시간을 RTT(Round Trip Time)이라고 한다. 클라이언트가 연속적으로 많은 요청을 수행해야 할 때(예를 들어 동일한 목록에 많은 요소를 추가하거나 많은 키로 데이터베이스를 채우는 경우) 이것이 성능에 어떤 영향을 미칠 수 있는지 쉽게 알 수 있다. 예를 들어 RTT 시간이 250밀리초인 경우(인터넷을 통한 링크가 매우 느린 경우) 서버가 초당 100,000개의 요청을 처리할 수 있더라도 초당 최대 4개의 요청을 처리할 수 있다.

사용된 인터페이스가 루프백 인터페이스인 경우 RTT는 훨씬 더 짧으며 일반적으로 1밀리초 미만이지만 연속해서 많은 쓰기를 수행해야 하는 경우에는 이 값도 추가된다.

이러한 병목을 개선하기 위해, Redis에서는 pipelining API를 제공한다. 이를 통해 클라이언트는 복수 개의 작업을 쌓아 한 번에 전송(request)할 수 있게 됩니다. 따라서 응답을 전혀 기다리지 않고 여러 명령을 한꺼번에 서버로 보낼 수 있고, 응답을 한번에 읽을 수 있습니다.

# Pipelining
Redis 명령을 일괄 처리하여 왕복 시간을 최적화하는 방법.

Redis 파이프라이닝은 개별 명령에 대한 응답을 기다리지 않고 한 번에 여러 명령을 실행하여 성능을 향상시키는 기술이다.

클라이언트가 이전 응답을 아직 읽지 않은 경우에도 새 요청을 처리할 수 있도록 요청/응답 서버를 구현할 수 있다. 이렇게 하면 응답을 전혀 기다리지 않고 서버에 여러 명령을 보내고 마지막으로 한 단계로 응답을 읽을 수 있다.

# 직렬화 역직렬화

### 직렬화
- 객체를 데이터 스트림으로 만드는 것.
- 객체에 저장된 데이터를 스트림에 쓰기 위해 연속적인 데이터로 변환하는 것
- 객체를 다른 곳으로 전송하거나 저장하기 위해서 사용.
- 객체의 필드를 바이너리 형식이나 바이트스트림으로 바꾸는 작업. 직렬화 되는 대상은 객체의 인스턴스 변수
### 역직렬화
- 직렬화의 반대로 다시 객체의 형태로 만드는 것

### Redis의 데이터 저장 형식은 byte array형태이다. 직렬화가 필요하다

### Spring Data Redis 직렬기
- JdkSerializationRedisSerializer
  - RedisCache와 RedisTemplate에서 default로 사용됨
- StringRedisSerializer
  - String형태로 저장
- JacksonJsonRedisSerializer
  - Json형태로 저장
  - 객체 클래스를 지정해주어야 한다
- GenericJackson2JsonRedisSerializer
  - Json형태로 저장
  - 객체 클래스를 지정해주지 않아도 된다. 단 직렬화되는 Dto가 같은 패키지 내에 있어야 한다.

## redis bulk insert code
```java

    public void bulkInsertForMenuList(String key, List<ChickenMenuInfoResDto> menuList){
        RedisSerializer<String> stringSerializer = redisTemplate.getStringSerializer();
        RedisSerializer<String> valueSerializer = (RedisSerializer<String>) redisTemplate.getValueSerializer();

        redisTemplate.executePipelined((RedisCallback<Object>) connection -> {
            byte[] serializeKey = stringSerializer.serialize(key);
            String value = parseObjectToString(menuList);
            byte[] serializeValue = valueSerializer.serialize(value);
            connection.set(serializeKey, serializeValue);

            return null;
        });
    }

```
