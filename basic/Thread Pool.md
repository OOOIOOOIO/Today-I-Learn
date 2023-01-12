# Thread Pool

![image](https://user-images.githubusercontent.com/74396651/211992175-67736070-066d-4b10-bdf4-1371bdaf4194.png)


> &nbsp;쓰레드 풀은 작업처리에 사용되는 쓰레드를 제한된 개수만큼 정해놓고 작업큐(Queue)에 들어오는 작업들을 하나식 쓰레드가 맡아 처리한다. 그렇게 하면 작업처리 요청이 폭증되어도 쓰레드 전체 개수가 늘어나지 않으므로 시스템 성능이 급격히 저하되지 않는다.(개수를 제한해서 하나씩 처리한다.)<br><br>&nbsp;프로세스 중 병렬 작업처리가 많아지면 쓰레드 개수가 증가되고 그에따른 쓰레드 생성과 스케쥴링으로 인해 CPU가 바빠져 메모리 사용량이 늘어난다. 이에 따라 시스템 성능이 저하되고 갑작스러운 병렬작업의 폭증에 따른 쓰레드 폭증을 막으려면 Thread Pool을 사용해야 한다.

<br>

## 사용
> &nbsp;Java는 Thread Pool을 생성하고 사용할 수 있도록 java.util.concurrent.Excutors 클래스와 java.util.concurrent.ExcectorService 인터페이스를 제공하고 있다. 

<br>

### ExcutorService 생성
> &nbsp;Executors는 ExecutorService를 생성하며 다음 메소드를 제공하여 쓰레드 풀 개수 및 종류를 정할 수 있다.

- newFixedThreadPool(int) : 인자 개수만큼 고정된 프레드풀을 만든다.
- newCachedThredPool() : 필요할때 필요한 만큼 쓰레드풀 생성. 이미 생성된 쓰레드를 재활용 할수 있어 성능 용이.
- newScheculedThreadPool(int) : 일정 시간 뒤에 실행되는 작업이나, 주기적으로 수행되는 작업이 있다면 스케줄스레드 풀을 활용 할 수 있다.
- newSingleThredExecutor() : 쓰레드 1개인 ExecutorService를 리턴한다. 싱글 스레드에서 동작하는 작업 처리시 사용한다.

<br>

### 작업 생성
- Runnable(리턴값 없음) 객체를 가져와 run() 메서드를 실행하거나
- Callable(리턴값 존재) 객체를 가져와 call() 메서드를 실행한다.

<br>

### 작업처리 요청
- ExecutorService의 작업큐에 Runnable 또는 Callable 객체를 넣는 행위를 말한다.
- ExecutorService는 작업처리 요청을 위해 두가지 메소드를 제공한다.



