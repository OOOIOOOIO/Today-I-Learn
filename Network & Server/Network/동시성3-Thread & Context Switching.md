# Thread & Context Switching
> 동시성 문제1, 2에서 병행성(Concurrency), 동기(Synchronous) / 비동기(Asynchronous), 블로킹(Blocking) / 논블로킹(Non-Blocking)에 대해 알아보았다. 이러한 개념들을 바탕으로 소프트웨어들이 겪고 있는 문제가 무엇이고 그 문제들에 대한 해결책으로 어떤 것들이 제시되고 있는지 알아보자.

<br>
<hr>
<br>

## Thread(쓰레드)
- 컴퓨터에 2개의 CPU가 있다고 하면 동시에 몇 개의 작업을 처리할 수 있을까?

![image](https://user-images.githubusercontent.com/74396651/204317291-f77b39a9-6ded-4fdf-8587-5c3b07533363.png)

- 당연히 2개의 작업을 처리할 수 있을 것이다. 하지만 하나의 컴퓨터에게 원하는 것은 여러 작업을 수행하는 것이다.
- 만약 2개의 CPU에서 4개의 작업을 동시에 수행하는 것처럼 보이게 하려면 어떻게 해야 할까?

![image](https://user-images.githubusercontent.com/74396651/204317587-c6bd93af-d95e-4d32-924f-7c42a9875411.png)

- 위와 같이 여러개의 작업을 빠르게 번갈아가면서 처리하면 사용자는 4개의 작업이 동시에 수행되는 것처럼 보이게 될 것이다.
- 이러한 하나의 Task 단위를 우리는 Thread(쓰레드)라고 부르며, 이러한 원리로 우리가 IDE를 수행하면서 동시에 웹 브라우저를 통해 서칭도 하고 음악도 들을 수 있는 것이다.

<br>
<hr>
<br>

## Context Switching
- 하나의 CPU가 여러 쓰레드를 번갈아가며 처리하려면 하나의 Thread에서 수행중인 동작을 멈추고 그 상태를 기억한 후 새로운 쓰레드로 이동해야 할 것이다. 
- 이러한 일련의 과정을 우리는 Context Switching이라고 부른다.
- Context Switching이 발생할 때 시스템에선 다음과 같은 작업이 발생한다.

![image](https://user-images.githubusercontent.com/74396651/204318568-307656fa-c2e8-41c8-b265-c998da47afd3.png)

- 보기에는 간단해 보이지만 Register에서 Stack으로 약 7개 이상의 값을 옮기는 과정은 결코 가볍지 않다. 
- 특히 1초에 수백번씩 반복되는데, Thread가 많아진다면 CPU 입장에선 너무나 부담스러운 일이 될 것이다.

<br>
<hr>
<br>

## Stack Size(스택 사이즈)
- 컴퓨터 과학 관점에서 보았을 때, 하나의 Thread는 하나의 Stack을 의미하기도 한다.
- 리눅스에서 하나의 Stack은 x86_64 기준 2MB 정도의 메모리를 차지한다.

![image](https://user-images.githubusercontent.com/74396651/204319651-b39a4261-261c-44a8-b6b6-c0953d5d5c70.png)

- 이러한 상황에서 Thread를 1000개 정도 생성한다면 메모리를 4GB 정도는 우습게 차지할 수 있는 것이다.
- 단순히 생각해서 하나의 웹 서버에서 동시에 1000개의 요청을 처리하기 위해 무려 4GB 메모리를 사용한다는 것이다.

<br>
<hr>
<br>

## Blocking & Synchronous Networking(블로킹 & 동기 네트워크)
- 전통적으로 사용되는 블로킹 & 동기 네트워킹 방식을 이용한 웹 서버에서는 많은 요청을 처리하기 위해 많은 Thread를 생성해야하고, Thread가 많아질수록 Context Switching의 부담이 커지는 동시에 많은 메모리도 차지하게 된다.

<br>
<br>
<br>
<br>
<br>

참조 :
