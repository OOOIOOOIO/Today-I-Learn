# Lazy evaluation
> 실제로 필요로 해지는 경우 연산을 시작하는 것! 반대로는 eager evaluation이 있다. eager evaluation은 할당되자마자 연산을 시작한다. 기본적으로 Java 기조는 eager evaluation을 기본으로 한다. Java8이 나오면서 Java Lazy Evaluation을 좀 더 유연하게 사용할 수 있게 되었다.

<br>

## 예제
```java
// 메서드 호출 1초 후 문자열에 "a"가 포함되어 있는지 판단하는 함수
static boolean compute(String str){
  
  try{
    Thread.sleep(1000);
  }catch(InterruptedException ignore){
  }
  
  return str.contains("a");
    
}

// ========================================

// eager evaluation!
static String eagerMatch(boolean b1, boolean b2){
  return b1 && b2 ? "match" : "incompatible";

}

// lazy evalutaion!(자바 7 이전)
static String lazyMatch(){
  return compute("hello_1") && compute("hello_2") ? "match" : "incompatible";
}
```
```java
public void test(){
  boolean b1 = compute("hello_1");
  boolean b2 = compute("hello_2");
  
  eagerMatch(b1, b2);
}
```

- 예제에서 eagerMatch 메서드는 b1, b2가 모두 true일 때 결과가 반환된다. b1, b2 변수를 파라미터로 받고 있는데, 두 변수는 compute를 모두 실행시켜야 얻을 수 있다. 이를 통해 eagerMatch와 관계없이 compute 메서드는 모두 실행되는 것을 확인할 수 있다.(2초 걸림)
- lazyMatch 메서드는 && 논리연산자로 묶여 있다. 이 경우 첫번째 compute("hello_1")에 대한 평가가 이루어진다. 그리고 true라면 다음 compute("hello_2")에 대한 평가를 시작한다. 이를 통해 lazyMatch는 필요한 로직(연산)만 실행되는 것을 확인할 수 있다.(1초 걸림)

<br>
<hr>
<br>

## Java 8 이후
> &nbsp;Java 8에서 다양한 Functional 메서드들이 추가 되었다. 그 중 Supplier라는 메서드가 있는데, 스펙은 아래와 같다.

![image](https://user-images.githubusercontent.com/74396651/204556237-2d610039-c53a-4db2-9e4d-a1eb7e5bad8f.png)

> &nbsp;이를 이용하여 Lazy evalutaion을 구현해보자.

```java
public void test2(){
  Supplier<Boolean> a = () -> compute("hello_1");
  Supplier<Boolean> b = () -> compute("hello_2");
  
  lazyMatch(a, b);

}

static String lazyMatch(Supplier<Boolean> a, Supplier<Boolean> b){
  
  return a.get() && b.get() ? "match" : "incompatible";
}

```

## Lazy Evaluation 장점 및 특징
- 필요하지 않은 연산은 하지 않는 것이 가능하다는 점이다.
- 이는 성능적으로 우의미한 결과를 낳을 수 있다.
- 이러한 Lazy Evalutaion 방식은 Java 8 Stream에서 기본이 된다.


<br>

## 예제
> 1 ~ 30에서 3의 배수만 걸래내 10을 곱한 값 중 앞에서 3가지만 가져오기.

```java
List<Integer> list = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15);

list.stream()
  .filter(integer -> {
    return integer % 3 == 0; // 필터링
  })
  .map(integer -> integer * 10) // 변형
  .limit(3) // 제한
  .collect(Collectors.toList()); // 결과 리턴
```

- 이렇게 Straem을 이용했을 때 15번의 연산(1~15)을 해야 하지만 총 9번(1~9)의 연산만으로 원하는 결과를 얻을 수 있다.
- 이게 바로 Stream이 가진 Lazy Evaluation을 통해 일어난 것이다!



<br>
<br>
<br>
<br>
<br>
<br>
참조 : https://sabarada.tistory.com/m/154



