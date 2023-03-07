# public key retrieval is not allowed 에러 해결법
MySQL 8.0, 버전 이상으로 Dbevaer로 접속을 시도하는데 에러가 발생했다. <br>
8.0 버전 이상부터는 보안이슈로 useSSL 옵션에 대한 추가적인 설정이 필요해졌다.<br>
allowPublicKeyRetrieval=true 설정을 해주어야한다.<br>


# DBever
<img width="950" alt="image" src="https://user-images.githubusercontent.com/74396651/223430532-05212264-9a64-4de0-8b90-1779004cbe74.png">
- 위 사진처럼 true로 바꿔준다.

<br>

# IDE
```
jdbc:mysql://localhost:3306/test?useSSL=false&allowPublicKeyRetrieval=true

```
- datasource url에 추가해준다.
- 혹은 인텔리제이로 DB에 접속할 때 local > Advanced > allowPublicKeyRetrieval을 확인하여 treu로 설정한다.

