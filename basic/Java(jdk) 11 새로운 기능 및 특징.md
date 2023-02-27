> 문득 내가 왜 jdk 11을 쓰고 있지...라는 생각이 들어 정리하였다.

# Java 11

## 1. 새로운 String 메서드 추가
- strip(): 문자열 앞, 뒤의 공백 제거.

- stripLeading(): 문자열 앞의 공백 제거.

- stripTrailing(): 문자열 뒤의 공백 제거.

> trim() 과의 차이점은, trim() 은 U+0020 이하의 값만을 공백으로 인식하여 제거한다 (tab, CR, LF, 공백). 하지만 유니코드에서는 이 외에 다양한 공백 문자가 존재하는데, 이를 처리하기 위해서는 기존에는 Character.isWhitespace(int) 를 사용해야 했다. Java 11 부터는 strip() 으로 편하게 처리할 수 있다. 그리고 성능도 수 배 빠른 것으로 알려짐.

- isBlank(): 문자열이 비어있거나 공백만 포함되어 있을 경우 true 를 반환한다. 즉, String.trim().isEmpty() 호출 결과와 같다.

- lines(): 문자열을 라인 단위로 쪼개는 스트림을 반환.

- repeat(n): 지정된 수 만큼 문자열을 반복하여 붙여 반환:

```java
String str = "ABC";
String repeated = str.repeat(3);	// "ABCABCABC"
 ```



## 2. java.nio.file.Files 클래스 유틸 메서드 추가
- Path writeString(Path, String, Charset, OpenOption): 파일에 문자열을 작성하고 Path로 반환한다. 파일 오픈 옵션에 따라 작동 방식을 달리하며, charset을 지정하지 않으면 utf-8 이 사용된다. (오버로딩 메서드로 writeString(Path, String, OpenOption) 존재.)

- String readString(Path, Charset): 파일 전체 내용을 읽어서 String으로 반환하고, 파일 내용을 모두 읽거나 예외가 발생하면 알아서 close 한다. charset을 지정하지 않으면 utf-8 이 사용된다. (오버로딩 메서드로 readString(Path) 존재.)

- boolean isSameFile(Path, Path): 두 Path 가 같은 파일을 가리키면 true, 아니면 false 를 반환한다. 파일이 실제로 존재하지 않아도, Path 를 기준으로 해서 같은 위치면 true 로 판단한다.

 

## 3. Pattern.asMatchPredicate()
- Java 8 의 asPredicate는 matcher().find() 를 사용하는 것에 반해, asMatchPredicate() 는 matcher().match() 를 사용하는 Predicate를 반환한다.

 

## 4. Predicate.not(Predicate)
- 인자로 받은 Predicate의 부정형 Predicate를 반환한다.

 

## 5. 람다 파라미터로 var 사용:
(var n1, var n2) -> n1 + n2
- Java 8 에 등장했으나 Java 10 에서 사라졌다가 Java 11 에서 복귀한 기능.

- 람다는 타입을 스킵할 수 있는데 이걸 사용하는 이유는, @Nullable 등의 어노테이션을 사용하기 위해 타입을 명시해야 할 때.

- var 를 사용하려면 괄호를 써야하며, 모든 파라미터에 사용해야 하고, 다른 타입과 혼용하거나 일부 스킵은 불가능함:

```java 
(var s1, s2) -> s1 + s2 // 안 됨. s2 에도 var 필요.
(var s1, String y) -> s1 + y // 안 됨. String 과 혼용 불가.

var s1 -> s1 // 안 됨. 괄호 필요.

(var o1, var o2) -> o1 - o2 // 정상
 ```



## 6. Optional.isEmpty()
- Optional이 비어있을 때 true 반환.

 

## 7. TimeUnit.convert(Duration)
```java
TimeUnit c = TimeUnit.DAYS;
c.convert(Duration.ofHours(24));	// 2
c.convert(Duration.ofHours(72));	// 3
 ```
 
 

## 8. Nest-Based Access Control (JEP 181)
- Java 10 까지 nested 클래스에서 자신, 혹은 outer 클래스의 private 멤버에 리플렉션을 통한 접근을 시도하면 IllegalAccessException 이 발생했고, 이를 피하기 위해 setAccessible(true) 을 호출해야만 했음.

- Java 11 부터는 setAccessible 없이 private 멤버를 호출할 수 있음.

- java.lang.Class 에 다음 메서드들이 추가됨.

- getNestHost(): nested 클래스에서 호출하면 자신을 감싸고 있는 outer 클래스를 반환하고, outer 클래스에서 호출하면 자신을 반환.

- boolean isNestmateOf(Class): 자신이 아규먼트로 받은 Class의 nested 클래스일 때 true 를 반환함.

- Class[] getNestMembers(): 자신을 포함하여 중첩 관계에 있는 모든 클래스를 배열로 반환함. (outer, siblings)

 

## 9. Epsilon Garbege Collector (No-Op GC, JEP 318)
- JVM으로 하여금 메모리 할당을 관리하지만, 사용된 메모리를 재사용하지 않도록 함. 메모리를 다 사용하면 OutOfMemory가 발생하고 JVM은 셧다운된다.

- 어플리케이션 테스트에 사용됨. GC는 어플리케이션과 함께 작동하며, 오버헤드가 있어 어플리케이션 성능에 영향을 준다. No-OP GC를 적용하여 GC를 배제함으로써 순수 어플리케이션의 성능, 메모리 부하 등을 테스트할 수 있도록 한다. GC 적용 시의 성능과 비교하여 GC의 영향도를 측정할 수 있다.

- 짧은 시간 수행하고 종료되는 어플리케이션에 사용됨. 간단히 작동하고 마치는, 메모리 부하가 크게 염려되지 않는 어플리케이션에 적절하게 사용될 수 있음.

- 아래 아규먼트를 사용하여 활성화한다:
   - -XX:+UnlockExperimentalVMOptions -XX:+UseEpsilonGC
 

## 10. Dynamic Class-File Constants (JEP 309)
- Java 클래스 파일 형식은 CONSTANT_Dynamic 이라는 새로운 상수 풀 형식을 지원하도록 확장 되었다.

- 새 상수 풀을로드하면 invokedynamic  호출 사이트를 연결하는 것이 연결을 부트 스트랩 메서드에 위임 하는 것처럼 생성을 부트 스트랩 메서드에 위임한다.

- 이 기능은 성능을 향상시키고 언어 디자이너와 컴파일러 구현자를 대상으로 한다.



## 11. Java Flight Recorder  (JEP 328)
- 상업용 OracleJDK 에 제공되던 JFR이 OpenJDF에 포함된다.

- Java 어플리케이션으로부터 프로파일링, 어플리케이션 진단 데이터 등을 얻을 수 있음.

- 성능 오버헤드가 1% 미만으로 알려져 있어, 운영 환경에서 사용할 수 있음.
- 다음 매개 변수를 사용할 수 있다.
   - -XX:StartFlightRecording=duration=120s,settings=profile,filename=java-demo-app.jfr

 

## 12. HTTP Client (JEP 321)
- Java 표준 HTTP 클라이언트 API.

- 그간 HTTP 통신을 위해 사용된 코드보다 성능이 개선됨.

- HTTP/1.1, HTTP/2, WebSocket을 지원한다. 
```java
HttpClient httpClient = HttpClient.newBuilder()
  .version(HttpClient.Version.HTTP_2)
  .connectTimeout(Duration.ofSeconds(20))
  .build();
  
HttpRequest httpRequest = HttpRequest.newBuilder()
  .GET()
  .uri(URI.create("http://localhost:" + port))
  .build();
  
HttpResponse httpResponse = httpClient.send(httpRequest, HttpResponse.BodyHandlers.ofString());

assertThat(httpResponse.body()).isEqualTo("Hello from the server!");
```
 

## 13. java 파일 실행 (JEP 330)
- javac를 통한 컴파일 없이 java 파일을 실행할 수 있음:
```
$> java HelloWorld
Hello world!!
```
- java 파일에 main 메서드가 존재해야 함.

- 다음과 같이 클래스패스 지정:
   - java --class-path=/myclasspath ExecutionTest.java

- 클래스패스에 동일한 이름의 클래스가 존재하면 에러 발생. (java 확장자 무시.)

 

## 14. 기타 제거된 기능 및 옵션
- com.sun.awt.AWTUtilities 클래스

- Lucida 폰트 (Oracle JDK)

- appletviewer Launcher

- javax.imageio JPEG 플러그인 alpha 이미지 지원 X

- sun.misc.Unsafe.defineClass

- Thread.destroy()

- Thread.stop(Throwable)

- JVM-MANAGEMENT-MIB.mib

- SNMP 에이전트

- JavaFX (Oracle JDK)

- Java EE (JAX-WS, JAXB, JAF, Common Anotations) (JEP 320)

- CORBA (JEP 320)

 

## 15. deprecated된 기능 및 옵션
- ThreadPoolExecutor는 Finalization에 의존성을 갖지 않도록 (should not)

- Nashorn 자바스크립트 엔진 (JEP 335)

- -XX+AggressiveOpts(JVM 옵션)

- Pack200 툴 및 API (JEP 336)

- 스트림 기반 GSSContext 메서드


<br>
<br>
<br>
<br>

[참고1](https://parkcheolu.tistory.com/174)
[참고2](https://recordsoflife.tistory.com/350)
