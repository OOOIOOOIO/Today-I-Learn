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
   - 파이프, 파일, 소켓 등을 이용한 통신 방법 이용!

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

# 멀티 프로세스와 멀티 쓰레드의 차이

## 멀티 프로세스
- 하나의 응용프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 하나의 작업(태스크)을 처리하도록 하는 것이다.
- 장점
    - 여러 개의 자식 프로세스 중 하나에 문제가 발생하면 그 자식 프로세스만 죽는 것 이상으로 다른 영향이 확산되지 않는다.
- 단점
    - Context Switching에서의 오버헤드
    - Context Switching 과정에서 캐쉬 메모리 초기화 등 무거운 작업이 진행되고 많은 시간이 소모되는 등의 오버헤드가 발생하게 된다.
    - 프로세스는 각각의 독립된 메모리 영역을 할당받았기 때문에 프로세스 사이에서 공유하는 메모리가 없어, Context Switching가 발생하면 캐쉬에 있는 모든 데이터를 모두 리셋하고 다시 캐쉬 정보를 불러와야 한다.
    - 프로세스 사이의 어렵고 복잡한 통신 기법(IPC)
    - 프로세스는 각각의 독립된 메모리 영역을 할당받았기 때문에 하나의 프로그램에 속하는 프로세스들 사이의 변수를 공유할 수 없다.
- 참고 Context Switching란?
    - CPU에서 여러 프로세스를 돌아가면서 작업을 처리하는 데 이 과정을 Context Switching라 한다.
    - 구체적으로, 동작 중인 프로세스가 대기를 하면서 해당 프로세스의 상태(Context)를 보관하고, 대기하고 있던 다음 순서의 프로세스가 동작하면서 이전에 보관했던 프로세스의 상태를 복구하는 작업을 말한다.

<br>

## 멀티 스레드
- 하나의 응용프로그램을 여러 개의 스레드로 구성하고 각 스레드로 하여금 하나의 작업을 처리하도록 하는 것이다.
- 윈도우, 리눅스 등 많은 운영체제들이 멀티 프로세싱을 지원하고 있지만 멀티 스레딩을 기본으로 하고 있다.
- 웹 서버는 대표적인 멀티 스레드 응용 프로그램이다.
- 장점
    - 메모리 공유로 인해 시스템 자원 소모 감소 (자원의 효율성 증대)
    - 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 자원을 효율적으로 관리할 수 있다.
    - 시스템 처리량 증가 (처리 비용 감소)
    - 스레드 간 데이터를 주고 받는 것이 간단해지고 시스템 자원 소모가 줄어들게 된다.
    - 스레드 사이의 작업량이 작아 Context Switching이 빠르다.
    - 간단한 통신 방법으로 인한 프로그램 응답 시간 단축
    - 스레드는 프로세스 내의 Stack 영역을 제외한 모든 메모리를 공유하기 때문에 통신의 부담이 적다.
- 단점
    - 주의 깊은 설계가 필요하다.
    - 디버깅이 까다롭다.
    - 단일 프로세스 시스템의 경우 효과를 기대하기 어렵다.
    - 다른 프로세스에서 스레드를 제어할 수 없다. (즉, 프로세스 밖에서 스레드 각각을 제어할 수 없다.)
    - 멀티 스레드의 경우 자원 공유의 문제가 발생한다. (동기화 문제)
    - 하나의 스레드에 문제가 발생하면 전체 프로세스가 영향을 받는다.

<br>

### 멀티 프로세스 대신 멀티 스레드를 사용하는 이유?
![image](https://user-images.githubusercontent.com/74396651/204328406-d108b2f7-8628-4f95-bd61-ec92611e77b2.png)


- 쉽게 설명하면, 프로그램을 여러 개 키는 것보다 하나의 프로그램 안에서 여러 작업을 해결하는 것이다.

### 여러 프로세스(멀티 프로세스)로 할 수 있는 작업들을 하나의 프로세스에서 여러 스레드로 나눠가면서 하는 이유?
- 자원의 효율성 증대
    - 멀티 프로세스로 실행되는 작업을 멀티 스레드로 실행할 경우, 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 자원을 효율적으로 관리할 수 있다.
    - 프로세스 간의 Context Switching시 단순히 CPU 레지스터 교체 뿐만 아니라 RAM과 CPU 사이의 캐쉬 메모리에 대한 데이터까지 초기화되므로 오버헤드가 크기 때문
    - 스레드는 프로세스 내의 메모리를 공유하기 때문에 독립적인 프로세스와 달리 스레드 간 데이터를 주고 받는 것이 간단해지고 시스템 자원 소모가 줄어들게 된다.
- 처리 비용 감소 및 응답 시간 단축
    - 프로세스 간의 통신(IPC)보다 스레드 간의 통신의 비용이 적으므로 작업들 간의 통신의 부담이 줄어든다.
    - 스레드는 Stack 영역을 제외한 모든 메모리를 공유하기 때문
프로세스 간의 전환 속도보다 스레드 간의 전환 속도가 빠르다.
    - Context Switching시 스레드는 Stack 영역만 처리하기 때문

<br>

### 주의할 점!
- 동기화 문제
- 스레드 간의 자원 공유는 전역 변수(데이터 세그먼트)를 이용하므로 함께 상용할 때 충돌이 발생할 수 있다.


<br>
<hr>
<br>

# Java에서의 Thread
- 일반 Thread와 거의 차이가 없으며, JVM이 운영체제 역할을 한다.
- 자바에선 Process가 존재하지 않고 Thread만 존재하며, 자바 Thread는 JVM에 의해 스케쥴되는 실행 단위 코드 블록이다.
- 자바에서 Thread 스케쥴링은 전적으로 JVM에 의해 이루어진다.
- JVM에 의해 하나의 프로세스가 발생하고 main() 안의 실행문들이 하나의 쓰레드이다.
- main() 이외의 또 다른 쓰레드를 만들려면 Thread 클래스를 상속하거나 Runnable 인터페이스를 구현해야 한다.

<br>

## JVM이 관리하는 정보들
- Thread가 몇 개 존재하는지
- Thread로 실행되는 프로그램 코드의 메모리 위치가 어디인지
- Thread의 상태
- Thread의 우선순위
- 즉, 개발자는 Java Thread로 작동할 Thread 코드를 작성하고, Thread 코드가 생명을 가지고 실행을 시작하도록 JVM에 요청하는 것 뿐이다.

<br>

## Thread 생명 주기
- Runnable(준비상태)
> 스레드가 실행되기 위한 준비단이다. CPU를 점유하고 있지않으며 실행(Running 상태)을 하기 위해 대기하고 있는 상태이다. 코딩 상에서 start( ) 메소드를 호출하면 run( ) 메소드에 설정된 스레드가 Runnable 상태로 진입합니다. “Ready“ 상태라고도 합니다.
- Running(실행상태)
> CPU를 점유하여 실행하고 있는 상태이며 run() 메서드는 JVM만이 호출 가능하다. Runnable(준비상태)에 있는 여러 스레드 중 우선 순위를 가진 스레드가 결정되면 JVM이 자동으로 run( ) 메소드를 호출하여 스레드가 Running 상태로 진입한다.
- Dead(종료상태)
> Running 상태에서 스레드가 모두 실행되고 난 후 완료 상태입니다. “Done” 상태라고도 한다.
- Blocked(지연상태)
> CPU를 점유권을 상실한 상태입니다. 후에 특정 메서드를 실행시켜 Runnable(준비상태)로 전환한다. wait( ) 메소드에 의해 Blocked 상태가 된 스레드는 notify( ) 메소드가 호출되면 Runnable 상태로 변경된다. sleep(시간) 메소드에 의해 Blocked 상태가 된 스레드는 지정된 시간이 지나면 Runnable 상태로 간다.

<br>
<hr>
<br>

# 예제

## Single Thread(Thread 클래스 상속)
```java
package com.example.demo.threadTest;

public class ThreadTest1 extends Thread {

    private int[] temp;

    public ThreadTest1(String threadName) {

        /*
            Thread 이름!!
            public Thread(String name) {
                this(null, null, name, 0);
            }
         */
        super(threadName);
        temp = new int[10];

        for (int start = 0; start < temp.length; start++) {
            temp[start] = start;
        }
    }

    @Override
    public void run() {
        for (int start : temp) {
            try {
                Thread.sleep(1000);

            } catch (InterruptedException interruptedException) {
                interruptedException.printStackTrace();

            }
            System.out.println("Thread Name : " + currentThread().getName());
            System.out.println("temp value : " + start);
        }
    }

    public static void main(String[] args) {
        ThreadTest1 tt1 = new ThreadTest1("첫번째"); // new Therad(String name)
        tt1.start();
    }
}

```

![image](https://user-images.githubusercontent.com/74396651/213122127-2eeee246-5423-421f-8b1d-dfcaff825b62.png)

<hr>

## Single Thread(Runnable 인터페이스 상속, Thread 클래스 상속보다 많이 쓰인다.)
```java
package com.example.demo.threadTest;

public class ThreadTest2 implements Runnable{

    private int[] temp;

    public ThreadTest2(){
        temp = new int[10];

        for (int start = 0; start < temp.length; start++) {
            temp[start] = start;
        }
    }

    @Override
    public void run() {

        for (int start : temp) {
            try {
                Thread.sleep(1000);

            } catch (InterruptedException interruptedException) {
                interruptedException.printStackTrace();
            }

            System.out.println("쓰레드 이름 : " + Thread.currentThread().getName());
            System.out.println("temp value : " + start);
        }
    }

    public static void main(String[] args) {
        ThreadTest2 tt2 = new ThreadTest2();
        Thread t = new Thread(tt2, "첫번쨰"); // new Thread(Runnable target, String name)

        t.start();
    }
}

```

![image](https://user-images.githubusercontent.com/74396651/213122965-3f3776dc-142c-48fa-a12d-845779b350d7.png)

<hr>

## Multi Thread-1
```java

```

<hr>

## Multi Thread-2
```java

```

<br>
<hr>
<br>

[참고](https://coding-factory.tistory.com/279)

