# 람다식(Lamda Expression)

> &nbsp;&nbsp;Stream 연산들은 매개변수로 함수형 인터페이스(Functional Interface)를 받도록 되어있다. 람다식의 반환값은 함수형 인터페이스이기 때문에 Stream API를 정확히 이해하기 위해 람다식과 함수형 인터페이스에 대해 알고 있어야 한다.<br>
> &nbsp;&nbsp;람다 함수는 프로그래밍 언어에서 사용되는 개념으로 익명 함수(Anonymous functions)를 지칭하는 용어이다. 현재 사용되고 있는 람다의 근간은 수학과 기초 컴퓨터과학 분야에서의 람다 대수이다. 람다 대수는 간단히 말하자면 수학에서 사용하는 함수를 보다 단순하게 표현하는 방법이다.

<br>

# 람다의 특징

- 람다 대수는 이름을 가질 필요가 없다. : 익명 함수(Anonymous functions)
   - 익명함수란 말 그대로 이름 없는 함수이다. 익명 함수들은 공통으로 일급객체(First Class citizen)라는 특징을 가지고 있다.<br><br>
   - 일급 객체란 일반적으로 다른 객체들에 적용 가능한 연산을 모두 지원하는 객체를 가르킨다. 함수를 값으로 사용할 수도 있으며 파라미터로 전달 및 변수에 대입하는 등 연산이 가능하다.<br><br>
- 두 개 이상의 입력이 있는 함수는 최정적으로 1개의 입력만 받는 람다 대수로 단순화 될 수 있다. : 커링(Curring)<br><br>
- 람다식 내에서 사용되는 지역변수는 final이 붙지 않아도 상수로 간주된다.<br><br>
- 람다식으로 선언된 변수명은 다른 변수명과 중복될 수 없다.<br><br>

<br>

# 람다의 장단점

- ## 장점
   - 코드의 간결성 : 람다를 사용하면 불필요한 반복문의 삭제가 가능하며 복잡한 식을 단순하게 표현할 수 있다.<br><br>
   - 지연연산 수행 : 람다는 지연연산을 수행함으로써 불필요한 연산을 최소화 할 수 있다.<br><br>
   - 병렬처리 가능 : 멀티쓰레드를 활용하여 병렬처리를 사용할 수 있다.<br><br>


- ## 단점
   - 람다식의 호출이 까다롭다.<br><br>
   - 람다 Stream 사용 시 단순 for문 혹은 while문 사용 시 성능이 떨어진다.<br><br>
   - 불필요하게 너무 사용하게 되면 오히려 가독성을 떨어 뜨릴 수 있다.<br><br>
   - 재귀로 만들 경우 부적합하다.

<br>

# 람다의 표현식

- 람다는 매개변수 화살표 함수몸체로 이용하여 사용할 수 있다. ex) (매개변수) -> {함수몸체}<br><br>
- 함수몸체가 단일 실행문이면 괄호{}를 생략할 수 있다.<br><br>
- 함수몸체가 return문으로만 구성되어 있는 경우 괄호{}를 생랄햘 수 없다.<br><br>

<br>

```java

//정상적인 유형
() -> {}
() -> 1
() -> { return 1; }

(int x) -> x+1
(x) -> x+1
x -> x+1
(int x) -> { return x+1; }
x -> { return x+1; }

(int x, int y) -> x+y
(x, y) -> x+y
(x, y) -> { return x+y; }

(String lam) -> lam.length()
lam -> lam.length()
(Thread lamT) -> { lamT.start(); }
lamT -> { lamT.start(); }


//잘못된 유형 선언된 type과 선언되지 않은 type을 같이 사용 할 수 없다.
(x, int y) -> x+y
(x, final y) -> x+y  

```

# 람다식 예제
```java
// 익명 함수를 통한 Thread 구현
Thread thread = new Thread(new Runnable() {

   @Override
   public void run() {
      System.out.println("Start");
      try {
         Thread.sleep(1000);
      } catch (InterruptedException e) {
         System.out.println(e.toString());
      }
      System.out.println("End");
   }
});

// 람다식을 이용한 Thread 구현
Thread thread2 = new Thread(() -> {
   System.out.println("Start");
   try {
      Thread.sleep(1000);
   } catch (InterruptedException e) {
      System.out.println(e.toString());
   }
   System.out.println("End");
});

// 람다식 및 forEach를 이용한 컬렉션 순회
List<Integer> list = new ArrayList<Integer>();
list.add(1);
list.add(2);
list.add(3);
list.add(4);

list.forEach(x -> System.out.println(x));
list.forEach(System.out::println);

```

<br>
<hr>
<br>

<br>
<hr>
<br>

# 함수형 인터페이스(Functional Interface)
> &nbsp;&nbsp;함수형 인터페이스는 일반적으로 "구현해야 할 추상 메소드가 하나만 정의된 인터페이스"를 의미한다.
> &nbsp;&nbsp;@FunctionalInterface 어노테이션을 붙여줌으로써 함수를 1급 객체처럼 다룰 수 있게 해주는 어노테이션으로, 인터페이스에 선언하여 단 하나의 추상 메소드만 갖도록 제한하는 역할을 한다.


```java

// 구현해야 할 메소드가 한개이므로 Functional Interface이다.
@FunctionalInterface
public interface Math {

    public int Calc(int a, int b);
    
}


// 구현해야 할 메소드가 두개이므로 Functional Interface가 아니다. (오류 사항)
@FunctionalInterface
public interface Math {

    public int Calc(int a, int b);
    public int Calc2(int c, int d);
    
}

```
<br>
<hr>
<br>


# Functional Interface  예제

```java
public class Lamda_공부 {
   
   // 함수형 인터페이스
	@FunctionalInterface
	interface Math{
		
		public int cal(int a, int b);
      
	}
	
	public static void main(String[] args) {
   
      // 익명 함수
		System.out.println(new Math() {
			public int cal(int a, int b) {
				return a + b;
			}
		}.cal(1, 2));		
      
      // 람다식을 이용한 익명 함수
		Math plus = (a, b) -> a + b;
		System.out.println(plus.cal(1, 2));
		

	}
}

```

<br>
<hr>
<br>
















