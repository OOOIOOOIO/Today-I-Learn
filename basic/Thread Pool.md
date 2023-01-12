# Thread Pool

![image](https://user-images.githubusercontent.com/74396651/211992175-67736070-066d-4b10-bdf4-1371bdaf4194.png)


> &nbsp;쓰레드 풀은 작업처리에 사용되는 쓰레드를 제한된 개수만큼 정해놓고 작업큐(Queue)에 들어오는 작업들을 하나식 쓰레드가 맡아 처리한다. 그렇게 하면 작업처리 요청이 폭증되어도 쓰레드 전체 개수가 늘어나지 않으므로 시스템 성능이 급격히 저하되지 않는다.(개수를 제한해서 하나씩 처리한다.)<br><br>&nbsp;프로세스 중 병렬 작업처리가 많아지면 쓰레드 개수가 증가되고 그에따른 쓰레드 생성과 스케쥴링으로 인해 CPU가 바빠져 메모리 사용량이 늘어난다. 이에 따라 시스템 성능이 저하되고 갑작스러운 병렬작업의 폭증에 따른 쓰레드 폭증을 막으려면 Thread Pool을 사용해야 한다.

<br>

## 사용
> &nbsp;Java는 Thread Pool을 생성하고 사용할 수 있도록 java.util.concurrent.Excutors 클래와 java.util.concurrent.ExcectorService 인터페이스를 제공하고 있다. 

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
> &nbsp;쓰레드 풀에게 작업을 시키기 전에 작업을 생성시켜야 쓰레드 풀에게 작업처리를 요청할 수 있다.<br>
> &nbsp;작업 생성은 Runnable 인터페이스 or Callable 인터페이스를 구현한 클래스로 작업을 요청할 코드를 삽입해 작업을 만들 수 있다.
- ExecutorService의 작업큐에 Runnable 또는 Callable 객체를 넣는 행위를 말한다.
- ExecutorService는 작업처리 요청을 위해 두가지 메소드를 제공한다.
<br>

### ExcutorService에 작업(Job) 추가
> &nbsp;Executors로 ExcecutorService를 생성했다면, 서비스 작업을 처리한다.<br>
> &nbsp;ExcutorService.submit() or excute() 메소드로 메소드 작업을 추가한다.<br>
> &nbsp;둘의 차이점은 Runnable의 run() 메서드는 리턴값이 없고, Callable의 call() 메서드는 리턴값이 있다는 점이다.<br>

   - excute
      - Runnable을 작업큐에 저장, 작업처리 결과(리턴값) 없음
      - 작업처리 도중 예외 발생시 쓰레드가 종료되고 해당 쓰레드는 쓰레드 풀에서 제거된다.
      - 쓰레드 풀은 다른 작업처리를 위해 새로운 쓰레드를 생성한다. 
      - excute(Runnable Command), Return Type : void
   - submit
      - Runnable 또는 Callable 작업큐에 저장, 리턴된 Future을 통해 작업처리 결과(리턴값)을 얻음
      - 작업처리 도중 예외가 발생하더라도 쓰레드가 종료되지 않고 다음 작업을 위해 재사용된다.
      - 가급적 쓰레드의 생성 오버헤더를 줄이기 위해 submit()을 사용하는 것이 좋다.
      - submit(Runnable task), Return Type : Future&lt;?&gt;
      - submit(Runnable task, V result), Return Type : Future&lt;V&gt;
      - submit(Callable&lt;V&gt; task), Return Type : Future&lt;V&gt;
- ExecutorService의 submit() 메소드는 매개값으로 준 Runnable 또는 Callable작업을 스레드 풀의 작업 큐에 저장하고 즉시 Future 객체를 리턴한다. 
- Future객체는 작업결과가 아니라 작업이 완료될때까지 기다렸다가 (지연) 최종결과를 얻는데 사용된다. 그래서 Future을 지연완료 객체라도 한다.

<br>

### 리턴값이 있는(Callable) 작업완료 통보
```java

Future future = excutorService.submit(taskThread);

Callable<T> taskThread = new Callable<T>(){

  @Override
  public T call() throw Exception{
  
    // 쓰레드에서 처리할 CODE
    
    return T;
  }

};
```
- Callable 작업의 처리요청은 ExcutorService의 submit() 메소드를 호출한다.
- submit() 메소드는 작업 큐에 Callable 객체를 저장하고 즉시 Future&lt;T&gt;를 리턴한다

<br>

### 리턴값이 없는(Runnable) 작업완료 통보
```java
Future future = executorService.submit(taskThread);

Runnable taskThread = new Runnable() {

	@Override
    public void run(){
    
    //쓰레드가 처리할 CODE 
    
    }
};
```
- Runnable은 리턴값이 없음에도 불구하고 Future객체를 리턴하는데, 이것은 스레드가 작업처리를 정상적으로 완료했는지, 처리도중 예외가 발생했는지 확인하기 위해서다. 정상완료 시 Future의 get메소드는 null을 리턴한다.
- 작업도중 예외발생시 ExecutorException을 발생시킨다. 

<br>

### 작업완료 순으로 통보
- 작업요청 순서대로 작업처리가 완료되는 것은 아니다.
- 작업의 양과 스레드 스케쥴링에 따라서 먼저 요청한 작업이 나중에 완료되기도 한다.
- 여러개의 작업들이 순차적으로 처리될 필요가 없고, 처리결과도 순차적으로 이용할 필요가 없다면 작업 처리가 완료된 순으로 결과를 얻어 이용한다.
- 스레드풀에서 작업처리가 완료된 것만 통보받는 방법은 CompletionService 의 처리완료된 작업을 가져오는 poll()과 take()메소드를 사용하면 된다.

<br>
<br>

[참고](https://cheershennah.tistory.com/170)
