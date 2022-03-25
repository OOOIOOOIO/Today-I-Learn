# Stream(스트림)
- &nbsp;자바에서는 파일이나 콘솔의 입출력을 직접 다루지 않고, 스트림(Stream)이라는 흐름을 통해 다룬다.<br>
&nbsp;스트림(Stream)이란 실제의 입력이나 출력이 표현된 데이터의 이상화된 흐름을 의미한다.<br>
&nbsp;즉, 스트림은 운영체제에 의해 생성되는 가상의 연결 고리를 의미하며, 중간 매개자 역할을 한다.

<br>

![](http://www.tcpschool.com/lectures/img_c_stream.png)

<br>

# 입출력 스트림
- 스트림은 한 방향으로만 통신할 수 있으므로, 입력과 출력을 동시에 처리할 수는 없다. 따라서 사용 목적에 따라 입력 스트림과 출력 스트림으로 구분된다.
- 자바에서는 java.io 패키지를 통해 InputStream과 OutputStream 클래스를 별도로 제공하고 있다. 즉, 자바에서 스트림 생성이란 이런한 스트림 클래스 타입의 인스턴스를 생성한다는 뜻이다.
- InputStream에는 read()를 이용해, OutputStream에는 write()를 이용해 해당 입출력 스트림으로부터 바이트를 읽어오고 저장한다.
- InputStream과 OutputStream은 기본적으로 바이트 스트림이다.

<br>

# 종류

<br>

## InputStream과 OutputStream

![image](https://user-images.githubusercontent.com/74396651/160087992-d6f0e696-a97e-4c7e-a7c8-b5c093e061aa.png)

<br>

## 바이트 기반 스트림

![image](https://user-images.githubusercontent.com/74396651/160088272-1ab99714-15a6-4e8a-8b24-9f1417cf7631.png)

<br>

## 바이트 보조 스트림

![image](https://user-images.githubusercontent.com/74396651/160088347-9711a74c-8315-4576-9181-f111e3e1b477.png)

<br>

## 문자 기반 스트림

![image](https://user-images.githubusercontent.com/74396651/160088407-b127edca-a4ef-4a01-bd6a-5b9ce90184d0.png)

<br>

## 문자 보조 스트림

![image](https://user-images.githubusercontent.com/74396651/160088541-378d8a1d-a271-4ded-a2c4-a166a9b92e06.png)

참고 및 사진 출처 : http://www.tcpschool.com/java/java_io_stream

<br>

<hr>

<br>

# 입력에 대해 이해한 것

![출처 : 점프 투 자바](https://user-images.githubusercontent.com/74396651/160093667-630adc0e-b4b2-40aa-8869-42769c028650.png)

- 스트림이란 한 곳에서 다른 곳으로의 데이터 흐름이라고 생각할 수 있다.
- 자바에서 가장 기본이 되는 입력 스트림은 InputStream 이다. 반대초 출력 스트림은 OutputStream 이다.

<br>

## Java의 인코딩
- 자바는 내부적으로(메모리 상에서) 문자열이 UTF-16으로 인코딩 되어 처리된다.
- 문자열 송/수신을 하기 위해 직렬화가 필요할 때에는 변형된 UTF-8을 사용한다.
- 문자열을 입출력할 때는 운영체제 기본 인코딩 값 또는 사용자가 지정한 인코딩 값으로 문자열을 인코딩한다.(내부 메모리 상에서 처리하는 것과는 다르다.)
- 1 ~ 127까지는 Ascii 코드 값과 유니코드(UTF-8, 16, ...), MS계열(MS949, CP949, ...)의 값이 같다. (ms랑 유니코드는 해당 범위에서 92번만 다른데 이는 역슬래쉬로 인해 발생한 문제이다. 
윈도우에서는 원화 표시로 표현되고 맥, 리눅스 계옐에서는 역슬래쉬(\)로 표현된다.

<br>
  
### 흐름

> &nbsp;만약 이클립스의 File encoding이 UTF-8이라면<br><br>
> &nbsp;입력(UTF-8) -> 송수신(modified UTF-8) -> 자바 메모리 (UTF-16) -> 송수신(modified UTF-8) -> 출력(UTF-8)<br><br>
> 처럼 흘러가게 된다.<br><br>
> &nbsp;즉, 운영체제 혹인 시스템에 설정되어 있는 인코딩 형식으로 입력받으면 UTF-16의 인코딩 규칙으로 인해 UTF-16으로 인코딩 되어 메모리에 올라가고
> 출력하게 될 경우 메모리에 UTF-16으로 저장되어 있는 값을 다시 운영체제 혹은 시스템에서 설정한 인코딩 형식으로 대응되는 문자를 출력하게 된다.

<br>

<hr>

<br>

## InputStream 과 System.in

![image](https://user-images.githubusercontent.com/74396651/160094177-ee7e1002-f014-4b48-abfe-a8517967c481.png)

- 위 사진에서 볼 수 있듯이 System 클래스의 in이라는 필드는 InputStream의 정적 필드이다. in 이라는 변수는 InputStream의 변수로 결국 InputStream 타입의 새 변수를 선언하고
그 변수에 System.in을 할당시킬 수 있다는 뜻이다.

<br>

![image](https://user-images.githubusercontent.com/74396651/160094639-871b27b1-2034-4d2d-a09c-de5ff7d416f9.png)

- InputStream 타입의 변수를 생성하고 입력을 받는 메소드인 read()를 통해 입력을 할 수 있다.
- InputStream은 입력 받는 데이터를 int형으로 저장하는데 이는 메모리에 UTF-16 10진수로 저장된다.
- InputStream은 1 byte만 읽는다.
- 입력 받은 문자가 2 byte 이상으로 구성되어 있는 인코딩을 사용할 경우 1 byte 값만 읽어들이고 나머지는 읽지 않고 스트림에만 남아있기 때문에 
출력할 대는 해당 데이터의 1 byte에 대한 인코딩 값을 10진수로 변환해 출력한다. 이러한 바이트 단위로 주고 받는 스트림을 "바이트 스트림" 이라고 한다.

<br>

<hr>

<br>

## Scanner(System.in)과 InputStreamReader()

<br>

### Scanner(System.in)

![image](https://user-images.githubusercontent.com/74396651/160096020-342fa58f-14f7-42be-8a96-667ae741f28a.png)

- 평소 사용하는 Scanner 클래스는 다음과 같이 풀어서 쓸 수 있다.

<br>

![image](https://user-images.githubusercontent.com/74396651/160096651-2dd493d4-c40d-42e5-8832-546941980dd7.png)

- Scanner 클래스 안에는 이렇게 오버로딩 되어있는데, 여기서 InputStreamReader가 나온다.

<br>

### InputStreamReader()

![image](https://user-images.githubusercontent.com/74396651/160096875-dbaad1dc-dda5-4e44-b1c6-b4abed9dd12a.png)

- InputStreamReader란 바이트 스트림에서 캐릭터 스트림으로 변환시키는 다리같은 역할이다. 즉, InputStream의 바이트 단위로 읽어 들이는 형식을 문자(Charater) 단위로 변환시키는
중간 다리라고 보면 된다. 이 때문에 Scanner를 사용해 입출력을 할 때 문자가 깨지지 않는 이유는 내부에서 InputStreamReader가 온전한 문자형태로 변환 및 처리해주기 때문이다.
이러한 문자 단위로 주고 받는 스트림을 "캐릭터 스트림" 이라고 한다.

<br>

![image](https://user-images.githubusercontent.com/74396651/160098244-73e9568d-002c-4c66-84d9-0fe9379721e5.png)

- 따라서 이렇게 쓸 수 있다는 뜻이다. 여러개를 받고 싶으면 char[]를 이용해야한다.

<br>

### 정리하자면
- InputStreamReader는 바이트 단위 데이터를 문자(charater) 단위 데이터로 처리할 수 있도록 변환해준다.
- InputStreamReader는 char 배열로 데이터를 받을 수 있다.

<br>

<hr>

<br>

## BufferedReader()

![image](https://user-images.githubusercontent.com/74396651/160099648-f00d0c64-23d4-4ed2-8811-1326857c19de.png)

- 지금까지 공부한 InputStream과 System.in 그리고 InputSreamReader를 이용해 이렇게 BufferedReader를 만들 수 있다.
- 이를 통해 기본적으로 바이트 스트림인 InputStream(System.in)을 통해 바이트 단위로 데이터를 입력 받는다.
- 입력 데이터는 char 형태로 처리하기 위해 중개자 역할인 InputStream Reader로 감싸준다.

<br>

## BuffredReader가 필요한 이유
- 앞서 Scanner 에서 InputStreamReader 을 설명할 때 '문자'를 처리한다고 했다. '문자열'이 아니다. (그래서 Scanner 에서도 내부에서 임시 배열을 두어 문자열처럼 사용하고 있다.)
- 만약 문자열을 입력하고 싶다면 매번 배열을 선언해야 한다는 단점은 그대로 남아있다. 심지어 입력받을 문자열의 길이가 가변적이라면 더욱 불편하다.
- 그래서 쓰는 것이 Buffer(버퍼)를 통해 입력받은 문자를 쌓아둔 뒤 한 번에 문자열처럼 보내버리는 것이다.
- BufferedReader 를 쓸 때 우리는 입력 메소드로 readLine() 을 많이 쓴다. 이 메소드는 한 줄 전체를(공백 포함) 읽기 때문에 char 배열을 하나하나 생성할 필요 없이 String 으로 리턴하여 바로 받을 수 있다는 장점이 있다.

<br>
  
## 특징

![image](https://user-images.githubusercontent.com/74396651/160103167-494c9654-82be-4366-8cff-bdd1f4c967e0.png)

- System.in = InputStream  -> InputStreamReader -> BufferedReader
   - byte 타입으로 읽어들이는 in을 char 타입으로 처리한 뒤 String, 즉 문자열로 저장할 수 있게 한다는 의미로 해석할 수 있다.
- 버퍼가 있는 스트림이다.
- Scanner와 달리 별다른 정규식을 검사하지 않는다.
- 따로 설정하지 않으면 디폴트로 8192개의 문자를 저장할 수 있다.

<br>

# 총 정리

![image](https://user-images.githubusercontent.com/74396651/160103500-f5d473f3-03ef-43dc-81b6-16ad395e6a13.png)


1. InputStream 은 바이트 단위로 데이터를 처리한다. 또한 System.in 의 타입도 InputStream 이다.<br>
2. InputStreamReader 은 문자(character) 단위로 데이터를 처리할 수 있도록 돕는다. InputStream 의 데이터를 문자로 변환하는 중개 역할을 한다.<br>
3. BufferedReader 은 스트림에 버퍼를 두어 문자를 버퍼에 일정 정도 저장해둔 뒤 한 번에 보낸다.


<br>

# Scanner 보다 BufferedReader가 빠른 이유
- Scanner 내부에선 정규식을 이용해 입력 받은 문자를 검사하고 막 변환에 변환을 한다. 하지만 BufferedReader는 

<br>

출처 : https://st-lab.tistory.com/41









