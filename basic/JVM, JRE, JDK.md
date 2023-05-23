# JVM, JRE, JDK
> 세 용어의 관계는 아래 사진과 같다!
![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/7960ea84-eecc-4823-af12-2c1cc816bb23)

## Java 철학
> 한 번 쓰고 모든 곳에서 실행한다(Wirte Once, Run Anywhere = WORA)

# JVM(Java Virtual Machine
1. 자바 프로그램이 어느 기기, 어느 운영체제 상에서도 실행될 수 있게 만들어 줍니다. => WORA
2. 자바 프로그램의 메모리를 효율적으로 관리 & 최적화한다.
- 가비지 컬렉션(Garbage Collection)
  - JVM이 메모리를 관리하는 프로세스를 지칭하는 용어입니다. 자바 프로그램 상에서 사용하지 않은 메모리를 지속적으로 찾아 제거함으로써 효율적인 메모리 관리를 가능하게 한다.


# JRE(Java Runtime Environment)
- JRE는 자바 클래스 라이브러리(Java class libraries), 자바 가상 머신(JVM) 그리고 위 그림에는 나오지 않았지만 자바 클래스 로더(Java class loader)를 포함하고 있다.
- 클래스 로더, 클래스 라이브러리를 통해 작성한 자바 코드를 라이브러리와 결합한 후 JVM에 넘겨 실행시킵니다. JRE는 그 자체로 특별한 기능을 한다기보다는 JVM이 원활하게 잘 작동할 수 있도록 환경을 맞춰주는 역할을 한다.
- 자바 8의 메모리 관리
  - 자바 메모리는 힙, 스택, 메타 스페이스로 구성
  - 힙 - 자바가 변수 내용을 저장하는 장소
  - 스택 - 자바가 함수 실행 및 변수 참조를 저장하는 장소
  - 메타 스페이스(과거 펌젠) - 자바가 클래스 정의와 같이 프로그램에서 변화하지 않는 정보를 저장하는 장소


# JDK(Java Developement Kit)
- JDK를 설치하면 JRE가 자동으로 설치 된다. JDK는 JRE를 포함하고 있고, JRE는 JVM을 포함하고 있다. 따라서 JDK를 설치하면 JRE, JVM이 자동으로 다 설치된다.
- 자바로 개발을 하지 않는 일반 사용자들은 자바로 만든 프로그램을 실행만 하면 되기 때문에 JRE만 설치해도 됩니다. 그러나 자바로 뭔가를 만들어보고 싶은 사람은 JDK를 설치해야 한다.
- JDK에는 JRE에는 없는 "자바 컴파일러(javac, java compiler)"를 포함하고 있다. 
- 컴파일러란 우리가 작성한 자바 문법을 컴퓨터가 이해할 수 있게 바꿔주는 해석기 같은 존재입니다.
- .java 파일을 만들어서 실행(빌드)하면 컴파일 작업을 거쳐 .class 라는 파일이 자동으로 생성된다. 

## Java 동작원리
![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/da61795c-af80-497e-b06c-3ada295d6092)
