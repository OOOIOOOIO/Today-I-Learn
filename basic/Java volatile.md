# Java volatile
- volatile keyword는 Java 변수를 Main Memory에 저장하겠다는 것을 명시한다.
- 매번 변수의 값을 Read할 대마다 CPU cache에 저장된 값이 아닌 Main Memory에서 읽는 것이다.
- 변수의 값을 Write할 때마다 Main Memory에 작서하는 것이다.

## volatile을 사용하는 이유
![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/2c2f0f5e-9a12-419a-ba6e-146e775ea886)

- volatile 변수를 사용하고 있지 않는 MultiThread 어플리케이션에서는 Task를 수행하는 동안 성능 향상을 위해 Main Memory에서 읽은 변수 값을 CPU Cache에 저장한다.
- 만약에 Multi Thread환경에서 Thread가 변수 값을 읽어올 때 각각의 CPU Cache에 저장된 값이 다르기 때문에 변수 값 불일치 문제가 발생한다.

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/d47b120b-458a-4d01-a443-8aadd9b4a51c)

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/47164e38-754a-4da9-a5dc-c82c91f09691)

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/95d9daf7-4bf9-44ba-81d9-ffe79f7f82d0)

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/4fe922c8-a8a1-4302-81d8-898fc14b7c78)

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/446b66e8-7be8-4fea-b340-cb0c2da7d488)




<br>
<br>
<br>
[참고 따옴](https://nesoy.github.io/articles/2018-06/Java-volatile)
