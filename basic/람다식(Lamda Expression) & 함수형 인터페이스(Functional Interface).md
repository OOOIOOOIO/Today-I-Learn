# 람다식(Lamda Expression)

> &nbsp;&nbsp;Stream 연산들은 매개변수로 함수형 인터페이스(Functional Interface)를 받도록 되어있다. 람다식의 반환값은 함수형 인터페이스이기 때문에 Stream API를 정확히 이해하기 위해 람다식과 함수형 인터페이스에 대해 알고 있어야 한다.<br><br>
> &nbsp;&nbsp;람다 함수는 프로그래밍 언어에서 사용되는 개념으로 익명 함수(Anonymous functions)를 지칭하는 용어이다. 현재 사용되고 있는 람다의 근간은 수학과 기초 컴퓨터과학 분야에서의 람다 대수이다. 람다 대수는 간단히 말하자면 수학에서 사용하는 함수를 보다 단순하게 표현하는 방법이다.<br><br>
> &nbsp;&nbsp;람다식은 람다식 자체로 메서드의 매개변수가 될 수 있고, 메서드의 결과로 반환될 수 있다는 것이 핵심이다.(first classs function)

<br>

# 람다식의 등장배경
> &nbsp;하나의 CPU 안에 다수의 코어를 삽입하는 멀티 코어 프로세스들이 등장하면서 일반 프로그래머에게도 병렬화 프로그램에 대한 필요성이 생기기 시작했다.<br><br>
> &nbsp;이러한 추세에 대응하기 위해 자바8에서는 병렬화를 위한 컬렉션(배열, List, Set, Map)을 강화하였고, 이러한 컬렉션을 더 효율적으로 사용하기 위해 스트림이 추가 되었고 스트림을 효율적으로 사용하기 위해 함수형 프로그램이, 함수형 프로그램을 위해 람다가, 람다를 위해 함수형 인터페이스가 나오게 되었다.

- #### 빅데이터 지원 -> 병렬화 강화 -> 컬렉션 강화 -> 스트림 강화 -> 람다 도입 -> 인터페이스 명세 변경 -> 함수형 인터페이스 도입
<br>

# 람다의 특징

- 람다 대수는 이름을 가질 필요가 없다. : 익명 함수(Anonymous functions)
   - 익명함수란 말 그대로 이름 없는 함수이다. 익명 함수들은 공통으로 일급객체(First Class citizen)라는 특징을 가지고 있다.
   - 일급 객체란 일반적으로 다른 객체들에 적용 가능한 연산을 모두 지원하는 객체를 가르킨다. 함수를 값으로 사용할 수도 있으며 파라미터로 전달 및 변수에 대입하는 등 연산이 가능하다.
   - 일급 객체의 조건
   	 - 함수의 매개변수로 전달할 수 있어야 한다.
   	 - 함수의 결과값으로 반환될 수 있어야 한다.
   	 - 할당문의 대상이 될 수 있어야 한다.
   	 - 동등성 비교가 가능해야 한다.(equals)<br><br>
- 두 개 이상의 입력이 있는 함수는 최정적으로 1개의 입력만 받는 람다 대수로 단순화 될 수 있다. : 커링(Curring)
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
   - 람다로 인한 무명함수는 재사용이 불가능하다.<br><br>
   - 람다 Stream 사용 시 단순 for문 혹은 while문 사용 시 성능이 떨어진다.<br><br>
   - 불필요하게 너무 사용하게 되면 오히려 가독성을 떨어 뜨릴 수 있다.<br><br>
   - 재귀로 만들 경우 부적합하다.

<br>

## 람다의 이점

> ### 람다는 익명 클래스와 다르게 invokedynamic을 사용하는 것을 볼 수 있다.
- #### 이점
	 - 미래의 최적화를 위해 특정 전략을 고정하지 않은 것, 최대한 바이트코드로 고정되어 컴파일 되지 않게 하는 것
	 	 -  특정 Translation strategy(실제 자바 실행 로직으로 변환하는 과정 및 전략)을 런타임에서 결정할 수 있다. 미래에 JVM 스펙이 업데이트 되었다고 하더라도 소스코드 수정 혹은 재컴파일 없이 그대로 실행 가능하다.
	 	 -  람다가 컴파일 타임에 완벽하게 변환이 되었다고 한다면, 나중에 수정사항이 있을 경우 프로젝트를 모두 재 컴파일 해야 하는 일이 생길 수 있다.
	 - 클래스 파일 표현에 안정성을 가지는 방법
	 	 - 람다는 위의 두가지 이점을 가지기 위해 람다 표현은 <code>() -> {}</code> 실제 자바 메서드 실행 로직(바이트 코드로 나온 실행 메서드)으로, 컴파일 타임이 아닌 invokedynamic을 통해 런타임에서 로직을 연결하고 실행한다.
	 	 - 이를 통해, 실제 람도 표현을 실행하는 로직을 결정하는 전략을 런타임에서 lazy하게 결정할 수 있다는 장점이 있다. 

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
// (매개변수) -> {실행 코드}

public interface Functional {
    int cal(int a, int b);
}

public interface Functional2 {
    void print(String str);
}

public interface Functional3 {
    void noArgs();
}

// 1. 작성 가능한 모든 내용을 생략 없이 작성한 경우     
Functional2 functional2 = (String name) -> { System.out.println(name) };

// 2. 매개변수의 타입을 생략한 경우   
Functional2 functional2 = (name) -> { System.out.println(name) };    

// 3. 매개변수가 한개여서 소괄호를 생략한 경우    
Functional2 functional2 = name -> { System.out.println(name) };          

// 4. 실행 코드가 한 줄이어서 중괄호를 생략한 경우    
Functional2 functional2 = name -> System.out.println(name);    

// 5. 매개변수가 없어서 소괄호를 생략할 수 없는 경우    
Functional3 functional3 = () -> System.out.println("functiona3");    

// 6. 반환값이 있는 경우 return 키워드 사용하는 경우     
Functional functional = (a, b) -> {
       System.out.println("print");
       return a+b;
};

// 7. 실행 코드가 반환 코드만 존재하는 경우 키워드와 중괄호 생략한 경우    
Functional functional = (a, b) -> a+b;
```

<br>

## 람다식의 타입과 형변환
- 함수형 인터페이스로 람다식을 참조할 수 잇을 뿐 람다식의 타입이 함수형 인터페이스 타입과 일치하는 것이 아니다.
- 람다식은 익명 객체에서 온 것이고, 익명 객체는 타입이 없다.
	 - 정확히 타입은 있지만 컴파일러가 임의로 정하기 때문에 알 수 없는 것이다.
	 - 그래서 양변의 타입을 일치시키기 위해선 형변환이 필요하다.\
- 람다식은 MyFunction 인터페이스를 직접 구현하지는 못한다.
- 하지만 인터페이스를 구현한 클래스의 객체와 완전히 동일하기 때문에 형변환을 허용하며 생략 가능하다.
```java
MyFunction f = (MyFunction)(() -> {});

```

<br>

- 참고로 람다식은 분명 객체인데도 Object 타입으로 형변환할 수 없다.
- 람다식은 오직 함수형 인터페이스로만 형변환이 가능하다.
```java
Object obj = (Object)(() -> {}); // Error
```

<br>
<hr>
<br>

# 함수형 인터페이스(Functional Interface)
> &nbsp;&nbsp;함수형 인터페이스는 일반적으로 "구현해야 할 추상 메소드가 하나만 정의된 인터페이스"를 의미한다.<br>
> &nbsp;&nbsp;함수형 인터페이스를 사용하는 이유는 자바의 람다식은 함수형 인터페이스로만 접근이 가능하기 때문이다.<br>
> &nbsp;&nbsp;@FunctionalInterface 어노테이션을 붙여줌으로써 함수를 1급 객체처럼 다룰 수 있게 해주는 어노테이션으로, 인터페이스에 선언하여 단 하나의 추상 메소드만 갖도록 제한하는 역할을 한다. static, default 메서드는 허용한다.


```java
// 구현해야 할 메소드가 한개이므로 Functional Interface이다.
@FunctionalInterface
public interface Math {

    // 추상 메서드는 오직 1개만 존재
    public int Calc(int a, int b);
    
    // static 메서드는 있어도 된다.
    static void temp() { };
    
    // default 메서드는 있어도 된다.
    default void temp2() { };
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
- 익명 객체를 람다식으로 대체 가능한 이유
   - 인터페이스를 구현한 익명 객체의 메서드와 람다식의 매개변수 타입과 개수 그리고 반환값이 일치하기 때문에 대체 가능하다.

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

## java.util.function 패키지
> 자바에서는 자주 사용되는 함수형 인터페이스들을 'java.util.function' 패키지에 미리 정의해 놓았다. 이 패키지에 정의된 인터페이스를 사용하고 만약 없을 경우 정의해서 사용하는 게 좋다.

<br>

## 함수형 인터페이스

```
< 자주 사용하는 타입인자 >

<T> : Type
<E> : Element
<K> : Key
<N> : Number
<V> : Value
<R> : Result
```

<hr>

<code>형식 : 함수형 인터페이스 : 메서드</code>

### 기본적인 함수형 인터페이스

- java.lang.Runnable : void run();
- Supplier&lt;T&gt; : T get();
- Consummer&lt;T&gt; : void accept(T t);
- Function&lt;T, R&gt; : R apply(T t);
- Predicate&lt;T&gt; : boolean test(T t);

<hr>

### 파라미터가 두 개인 함수형 인터페이스

- BiConsumer&lt;T, U&gt; : void accept(T t, U u);
- BiPredicate&lt;T, U&gt; : boolean test(T t, U u);
- BiFunction&lt;T, U, R&gt; : R apply(T t, U u);

> 파라미터가 3개 이상인 함수형 인터페이스의 경우 직접 정의하여 사용해야 한다. 

<hr>

### 하나의 파라미터를 받고 동일한 타입을 리턴하는 함수형 인터페이스

- UnaryOperator&lt;T&gt; : T apply(T t);
- BinaryOperator&lt;T&gt; : T apply(T t1, T t2);

> 대부분 람다식은 단순하기 때문에 두 개의 파라미터만으로도 충분히 정의가 되기 때문에 패키지에 대부분 포함되어 있다.

<hr>

> 제네릭을 사용하는 함수형 인터페이스는 기본형(Primitive Type)을 사용할 때, 랩퍼(Wrapper) 클래스를 사용해야하는 비효율이 있다.
> 따라서 기본형(Primitive Type)을 사용하는 함수형 인터페이스들도 제공된다.

### 기본형(Primitive Type)을 사용하는 함수형 인터페이스

- IntFunction&lt;R&gt; : R apply(int value);
- LongFunction&lt;R&gt; : R apply(long value);
- DoubleFunction&lt;R&gt; : R apply(double value);

<br>

- ToIntFunction&lt;T&gt; : int applyAsInt(T t)
- ToLonFunction&lt;T&gt; : long applyAsLong(T t)
- ToDoubleFunction&lt;T&gt; : double applyAsDouble(T t)

> 함수형 인터페이스의 이름을 살펴보면 어떤 기본 타입과 연관되어 있는지 알 수 있다. 이 밖에도 IntTolongFunction, DoubleToIntFunction, ObjIntConsumer&lt;T&gt; 등도 존재한다.

<hr>

### 컬렉션과 함께 사용할 수 있는 함수형 인터페이스

<code>형식 : 인터페이스 | 메서드 : 설명</code>

- Collection | boolean removeIf(Perdicate&lt;E&gt; filter); : 조건에 맞는 엘리먼트 삭제
- List | void replaceAll(UnaryOperator&lt;E&gt; operator); : 모든 엘리먼트에 operator를 적용하여 대체(replace)
- Iterable | void forEach(Consumer&lt;T&gt; action); : 모든 엘리먼트에 action 수행
- Map | V compute(K key, BiFunction&lt;K, V, V&gt; f); : 지정된 키에 해당하는 값에 f를 수행
- Map | V computeIfAbsent(K key, Function&lt;K, V&gt; f); : 지정된 키가 없으면 f 수행 후 추가
- Map | V computeIfPresent(K key, BiFunction&lt;K, V, V&gt; f); : 지정된 키가 있을 때, f 수행
- Map | V merge(K key, V value, BiFunction&lt;K, V, V&gt; f); : 모든 엘리먼트에 Merge 작업 수행, 키에 해당하는 값이 있으면 f를 수행해 병합 후 할당
- Map | void forEach(BiConsumer&lt;K, V&gt; action); : 모든 엘리먼트에 action 수행
- Map | void replaceAll(BiFunction&lt;K, V, V&gt; f); : 모든 엘리먼트에 f 수행 후 대체



<br>
<hr>
<br>

## Function의 합성

![image](https://user-images.githubusercontent.com/74396651/214798118-227d6b93-15ed-46aa-b4dc-e9da217faa36.png)

<br>

### 함수의 합성을 지원하는 디폴트 메서드

- default &lt;V&gt; Function &lt;T, V&gt; andThen (Function &lt;? super R, ? extends V&gt; after);
- default &lt;V&gt; Function &lt;V, R&gt; compose (Function &lt;? super V, ? extends V&gt; before);
- static &lt;V&gt; Function &lt;T, T&gt; identity();

> f.andThen(g)를 수행하면 f 함수를 실행한 결과 값을 다시 g 함수의 인자로 전달하여 결과를 얻는 새로운 함수를 만들어 낸다. 이 때, f함수의 리턴 타입이 g 함수의 파라미터 타입과 호환되어야 한다.<br>
> 반대로 f.compose(g)를 수행할 경우 g 함수르 먼저 적용하고 f를 나중에 적용하는 함수를 만들어 낸다. 마찬가지로 먼저 적용되는 함수 g의 리턴 타입과 나중에 적용되는 함수 f의 파라미터 타입이 맞아야 한다.<br>
> identity 메소드는 "항등함수"를 만들어 낼 때 사용된다. 항등함수는 잘 사용되는 편은 아니며 Stream의 map()으로 변환 작업할 때 변환 없이 그래도 처리하는 경우에 사용된다.


<br>
<hr>
<br>

## Predicate 결합

![image](https://user-images.githubusercontent.com/74396651/214800968-1b20bba2-29d0-4940-8248-fce5399a56a4.png)

<br>

### Prediate을 결합할 때 사용하는 디폴트 메소드

- default Predicate&lt;T&gt; and (Predicate&lt;? super T&gt; other);
- default Predicate&lt;T&gt; or (Predicate&lt;? super T&gt; other);
- default Predicate&lt;T&gt; negate();
- static &lt;T&gt; Predicate&lt;T&gt; isEqual(Object targetRef);
- 예시
```java
Predicate<Integer> greater = x -> x > 10;
Predicate<Integer>
```






























