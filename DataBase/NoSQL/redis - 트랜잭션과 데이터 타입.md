# 트랜잭션과 데이터 타입
[Redis 공식 레퍼런스(명렁어)](https://redis.io/commands/)

## 기본 연산

### SET, GET
- SET : 키 값을 추가할 수 있다. 항상 KEY-VALUE로 된 두 개의 매개변수를 필요로 한다.
- GET : SET으로 입력한 값을 일을 떄 사용한다. KEY값을 통해 읽는다.

<img width="270" alt="image" src="https://user-images.githubusercontent.com/74396651/229740356-ef87d3a6-1120-4483-b269-096634591c1f.png">

<br>

### MSET, MGET
네트워크 트래픽을 줄이기 위해 mget 명령으로 여러 쌍의 key-value를 불러올 수 있다. 리스트로 반환한다.

<img width="324" alt="image" src="https://user-images.githubusercontent.com/74396651/229752907-c4502394-8ac8-4d2e-9d88-b428e2c9df0f.png">


<br>

### 숫자 연산
Redis는 모든 값을 문자열로 저장한다. 그러나 문자열로 된 숫자를 정수(Integer)로 인식하고 처리해주는 연산을 제공한다.
- incr : 숫자 값에 1 증가
- decr : 숫자 값으 1 감소
- incrby : 지정한 정수 더함
- decrby : 지정한 정수 뺌

<img width="238" alt="image" src="https://user-images.githubusercontent.com/74396651/229741277-effa9f7b-7d0d-468d-a52d-60af20b31134.png">

<img width="256" alt="image" src="https://user-images.githubusercontent.com/74396651/229741437-515a12c0-afec-4a85-872b-64ae6c078598.png">

<br>
<hr>
<br>


## 트랜잭션
- multi : 여러 명령을 하나의 블록으로 묶어두고 queue에 쌓아둔다.
- exec : multi에 쌓아둔 queue를 실행한다.
- discard : multi queue에 쌓아둔 트랜잭션을 중지한다.

### multi-exec
<img width="292" alt="image" src="https://user-images.githubusercontent.com/74396651/229744539-42682826-ba30-4e80-ba48-abddf6aceab4.png">

### multi-discard 
<img width="454" alt="image" src="https://user-images.githubusercontent.com/74396651/229744820-f501b483-5817-4e63-891e-7413008c87c5.png">

### multi-discard-exec
discard 명령을 실행 후에 exec를 실행하면 queue 쌓였던 명령들이 실행되지 않는다. 트랜잭션을 취소하는 개념인데, RDBMS의 commit 전에 rollback과 매커니즘은 다르지만 비슷한 개념으로 보면 됩니다.
<img width="273" alt="image" src="https://user-images.githubusercontent.com/74396651/229745016-b18a2401-7790-4408-b670-a659b8584a4b.png">

<br>
<hr>
<br>

## 데이터 타입
- Redis는 여러가지 데이터 타입을 처리할 수 있다. 
- List, Hash, Set, Sort Set 데이터 타입이 존재하며, Redis의 데이터 타입들은 Key 하나당 2^23개 또는 40억개 이상의 값을 가질수 있다. 
- Redis의 명령들은 다음 형태의 이름을 갖는다. 
  - Set 명령들은 S로 시작, Hash는 H, Sort Set은 Z로 시작한다. 리스트 명령들은 연산의 방향에 따라서 왼쪽 L, 오른쪽 R로 시작합니다.

<br>

## Hash
논리적으로 key 필드를 구분하는 대신 key-value 쌍으로 된 데이터를 포함하는 Hash를 생성할 수 있다. Key 필드를 나타낼 때에는 콜론(:)을 사용한다. 해시는 Key 필드를 사용함으로 Key 자체의 값을 주지 않아도 된다.<br>
Document 타입의 DB인 MongoDB와는 다르게 Redis의 Hash는 중첩이 될 수 없다. List 타입의 데이터 타입에서도 중첩은 불가능합니다. Hash는 문자열 값만 저장 할 수 있다. Hash의 값으로 다른 Hash에 저장하는것도 불가능하다.

#### HSET & HMSET : 저장
- HSET : 입력한 해시 키 밑에 지정한 필드에 값을 저장하고 필드 값이 존재하면 덮어쓴다(HSET key field value)
- HMSET : 입력한 해시 키 밑에 지정한 필드에 값을 저장하고 필드 값이 존재하면 덮어쓴다(HMSET key field1 value1 field2 value2)
<img width="437" alt="image" src="https://user-images.githubusercontent.com/74396651/229758036-beed3412-338f-46e7-9119-577ab20d163a.png">


#### HGET & HVALS & HGETALL
- HGET : 입력한 해시 키 밑에 지정한 필드의 값을 가져온다. 없으면 nil 반환
- HMGET : 입력한 해시 키 밑에 여러 필드의 값을 가져온다. 없으면 nil 반환
<img width="332" alt="image" src="https://user-images.githubusercontent.com/74396651/229758297-73034a1c-7449-4745-af7a-46160f5958e5.png">
- HGETALL : 입력한 새시 키 밑에 모든 필드와 값을 가져온다. 필드1, 값1, 필드2, 값2, ... 형태로 반환
<img width="311" alt="image" src="https://user-images.githubusercontent.com/74396651/229758678-9199db03-4808-4411-acd2-5211a1fc05a2.png">


#### HDEL & DEL
- HDEL : 입력한 해시 키 밑에 필드를 삭제한다.
<img width="314" alt="image" src="https://user-images.githubusercontent.com/74396651/229760101-a1fe18e0-b44a-4a9a-ae34-13c8e533cd6d.png">
- DEL : 입력한 해시 키를 삭제한다.
<img width="358" alt="image" src="https://user-images.githubusercontent.com/74396651/229760246-3fea13a8-bdd3-47d3-9707-8203323d7c50.png">

#### HLEN 
- HLEN : 해당 Hash의 필드 개수 조회
<img width="445" alt="image" src="https://user-images.githubusercontent.com/74396651/229760934-45bdf611-d70c-4328-8952-45a070b27dac.png">

#### HINCRBY
- HINCRBY : 정수 필드의 값을 주어진 값만큼 증가
<img width="422" alt="image" src="https://user-images.githubusercontent.com/74396651/229761347-5b313d4c-e389-487c-a9f5-6a48bd76a873.png">
> 문자는 그냥 다시 HSET으로 덮어씌웠다

<br>

## List
여러 개의 순서적인 값을 포함하여, Queue와 Stack 모두로 동작할 수 있다. Queue는 FIFO(first in, first out) 알고리즘으로 동작하며, Stack은 LIFO(last in, frist out) 알고리즘으로 동작한다. List는 많은 복잡한 동작을 할 수 있다. 리스트 중간에 데이터를 끼워 넣거나, 크기를 제한 하거나, 리스트들간의 값을 옮길 수도 있다.<br>
Redis의 모든 List 연산에서는 0을 기준으로 하는 인덱스를 사용한다. 맨 왼쪽, 첫번째의 요소가 1이 아닌 0으로 시작합니다. 인덱스 값이 음수인 경우는 끝(오른쪽)에서 앞쪽(왼쪽)으로 오면서 나타내는 위치를 의미한다. -1은 맨 끝(오른쪽)이다.

- RPUSH / LPUSH : 오른쪽/왼쪽에 삽입
<img width="304" alt="image" src="https://user-images.githubusercontent.com/74396651/232008395-1c32d6a3-731f-4e0f-9a2b-a09c8b97772a.png">

- LLEN : 리스트 크기 출력
<img width="235" alt="image" src="https://user-images.githubusercontent.com/74396651/232008423-186cfaef-28e3-4731-9fe3-18e4ec70e86d.png">

- LRANGE : 범위를 지정하여 리스트 부분 조회
<img width="262" alt="image" src="https://user-images.githubusercontent.com/74396651/232008513-ebfc6a98-ed9f-4024-a2d3-9d8cae35240c.png">

- RPOP / LPOP : 오른쪽/왼쪽 한 후 삭제
<img width="230" alt="image" src="https://user-images.githubusercontent.com/74396651/232008559-6f23c21b-7c8a-4ded-8bda-b582a5f1322d.png">

- LREM : 주어진 키로부터 일치되는 값 삭제, 삭제할 개수와 값 입력
<img width="301" alt="image" src="https://user-images.githubusercontent.com/74396651/232008945-2cc4fcf3-deba-44dd-8f80-c3aff97229f0.png">
- RPOPLPUSH : 오른쪽 호출 후 왼쪽에 넣기, RPOPLPUSH만 명령어가 존재하며, RPOPRPUSH, LPOPLPUSH, LPOPRPUSH 같은 명령어는 존재하지 않는다. 해당 조합 명령은 cli에서는 불가능하며, Redis를 지원하는 프로그래밍 언어에서 멀티블록을 엮어서 실행하면 된다.

- Blocking List :  호출할 값이 생성되기 전까지 Blocking을 하는 명령어. 값을 호출하기 위한 키와 타임아웃 시간(초)가 필요.


<br>
<hr>
<br>

## SET
Set은 중복된 값이 없고 정렬이 되지 않은 데이터들의 모임이다. 두 개 이상의 키 값들 간의 Union이나 intersection 같은 복잡한 연산을 수행할 때 필요하다. 하나의 공통 키를 갖는 집합을 만들고자 하며, SADD 명령을 통해 값을 추가할 수 있다.

- SADD : set 생성
<img width="321" alt="image" src="https://user-images.githubusercontent.com/74396651/236630658-d46b04a7-7f36-4424-b71b-02f90cb716fa.png">

- SMEMBERS : set이 가진 값 출력

<img width="244" alt="image" src="https://user-images.githubusercontent.com/74396651/236630665-b6b7e95c-997f-4953-b177-54eca3cc63fb.png">

- SINTER : 교집합

<img width="317" alt="image" src="https://user-images.githubusercontent.com/74396651/236630703-26f8b42d-d694-4310-8da6-f477856d5862.png">

- SDIFF : 차집합

<img width="297" alt="image" src="https://user-images.githubusercontent.com/74396651/236630718-1b188052-9c79-4267-9e6e-d592882d1dca.png">

- SUNION : 합집합

<img width="272" alt="image" src="https://user-images.githubusercontent.com/74396651/236630729-a53327f3-9dbc-4b14-88e5-cc34ad0add39.png">

- SUNIONSTORE, SINTERSTORE, SDIFFSTORE : 연산 결과를 새로운 SET으로 저장

- SMOVE : 한 SET의 값들으 다른 SET으로 이동
- SCARD : SET의 개수를 카운트
- SPOP : 무작위로 값 추출
- SREM : SET에서 값 삭제

### GET/SET과 HGET/HSET의 차이

![image](https://user-images.githubusercontent.com/74396651/229754963-08789ed5-94f4-48cc-8eb7-e70c2af1a3b3.png)
[참고](https://velog.io/@kimjiwonpg98/Redis-SET-vs-HSET)


