# Serialization(직렬화) - Java

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/cc8b61da-b1e0-4b40-a8a3-1540c504a511)
> Serializable 인터페이스를 보면 아무것도 없는 것을 확인할 수 있다. 하지만 우리가 만든 클래스가 파일에 읽거나 쓸 수 있도록 하거나, 다른 서버로 보내거나 받을 수 있게 하려면 반드시 Serializable 인터페이스를 상속받아야 한다.

- 자바에서의 직렬화란 자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 바이트(byte) 형태로 변환하는 기술과 바이트로 변환된 데이터를 다시 객체로 변환하는 기술(역직렬화)를 아울러서 이야기 한다.
- 시스템적으로 이야기하자면 JVM(Java Virtual Machine)의 Runtime Data Area(힙, 스택 메모리)에 상주되어 있는 객체 데이터를 바이트 형태로 변환하는 기술과 직렬화된 바이트 형태의 데이터를 객체로 변환하여 JVM으로 상주시키는 형태를 이야기 한다.

## 예시

```
import java.io.Serializable;

public class Member implements Serializable {

    private String name;
    private String email;
    private int age;

    public Member(String name, String email, int age) {
        this.name = name;
        this.email = email;
        this.age = age;
    }

    @Override
    public String toString() {
        return String.format("Member{name='%s', email='%s', age='%s',", name, email, age);
    }
}
```

```
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.util.Base64;

public class ObjectSerializableExam{

    public static void main(String[] args) throws Exception {
        Member member = new Member("성호킴", "polite159@gmail.com", 26);
        byte[] serializedMember;

        try(ByteArrayOutputStream baos = new ByteArrayOutputStream()) {
            try(ObjectOutputStream oos = new ObjectOutputStream(baos)) {
                oos.writeObject(member); // 저장
                // 직렬화된 member 객체
                serializedMember = baos.toByteArray();
            }
        }
        // base64로 인코딩한 문자열
        String base64Member = Base64.getEncoder().encodeToString(serializedMember);

        // base64로 디코딩한 문자열
        byte[] deserializedMember = Base64.getDecoder().decode(base64Member);

        try(ByteArrayInputStream bais = new ByteArrayInputStream(deserializedMember)) {
            try(ObjectInputStream ois = new ObjectInputStream(bais)) {
                Object objectMember = ois.readObject();
                // member 객체로 역직렬화
                Member readMember = (Member) objectMember;
                System.out.println(member);
            }
        }
    }
}
```

## 직렬화 종류
- 문자열 형태의 직렬화 방법
  - 직접 데이터를 문자열 형태로 확인 가능한 직렬화 방법입니다. 범용적인 API나 데이터를 변환하여 추출할 때 많이 사용됩니다. 표형태의 다량의 데이터를 직렬화시 CSV가 많이 쓰이고 구조적인 데이터 이전에는 XML을 많이 사용했지만 최근에는 JSON을 많이 사용하고 있습니다.

## 직렬화를 사용하는 경우
> JVM의 메모리에만 상주되어 있는 객체 데이터를 그대로 영속화(persist)가 필요할 때 사용된다. 시스템이 종료되더라도 없어지지 않는 장점을 가지며 영속화된 데이터이기 때문에 네트워크로 전송도 가능하다. 그리고 필요할 때 직렬화 된 객체 데이터를 가져와서 역직렬화하여 객체를 바로 사용할 수 있게 된다.
- 서블릿 세션들은 대부분 세션의 Java 직렬화를 지원하고 있다. 단순히 세션을 서블릿 메모리 위에서 운용한다면 직렬화가 필요없지만, 파일로 저장하거나 세션 클러스터링, DB를 저장하는 옵션등을 선택하게 되면 세션 자체가 직렬화되어 저장되어 전달됩니다.
- 캐시에서도 직렬화는 사용된다. 주로 DB를 조회한 후 가져온 데이터 객체 같은 경우 실시간 형태로 요구하는 데이터가 아니라면 메모리, 외부 저장소, 파일 등을 저장소를 이용해서 데이터 객체를 저장한 후 동일한 요청이 오면 DB를 다시 요청하는 것이 아니라 저장된 객체를 찾아서 응답하게 하는 형태를 캐시를 사용한다라고 한다. 캐시를 이용하면 DB 리소스를 절약할 수 있기 때문에 많은 시스템에서 자주 활용됩니다. 이렇게 캐시할 부분을 자바 직렬화된 데이터를 저장해서 사용된다.


## 직렬화가 필요한 경우
- 생성한 객체를 파일로 저장할 일이 있을 경우
- 저장한 객체를 읽을 일이 있을 경우
- 다른 서버에서 생성한 객체를 받을 경우

## Java가 파일을 구분하는 법
A라는 서버에서 B라는 서버로 SerialDTO라는 클래스의 객체를 전송할 때. 전송받는 B 서버에는 SerialDTO라는 클래스가 있어야 한다.<br>
그런데 만약 A 서버가 갖고 있는 SerialDTO에는 변수가 3개 있고, B 서버의 SerialDTO에는 변수가 4개 있는 상황이 발생하면 어떻게 될까. 이러한 겨우 자바에서는 제대로 처리를 못하게 된다.<br>
자바는 해당 객체가 같은 객체인지 serialVersionUID를 통해 구분할 수 있다. 클래스 이름이 같더라도 이 ID가 다르면 다른 클래스라고 인식한다.<br>
또한 같은 UID라고 할지라도, 변수의 개수나 타입 등이 다르면 이 경우도 다른 클래스로 인식합니다.

## serialVersionUID
![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/2d33f220-c9bf-4771-a030-67df8b0d292e)
- HashMap 클래스를 보면 serialVersionUID 변수를 확인할 수 있다. Serializable 인터페이스를 상속 받은 후 위와 같이 serialVersionUID 변수 값을 지정해주는 것을 권장한다. 별도로 지정하지 않으면 컴파일될 때 자동으로 생성된다.
- static final long으로 선언해야 하며 변수명도 serialVersionUID로 선언해야 한다.
- 아무 값이나 지정해도 상관없다. 값의 의미는 해당 객체의 버전을 명시한다.

### 예외
- serialVersionUID의 정보가 일치하지 않을 경우 java.io.InvalidClassException 에외가 발생한다.
  - 역직렬화 할 시 직렬화된 데이터 타입과 다를 경우
- 직렬화된 자바 데이터에 존재하는 멤버 변수가 없거나 추가될 경우에는 예외가 발생하지 않고 값이 없어진다.
<br>

# transient
- Serialize하는 과정에서 제외하고 싶은 경우 선언하는 키워드
- 패스워드나 보안정보 등 직렬화 과정에서 제외하고 싶은 경우 적용한다.

```
import java.io.Serializable;

public class Member implements Serializable {

    private String name;
    private String email;
    private transient int age;

    public Member(String name, String email, int age) {
        this.name = name;
        this.email = email;
        this.age = age;
    }

    @Override
    public String toString() {
        return String.format("Member{name='%s', email='%s', age='%s',", name, email, age);
    }
}
```
- 필드는 유지되지만 null값이 대입된다.


<br>
<br>
<br>
[참고](https://techblog.woowahan.com/2551/)<br>
[참고](https://devlog-wjdrbs96.tistory.com/268)
