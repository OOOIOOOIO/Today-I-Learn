# Synchronized
> 멀티 쓰레드를 잘 사용하면 프로그램적으로 좋은 성능을 낼 수 있지만, 멀티쓰레드 환경에서 반드시 고려해야할 점인 쓰레드간 동기화를 해결하지 못한다면 큰일난다..<br>
> 예를 들어 쓰레드간 서로 공유하고 있는(수정 가능) 데이터가 있다. 쓰레드간 동기화가 되지 않은 상황에서 멀티 쓰레드 프로그램을 돌리면 data의 안정성과 신뢰성을 보장할 수 없다.<br>
> data의 안정성과 신뢰성을 보장하기 위해선 Thread-safe 하게 설계해야 하며 자바에서는 synchronized 키워드를 제공해 쓰레드간 동기화를 시켜 data를 Thread-safe하게 만들어 준다.

<br>

## 자바에서의 Sychronized 키워드
- 자바에서 지원하는 synchronized 키워드는 여러개의 쓰레드가 한개의 자원을 사용하고자 할 때, 현재 데이터를 사용하고 있는 해당 쓰레드를 제외하고 나머지 쓰레드들을 데이터에 접근할 수 없게 막는 개념이다.
- 동기화는 객체에 대한 동기화로 이루어지는데(synchronized on some object), 같은 객체에 대한 모든 동기화 블록은 한 시점에 오직 한 쓰레드만이 블록 안으로 접근하도록(실행하도록) 한다. 블록에 접근을 시도하는 다른 쓰레드들은 블록 안의 쓰레드가 실행을 마치고 블록을 벗어날 때까지 블록(blocked) 상태가 된다.
   - synchronized 키워드를 사용하면 자바 내부적으로 메서드느 변수에 동기화를 하기 위해 block, unblock 처리를 하게 되는데, 이런 처리들이 만약 너무 많아지게 되면 성능저하를 일으키는 것이다.
- 메소드 레벨의 동기화는 해당 인스턴스 자체로 락을 걸어버린다.
- 자바 동기화 블록은 메소드나 블록 코드에 동기화 영역을 표시하며 자바에서 경합 조건을 피하기 위한 방법으로 쓰인다. 
- synchronized 키워드는 네가지 유형의 블록에 쓰인다.
   - 인스턴스 메소드
   - 스태틱 메소드
   - 인스턴스 메소드 코드 블록
   - 스태틱 메소드 코드 블록

<br>

### 인스턴스 메소드 동기화
```java
public synchronized void add(int value){
  this.count += value;
}
```



<br>




<br>
<hr>
<br>



## 멀티쓰레드 예제

```java
package com.example.demo.synchronizedTest;

public class SynchronizedMultiThread_1 {

    public static void main(String[] args) {
        Task task = new Task();
        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);

        t1.setName("t1-Thread");
        t2.setName("t2-Thread");

        t1.start();
        t2.start();

    }

}

class Task implements Runnable {
    Account acc = new Account(); // 여러 쓰레드(멀티쓰레드)에서 객체 공유

    @Override
    public void run() {
        while(acc.balance > 0 ){
            // 100, 200, 300 중의 한 값을 임의로 선택해서 출금(withDraw)한다.
            int money = (int)(Math.random() * 3 + 1) * 100;
            acc.withDraw(money);
        }
    }
}

class Account{
    int balance = 1000;

    public void withDraw(int money){
        if (balance >= money) {
            try {
                Thread thread = Thread.currentThread();

                System.out.println(thread.getName());

                Thread.sleep(1000);

                System.out.println(thread.getName()+" before balance:" + balance);
                balance -= money;
                System.out.println(thread.getName()+" money:" + money);

                System.out.println(thread.getName()+" after balance:" + balance);

            }catch (Exception e) {}
        }
    }
}

```

### 결과
```
t1-Thread
t2-Thread
t1-Thread before balance:1000
t2-Thread before balance:1000
t2-Thread money:100
t1-Thread money:200
t2-Thread after balance:700
t1-Thread after balance:700
t2-Thread
t1-Thread
t2-Thread before balance:700
t1-Thread before balance:700
t2-Thread money:100
t1-Thread money:200
t2-Thread after balance:400
t2-Thread
t1-Thread after balance:400
t1-Thread
t2-Thread before balance:400
t2-Thread money:100
t1-Thread before balance:400
t1-Thread money:200
t1-Thread after balance:100
t1-Thread
t2-Thread after balance:100
t2-Thread
t1-Thread before balance:100
t2-Thread before balance:100
t2-Thread money:100
t2-Thread after balance:-100
t1-Thread money:100
t1-Thread after balance:-100
```

<br>

## 사용법

### 메서드에 사용하는 경우
```java
public synchronized void method(//TODO);
```

```java
package com.example.demo.synchronizedTest;

public class SynchronizedMultiThread_2 {

    public static void main(String[] args) {
        Task2 task2 = new Task2();
        Thread t1 = new Thread(task2);
        Thread t2 = new Thread(task2);

        t1.setName("t1-Thread");
        t2.setName("t2-Thread");

        t1.start();
        t2.start();

    }

}

class Task2 implements Runnable {
    Account2 acc = new Account2(); // 여러 쓰레드(멀티쓰레드)에서 객체 공유


    @Override
    public void run() {
        while(acc.balance > 0 ){
            // 100, 200, 300 중의 한 값을 임의로 선택해서 출금(withDraw)한다.
            int money = (int)(Math.random() * 3 + 1) * 100;
        
            acc.withDraw(money);

        }
    }
}

class Account2{
    int balance = 1000;

    public synchronized void withDraw(int money){
        if (balance >= money) {
            try {
                Thread thread = Thread.currentThread();

                System.out.println(thread.getName());

                System.out.println(thread.getName()+" before balance:" + balance);
                balance -= money;
                System.out.println(thread.getName()+" money:" + money);

                System.out.println(thread.getName()+" after balance:" + balance);
                Thread.sleep(1000);

            }catch (Exception e) {}
        }
    }
}

```

<br>

### 결과
```
 t1-Thread
 t1-Thread before balance:1000
 t1-Thread money:300
 t1-Thread after balance:700
 t2-Thread
 t2-Thread before balance:700
 t2-Thread money:100
 t2-Thread after balance:600
 t1-Thread
 t1-Thread before balance:600
 t1-Thread money:300
 t1-Thread after balance:300A
 t2-Thread
 t2-Thread before balance:300
 t2-Thread money:200
 t2-Thread after balance:100
 t2-Thread
 t2-Thread before balance:100
 t2-Thread money:100
 t2-Thread after balance:0
 ```
 
<br>
<hr>
<br>

### 객체 변수에 사용하는 경우(block문)
```java
private Object obj = new Object();

public void method(){ 
  sychronized(obj){
    //TODO
  }
}
```

```java
package com.example.demo.synchronizedTest;

public class SynchronizedMultiThread_2 {

    public static void main(String[] args) {
        Task2 task2 = new Task2();
        Thread t1 = new Thread(task2);
        Thread t2 = new Thread(task2);

        t1.setName("t1-Thread");
        t2.setName("t2-Thread");

        t1.start();
        t2.start();

    }

}

class Task2 implements Runnable {
    Account2 acc = new Account2(); // 여러 쓰레드(멀티쓰레드)에서 객체 공유


    @Override
    public void run() {
        while(acc.balance > 0 ){
            // 100, 200, 300 중의 한 값을 임의로 선택해서 출금(withDraw)한다.
            int money = (int)(Math.random() * 3 + 1) * 100;
            synchronized (acc){
                acc.withDraw(money);
            }

        }

//        synchronized (acc){
//            while(acc.balance > 0 ){
//                // 100, 200, 300 중의 한 값을 임의로 선택해서 출금(withDraw)한다.
//                int money = (int)(Math.random() * 3 + 1) * 100;
//
//                acc.withDraw(money);
//            }
//        }
    }
}

class Account2{
    int balance = 1000;

    public void withDraw(int money){
        if (balance >= money) {
            try {
                Thread thread = Thread.currentThread();

                System.out.println(thread.getName());

                System.out.println(thread.getName()+" before balance:" + balance);
                balance -= money;
                System.out.println(thread.getName()+" money:" + money);

                System.out.println(thread.getName()+" after balance:" + balance);
                Thread.sleep(1000);

            }catch (Exception e) {}
        }
    }
}


```

<br>

### 결과
```
t1-Thread
t1-Thread before balance:1000
t1-Thread money:300
t1-Thread after balance:700
t2-Thread
t2-Thread before balance:700
t2-Thread money:100
t2-Thread after balance:600
t1-Thread
t1-Thread before balance:600
t1-Thread money:100
t1-Thread after balance:500
t2-Thread
t2-Thread before balance:500
t2-Thread money:200
t2-Thread after balance:300
t1-Thread
t1-Thread before balance:300
t1-Thread money:300
t1-Thread after balance:0


```

#### 이처럼 synchronized 키워드를 사용해 공유데이터인 변수 balacne를 thread-safe하게 만들었다. 때문에 데이터나 메서드를 점유하고 있는 쓰레드가 온전히 자신의 작업을 마칠 수 있었다.
