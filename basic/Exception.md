# 예외처리 Exception Handling

- &nbsp;자바에서의 예외는 Error, 일반 예외(Checked Exception, OtherException)와 실행 예외(Unchecked Exception, RuntimeException)가 있다.<br>&nbsp;전자인 Checked Exception은
개발자가 반드시 예외 처리를 직접 진행해야 한다. 후자인 Unchecked Exception 는 명시적인 예외 처리가 강제되는 것이 아니므로 개발자가 예외처리를 
직접하지 않아도 된다.<br>&nbsp;Checked Exception은  컴파일 시 예외가 발생하고 Unchecked Exception은 컴파일은 통과하지만 런타임 시 예외가 발생한다.

<br>

![image](https://user-images.githubusercontent.com/74396651/160061275-0a491117-85e4-4ca4-81e9-f9d1f8f14211.png)

<br>

## Error

- &nbsp;Error는 메모리 부족(OutOfMemoryError), 스택오버플로우(StackOverFlowError)처럼 차바 가상 기계(JVM)나 하드웨어 등 시스템의 문제로 발생하는 것을 의미한다.<br>&nbsp;
즉, 개발자가 처리할 수 있는 영역이 아니기 때문에 Error가 발생하면 프로그램을 종료시키는 것이 보통이다.

<br>

![image](https://user-images.githubusercontent.com/74396651/160062221-78554302-df27-46b7-a47b-b02fb14c695e.png)

<br>

## Checked Exception

- &nbsp;모든 예외 클래스는 java.lng.Exception 클래스를 상속받는다. 
- &nbsp;Exception 클래스 자체는 checked exception 이다.
- &nbsp;Exception 클래스는 Throwable 클래스의 자식 클래스이다.
- &nbsp;반드시 throws를 통해 예외를 던지거나 try-catch로 예외 처리를 해주어야 하는 강제성이 있다.
- &nbsp;컴파일 시점에 체크된 exception이다.
- &nbsp;예외 발생시 roolback 처리를 하지 않는다.(트랜잭션 처리)

<br>

## Checked Exception 종류

- ClassNotFoundException : 클래스를 찾지 못하는 경우
- SqlException : 데이터 소스에 액세스하는 동안 발생하는 예외
- IOException : 스트림, 파일 및 디렉터리를 사용하여 정보에 액세스하는 동안 throw되는 예외
- 등등 ...
<br>

<hr>

<br>

## Unchecked Exception(RuntimeException)

- &nbsp;모든 예외 클래스는 java.long.Exception 클래스를 상속받는다. 
- &nbsp;Exception 클래스의 자식 클래스 중 RuntionException 클래스는 Unchecked Exception이다.
- &nbsp;RuntimeException의 자식 클래스들 모두 포함, Unchecked Exception이고 try-catch문으로 예외처리를 직접 하기 보다는 예외가 발생하지 않도록 프로그래머가 주의해야 한다.
- &nbsp;런타임 시점에 체크된 exception이다.
- &nbsp;예외 발생시 roolback 처리를 해야 한다.(트랜잭션 처리)

<br>

## Unchecked Exception 종류

- ArithmeticException : 정수를 0으로 나누었을 때
- ArrayStoreException : 배열의 타입과 다른 타입의 객체를 넣으려는 경우
- ArrayIndexOutOfBoundsException : 배열을 참조하려는 인덱스가 잘못된 경우
- NullPointerException : Null 객체를 참조할 때 발생
- OutOfMemoryException : 사용 가능한 메모리가 없는 경우
- ... 등등 너무 많다.


## 간단히 생각해보면 Unchecked Exception이란 사람이 코드를 짜면서 생길 수 있는 예외이다.


<br>

# 사용자 정의 예외

- &nbsp;만약 사용자 정의 예외 클래스를 만들게 된다면<br>
Checked Exception : extends Exception / Unchecked Exception : extends RuntimeException 을 상속하면 된다.



<br>

```java

ex) class의 이름은 사용자가 임의로 설정하면 되고 extends를 통해 원하는  예외를 상속하면 된다.


public class AnyCreateException extends Exception {

      public AnyCreateException() {;}; // 기본 생성자
      
      public AnyCreateException(String message) {//에외 메시지를 전달하기 위해 String 타입의 매개 변수를 갖는 생성자.
          super(message);

      }
}
```

<br>

# 예외 떠넘기기

- 메소드 내부에서 예외가 발생할 수 있는 코드를 작성할 때 , try-catch 블록으로 예외 처리 하는 것이 기본이지만, 경우에 따라서는
메소드를 호출한 곳으로 예외 처리를 떠넘길 수도 있습니다.<br>&nbsp;이 때 사용하는 키워드가 throws 이다. throws가 붙은 메소드를 사용하는 곳에서
반드시 try-catch를 사용해 처리해주어야 한다.<br>&nbsp;메인메소드에서 throws를 통해 예외를 넘기게 되면 JVM에서 최종적으로 처리를 하게 된다.

<br>

## throw
- 예외를 발생시키는 것. 메소드 내에서 상위 블럭으로 예외를 던지는 것.<br>&nbsp;억지로 에러를 발생시킬 때도 사용되지만
현재 메소드의 에러를 처리한 후에 상위 메소드에 에러 정보를 줌으로써 상위 메소드에서도 에러가 발생한 것을 감지할 수 있다.<br>&nbsp;
throw 예약어 뒤에는 java.lang.Throwble 클래스를 상속받은 자식 클래스의 객체를 지정해야 한다.

<br>

## thorws
- 예외를 던지는 것(throw도 마찬가지로 던진다). 현재 메소드에서 상위 메소드로 예외를 던진다.<br>&nbsp;
메소드를 정의할 때 throws 예약어를 시그니쳐에 추가하면 "그 메소드를 호출하는 곳"에서 예외 처리를 해야한다.<br>&nbsp;
Function throws SomeException이라는 문장을 생각하면 이해하기 쉬울 것이다.<br>&nbsp;
Function이 SomeException(예외)를 던진다는 뜻으로 Function을 사용하는 곳(호출하는 곳)을 try-catch 블록으로 감싸준다.

<br>

### throw는 프로그래머의 판단에 따른 처리하고, 실제로 예외를 발생시키는 것.<br>
### throws는 예외를 자신이 처리하지 않고, 자신을 호출하는 메소드에게 책임을 전가 하는 것. 




