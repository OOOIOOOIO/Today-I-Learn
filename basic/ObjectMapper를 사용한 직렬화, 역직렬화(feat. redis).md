# ObjectMapper를 사용한 직렬화, 역직렬화(Feat. redis)

## ObjectMapper란

<br>
<hr>
<br>

## 직렬화와 역직렬화

<br>
<hr>
<br>

## 문제점

### Jackson2JsonRedisSerializer, GenericJackson2JsonRedisSerializer(ObjectMapper) 사용시 에러사항
1. Jackson2JsonRedisSerializer 특정 클래스 혹은 Object, class 타입 리턴 못받음
  - nested exception is org.springframework.data.redis.serializer.serializationexception발생
2. GenericJackson2JsonRedisSerializer class 타입 리턴 받지만 LinkedHashMap
3. 
4. 

<img width="884" alt="image" src="https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/90a5873b-aebb-4cf3-87df-9932aef518d6">

<br>
<hr>
<br>

## 해결방안 : StringRedisSerializer 사용 및 ObjectMapper를 사용한 직렬화 및 역직렬화


<br>
<hr>
<br>

## Code

#### Service

<img width="1106" alt="image" src="https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/e206e19f-3fd4-4346-b59a-69ca0a21ce0b">

<br>
<hr>
<br>

#### RedisUtil

#### 이전 코드
<img width="769" alt="image" src="https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/b340b7ac-74c1-4e58-bfbd-fb476c168978">

#### 해결 후 코드

<img width="763" alt="image" src="https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/59ea03bc-938f-48ad-b8c7-d7e47f7f756b">

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/186f0bad-1606-47f5-b49c-f9324cbf08a1)

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/49b1f6ac-925e-4c4f-ba0a-13d38af78536)

<img width="1602" alt="image" src="https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/51a815ab-7402-4f27-b474-d0e765da8b6a">

<br>
<hr>
<br>

## 후...
nested exception is org.springframework.data.redis.serializer.serializationexception을 해결하려고 Jackson2JsonRedisSerializer, GenericJackson2JsonRedisSerializer, hashValue 뭐가 문제지 삽질하다가 레디스와 자바 타입이 다르니 꼬이는 것 같은데... 흠 하다가 GenericJackson2JsonRedisSerializer에 ObjectMapper로 날짜를 파싱하는 블로그를 보고 아 그냥 String으로 넣고 Java type으로 파싱하자!가 떠올라 ObjectMapper를 사용해 해결해 보았다! 유레카였다!!! 해결할 땐 많이 화났지만 해결하니 재밌다 히히!




