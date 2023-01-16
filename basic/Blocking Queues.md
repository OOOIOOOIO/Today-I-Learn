# Blocking Queues
> &nbsp;블로킹 큐란 특정 상황에 쓰레드를 대기하도록 하는 큐이다. 큐에서 엘리먼트를 빼려고 시도했는데(디큐) 큐가 비어있다거나, 큐에 엘리멘트를 넣어려고 했는데(인큐) 큐에 넣을 수 있는 공간이 없다거나 할 때 디큐/인큐 호출 쓰레드를 대기하도록 한다.<br><br>
> &nbsp;비어있는 큐에서 엘리먼트를 빼려고 시도하는 쓰레드의 대기 상태는 다른 쓰레드가 이 큐에 엘리먼트를 넣을 때까지 지속된다.<br><br>
> &nbsp;꽉 찬 큐에 엘리먼트를 넣으려고 시도하는 쓰레드의 대기 상태는 다른 쓰레드가 큐에서 엘리먼트를 빼거나 큐를 정리하여(Clean) 큐의 공간이 확보될 때까지 지속된다.

![image](https://user-images.githubusercontent.com/74396651/212630369-d3f60848-4ee4-4f46-b7e8-b77cf1f69f89.png)
- [java.util.concurrent.BlockingQueue(원문)](https://jenkov.com/tutorials/java-util-concurrent/blockingqueue.html)

### Blocking Queue 구현
> 블로킹 큐의 구현읜 바운디드 세마포어와 유사하다.[바운디드 세마포어](http://parkcheolu.tistory.com/28)
```java
public class BlockingQueue {

  private List queue = new LinkedList();
  private int  limit = 10;

  public BlockingQueue(int limit){
    this.limit = limit;
  }


  public synchronized void enqueue(Object item)
  throws InterruptedException  {
    while(this.queue.size() == this.limit) {
      wait();
    }
    if(this.queue.size() == 0) {
      notifyAll();
    }
    this.queue.add(item);
  }


  public synchronized Object dequeue()
  throws InterruptedException{
    while(this.queue.size() == 0){
      wait();
    }
    if(this.queue.size() == this.limit){
      notifyAll();
    }

    return this.queue.remove(0);
  }

}
   
```

> &nbsp;큐 크기가 크기 제한에 다다르면 enqueue()와 dequeue()에서 notifyAll()이 호출된다. 큐 크기가 제한에 다다르지 않은 상태로 enqueue() 나 dequeue()가 호출되면 쓰레드는 대기하지 않는다.

<br>
<br>
<br>

[참고](https://parkcheolu.tistory.com/29)
