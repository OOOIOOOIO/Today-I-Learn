# Process(프로세스)
- Process(프로세스)란 단순히 실행 중인 program(프로그램)이라고 할 수 있다.
- 즉, 사용자가 작성한 프로그램이 운영체제에 의해 메모리 공간을 할당받아 실행 중인 것이다. 
- Process는 프로그램에 사용되는 데이터와 메모리 등의 자원 그리고 Thtread로 구성된다.
   - #### 할당받는 시스템 자원의 예시
   - CPU 시간
   - 운영되기 위해 필요한 주소 공간
   - Code, Data, Stack, Heap의 구조로 되어 있는 독립된 메모리 영역

![image](https://user-images.githubusercontent.com/74396651/204324498-c8fdc9da-9c2d-4059-a4ee-8b0c4e4a1d6a.png)

## 특징
- Process는 각각 독립된 메모리 영역(Code, Data, Stack, Heap의 구조)을 할당받는다.
- 기본적으로 Process는 최소 1개의 Thread(메인 쓰레드)를 가지고 있다.
- 각 프로세스는 별도의 주소 공간에서 실행되며, 한 Process 다른 Process 변수나 자료구조에 접근할 수 없다.
- Process가 다른 Process의 자원에 접근하려면 Process 간의 통신(IPC, inter-process communication)을 사용해야 한다.
   - 파이프, 파일, 소켓 등을 이용한 통신 방법 이용

<br>
<hr>
<br>

# Thread(쓰레드)
- Thread(쓰레드)란 Process(프로세스) 내에서 실제로 작업을 수행하는 주체를 의미한다.
- 모든 Process에는 한 개 이상의 쓰레드가 존재하여 작업을 수행한다.
- 또한 두 개 이상의 쓰레드를 가지는 프로세스를 멀티 쓰레드 프로세스(mulit-threaded prcess)라고 한다.

![image](https://user-images.githubusercontent.com/74396651/204325373-1b67c249-91ce-468b-a84d-2d8ff14eaf68.png)

## 특징
- Thread는 Process 내에서 각각 Stack만 따로 할당 받고 Code, Data, Heap 영역은 공유한다.
- Thread는 하나의 Process 내에서 동작되는 여러 실행의 흐름으로, Process 내의 주소 공간이나 자원들(Heap 공간 등)을 같은 프로세스 내에 Thread끼리 공유하면서 실행된다.
- 같은 Process 안에 있는 여러 Thread들은 같은 Heap 공간을 공유한다. 반면 Process는 다른 Process의 메모레이 직접 접근할 수 없다.
- 각각의 Thread는 별도의 Register와 Stack을 갖고 있지만, Heap 메모리는 서로 읽고 쓸 수 있다.
- 한 Thread가 Process 자원을 변경하면, 다른 이웃 Thread(sibling thread)도 그 변경 결과를 즉시 볼 수 있다.

<br>
<hr>
<br>












