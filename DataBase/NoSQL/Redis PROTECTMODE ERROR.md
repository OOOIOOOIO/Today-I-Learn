ACCESS DENIED -> PRTECTMODE 떄매

bind 0.0.0.0 ::1 + requirepass 설정했더니 에러
그래서 그냥
bind 0.0.0.0만 하고 spring yml의 host에 0.0.0.0 적어줬더니 잘 됨 하..


http://redisgate.kr/redis/server/protected-mode.php

https://velog.io/@yeezze/ec2%EC%97%90-Redis-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0

https://www.baeldung.com/linux/redis-server-remote-connect

https://redis.io/commands/auth/
