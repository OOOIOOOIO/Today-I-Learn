# Generic
> Java에서 제네릭은 데이터의 타입을 일반화하는 것을 의미한다. 클래스나 메소드에서 사용할 데이터의 타입을 컴파일 시에 미리 지정하는 방법이다. 제네릭(Generic)이라는 단어의 의미에도 '일반적인'이라는 뜻이 있다.

<br>
<hr>
<br>

## 장점
- 제네릭을 사용할 경우 타입에 대한 고려 없이 코드를 깔끔하게 작성할 수 있으며 코드의 재사용성이 높아진다.
- 제네릭을 사용할 경우 잘못된 타입을 사용할 경우 컴파일 시점에서 알 수 있다.

<br>
<hr>
<br>

## 단점


<br>
<hr>
<br>

## 제네릭에서 쓰이는 문자

![image](https://user-images.githubusercontent.com/74396651/217191431-01d6d787-1b2a-4359-91ae-2c9f4450a767.png)

<hr>

## 사용법

```java
pubilc class TestClass<T, U, ...> { //TODO }
public interface<T, U, ...> { //TODO }

```

![image](https://user-images.githubusercontent.com/74396651/217183045-edfbd879-a198-441e-855b-64daa7045b09.png)


<br>
<hr>
<br>

## 제네릭 한정적 타입 매개변수
> 제네릭으로 사용할 수 있는 타입을 한정할 수도 있다. 예를 들어 특정 인터페이스를 구현한 클래스만 인자로 받을 수 있도록 클래스 선언 시 제네릭 타입으로 타입 매개변수를 제한할 수 있다.
```java
public class TestClass <T extends NewClass>
```
- 클래스의 상속을 정의할 때 사용한 extends 키워드를 제네릭 정의에 사용하면, 제네릭 타입을 제한한다는 의미가 된다.
- 위 코드에서 TestClass는 NewClass 혹은 New Class의 서브 클래스만 타입으로 가지도록 제한하였다.

```java
public class TestClass <T supder NewClass>
```
- 위 코드는 TestClass가 NewClas의 상위 클래스만 타입으로 가지도록 제한하였다.


<br>
<hr>
<br>

## 제네릭 와일드 카드

```java
public class Calcu {
    public void printList(List<?> list) {
       for (Object obj : list) {
    	   System.out.println(obj + " ");  
       }
    }

    public int sum(List<? extends Number> list) {
      int sum = 0;
      for (Number i : list) {
    	  sum += i.doubleValue();  
      }
      return sum;
    }

   public List<? super Integer> addList(List<? super Integer> list) {
      for (int i = 1; i < 5; i++) {
    	 list.add(i); 
      }
      return list;
    }
}
```
> 와일드카드 타입에는 총 세가지의 형태가 있으며 물음표(?) 키워드로 표현된다.

- 제네릭타입<?> : 타입 파라미터를 대치하는 것으로 모든 클래스나 인터페이스타입이 올 수 있습니다.

- 제네릭타입<? extends 상위타입> : 와일드카드의 범위를 특정 객체의 하위 클래스만 올 수 있습니다.

- 제네릭타입<? super 하위타입> : 와일드카드의 범위를 특정 객체의 상위 클래스만 올 수 있습니다.

<br>
<hr>
<br>

## 제네릭 메서드
> 클래스와 마찬가지로 메서드 역시 제네릭으로 만들 수 있다. 참고로 제네릭 메소드를 사용하기 위해 클래스까지 제네릭일 필요는 없다.

```java
public 제네릭명시 리턴타입 메소드명(파라미터타입 파라미터 변수명){

}

public <T> T testMethod(T param){
  //TODO
}

public static <T extends CharSequence> void testMethod(T param){
  System.out.print(param.charAt(0));
}
```
- 제네릭 클래스를 사용하고 그 클래스 내에 제네릭 메소드를 사용할 경우, 클래스의 T와 메소드의 T는 전혀 관련이 없다.
- 제네릭 메소드가 필요한 이유는 static 메소드 때문이다. 자바의 제네릭은 new 메소드를 이용해서 객체를 생성할 때 타입을 받아 구체화 된다. 하지만 static 클래스는 객체를 생성하지 않기 때문에 클래스에 정의된 제네릭을 사용할 수 없다.


<br>
<hr>
<br>

## 제내릭을 사용할 수 없는 경우
- 제네릭으로 배열을 생성할 수 없다.
   - new 연산자를 통햅 배열을 생성할 경우, new 연산자는 heap 영역에 충분한 공간이 있는지 확인 후 메모리를 확보하는 역할을 한다.
   - 하지만 충분한 공간이 있는지 확인하기 위해선 타입을 알아야 한다. 제네릭을 사용할 경우 컴파일 시점에 타입 T가 무엇인지 알 수 없기 때문에 제네릭을 사용해 배열을 사용할 수 없다.
- static 변수를 제네릭으로 사용할 수 없다.
   - 제네릭을 사용할 경우 하나의 공유변수가 생성되어 인스턴스에 따라 타입이 바뀌기 때문에 제네릭을 사용할 수 없다. 







