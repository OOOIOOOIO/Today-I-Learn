# 들어가면서

### 쓰레드를 무한으로 늘리게 되면 어떤 문제가 발생하는지
- 성능 저하
- 쓰레드도 하나의 자원이므로 계속적으로 소모되면 자원고갈로 인해 메모리풀로 인해 서버가 다운될 수 있다.
- 서버 입장에서 가장 중요한 것은 서버가 다운되지 않고 안정적으로 운영되는 것이다.

<br>

### 서버를 어떻게 안정적으로 운영할까
- 쓰레드를 미리 만들어 놓고 재사용하는 방식으로 사용한다. ==> 쓰레드 풀

### 쓰레드 풀 사용이유
- 서버가 모든 요청에 대해 Thread를 매번 생성하게 되면 성능상 문제가 발생할 수 있다.
- 이를 극복하기 위해 ThreadPool을 적용해 일정 수의 작업을 동시에 처리하도록 한다.

# ThreadPoolExcector

### ThreadPoolExecutor 생성자 
```java
//ThreadPoolExecutor 생성자 

ThreadPoolExecutor(int corePoolSize, int maximumPoolSize, long keepAliveTime, TimeUnit unit, BlockingQueue<Runnable> workQueue)

ThreadPoolExecutor(int corePoolSize, int maximumPoolSize, long keepAliveTime, TimeUnit unit, BlockingQueue<Runnable> workQueue, RejectedExecutionHandler handler)

ThreadPoolExecutor(int corePoolSize, int maximumPoolSize, long keepAliveTime, TimeUnit unit, BlockingQueue<Runnable> workQueue, ThreadFactory threadFactory)

ThreadPoolExecutor(int corePoolSize, int maximumPoolSize, long keepAliveTime, TimeUnit unit, BlockingQueue<Runnable> workQueue, ThreadFactory threadFactory, RejectedExecutionHandler handler)
```

<br>

### threadPoolExecutor 생성 
```java
//Creating a threadPoolExecutor

int corePoolSize = 10;
int maxPoolSize = 15;
long keepAliveTime = 6000;
ExecutorService es = new threadPoolExecutor(corePoolSize, maxPoolSize, keepAliveTime, TimeUnit.MILLISECONDS, new LinkedBlockingQueue < Runnable > ());
```
- int corePoolSize
   - 기본 풀 사이즈를 의미
   - 실행할 최소 Thread 수 
- int maximumPoolSize
   - 최대 지원 Thread 수
- long keepAliveTime 
   - 쓰레드 미사용 시 제거 대기 시간
   - corePoolSize보다 쓰레드가 많아졌을 경우 maximumPoolSize까지 쓰레드가 생성되는데 keepAliveTime시간만큼 유지했다가 다시 corePoolSize로 유지되는 시간을 의미한다. 
- TimeUnit unit
   - keepAliveTime 값의 시간단위 (eg. milliseconds, seconds.. ) 
- BlockingQueue <Runnable> workQueue
   - 요청된 작업들이 저장될 큐 : 작업 대기열 관리
   - corePoolSize보다 작업 쓰레드가 많아졌을 경우, 남는 쓰레드가 없을 경우, workQueue에서 대기한다.
> &nbsp;여기서 maximumPoolSize 옵션에 유의해야하는데, maximumPoolSize 이 사용되는 시점이다. 단순히 생각하기로는 corePoolSize만큼 쓰레드들에게 task를 할당하고, 이 이상 task가 들어오면 maximumPoolSize 까지 쓰레드를 추가하면서 task를 실행시키다가 maximumPoolSize까지 쓰레드가 꽉 차면 그때부터 workQueue에 task를 보관한다고 생각할 수 있지만, javadoc 문서를 확인하면 이러한 순서로 동작하지 않는다.<br><br>


  
  
  
  
  
  
  
