- 람다식에서 외부 지역 변수를 참조하여 사용할 경우 final 혹은 effectively final 이어야 하는 이유는 지역 변수가 Stack(스택)에 저장되기 때문이다.

- 람다식에서는 값을 바로 참조하는 것에 제약이 있어 복사된 값을 이용하게 되는데, 이때 멀티쓰레드 환경에서 복사될/된 값이 변경 가능할 경우 이로 인한 동시성 이슈를 대응할 수 없다.

- https://dev-jwblog.tistory.com/153

- ![image](https://github.com/user-attachments/assets/49174298-66c2-46a3-91a0-4de609e6d732)
