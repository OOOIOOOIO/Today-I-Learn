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
- 메소드 선언문의 synchronized 키워드는 이 메소드에 동기화를 걸겠다는 의미이다.
- 인스턴스 메소드의 동기화는 이 메소드를 가진 인스턴스(객체)를 기준으로 이루어진다. 
- 그러므로, 한 클래스가 동기화된 인스턴스 메소드를 가진다면, 여기서 동기화는 이 클래스의 한 인스턴스를 기준으로 이루어진다. 
- 그리고 한 시점에 오직 하나의 쓰레드만이 동기화된 인스턴스 메소드를 실행할 수 있다. 

<br>

### 스태틱 메소드 동기화
```java
public static synchronized void add(int value){
  this.count += value;
}
```
- 스태틱 메소드의 동기화는 인스턴스 메소드와 같은 방식으로 이루어진다.
- 스태틱 메소드 동기화는 이 메소드를 가진 클래스의 클래스 객체를 기준으로 이루어진다. 
- JVM 안에 클래스 객체는 클래스 당 하나만 존재할 수 있으므로, 같은 클래스에 대해서는 오직 한 쓰레드만 동기화된 스태틱 메소드를 실행할 수 있다.
- 만일 동기화된 스태틱 메소드가 다른 클래스에 각각 존재한다면, 쓰레드는 각 클래스의 메소드를 실행할 수 있다.
- 
 <br>
 
 ### 인스턴스 메소드 안의 동기화 블록
 ```java
public void add(int value){

   synchronized(this){
      this.count += value;   
   }
}
  ```
 - 동기화가 반드시 메소드 전체에 대해 이루어져야 하는 것은 아니다. 
 - 종종 메소드의 특정 부분에 대해서만 동기화하는 편이 효율적인 경우가 있다. 이럴 때는 메소드 안에 동기화 블록을 만들 수 있다.
 - 이렇게 메소드 안에 동기화 블록을 따로 작성할 수 있다. 메소드 안에서도 이 블록 안의 코드만 동기화하지만, 이 예제에서는 메소드 안의 동기화 블록 밖에 어떤 다른 코드가 존재하지 않으므로, 동기화 블록은 메소드 선언부에 synchronized 를 사용한 것과 같은 기능을 한다.
 - 동기화 블록이 괄호 안에 한 객체를 전달받고 있음에 주목하자. 예제에서는 'this' 가 사용되었다. 이는 이 add() 메소드가 호출된 객체를 의미한다. 
 - 이 동기화 블록 안에 전달된 객체를 모니터 객체(a monitor object) 라 한다. 이 코드는 이 모니터 객체를 기준으로 동기화가 이루어짐을 나타내고 있다. 동기화된 인스턴스 메소드는 자신(메소드)을 내부에 가지고 있는 객체를 모니터 객체로 사용한다.
- 같은 모니터 객체를 기준으로 동기화된 블록 안의 코드를 오직 한 쓰레드만이 실행할 수 있다.
- 
 <br>

### 스태틱 메소드 안의 동기화 블록
- 아래 두 메소드는 각 메소드를 가지고 있는 클래스 객체를 동기화 기준으로 잡는다.
 
 ```java
public class MyClass {

   public static synchronized void log1(String msg1, String msg2){
      log.writeln(msg1);
      log.writeln(msg2);
   }

   public static void log2(String msg1, String msg2){
      synchronized(MyClass.class){
         log.writeln(msg1);
         log.writeln(msg2);  
      }
   }
}
 ```
- 같은 시점에 오직 한 쓰레드만 이 두 메소드 중 어느 쪽이든 실행 가능하다. 
- 두 번째 동기화 블록의 괄호에 MyClass.class 가 아닌 다른 객체를 전달한다면, 쓰레드는 동시에 각 메소드를 실행할 수 있다.


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
