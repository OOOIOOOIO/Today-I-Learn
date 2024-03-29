# PORT


## 개념
- 운영체제 통신의 종단점이다. 이 용어는 하드웨어 장치에도 사용되지만
- 소프트웨어에서는 네트워크 서비스나 특정 프로세스르 식별하는 논리 단위이다.
- URI 문법에 의해서 사용 및 표기할 수 있으며, IP 주소와 함께 표기하는 예는 다음과 같다.
   - ftp://000.000.000.000:21 --> 000~은 IP 주소를 나타내며 : 다음 21이 포트 번호이다.

<hr>

## PORT의 사용
- 컴퓨터에서 port란 외부의 다른 장비와 접속하기 위한 플러그와 같다고 생각할 수 있다.
- 컴퓨터나 노트북의 뒷면이나 옆면을 보면 네트워크, 마우스, 키보드 등을 연결하기 위한 포트들을 확인할 수 있다.
- 우리가 웹 브라우저를 이용하여 인터넷상에 있는 서버에 접속할 때 컴퓨터에 있는 웹 브라우저 프로그램과 서버에 있는 웹 서버 프로그램을 연결해주는 플러그 같은 역할을 하는 것이 포트이다.
- 특정 서버에 접속하려면 URL이나 IP 주소를 입력한다. 그러면 인터넷상에서 URL 또는 IP를 토대로 해당 서버가 있는 컴퓨터로 찾아간다.
그런데 대부분의 컴퓨터에서는 여러 개의 프로그림이 동시에 실행되고 있어, 내가 접속하려는 프로그램이 어떤 프로그램인지 컴퓨터에게 알려줘야 한다.
이때 사용되는 것이 바로 포트 번호이다.
   - IP address : 컴퓨터를 찾을 때 필요한 주소를 나타낸다.
   - PORT : 컴퓨터 안에서 프로그램을 찾을 때 사용된다.

<hr>

## Well-known PORT
- 0 ~ 1023 : Well-known port, 잘 알려진 포트(특정 쓰임새를 위해서 할당한 TCP, UDP 포트 번호로 이루어져 있다.)
- 1024 ~ 49151 : registered port, 등록된 포트
- 49152 ~ 65535 : dynamic port, 동적 포트

### Well-known PORT
![image](https://user-images.githubusercontent.com/74396651/198956404-f5e01a40-0b76-401d-a807-ae5023d7b653.png)

<hr>

## 포트 = 논리적인 접속 장소
- 인터넷 프로토콜인 TCP/IP를 사용할 때 클라이언트가 네트워크 상의 특정 서버 프로그램을 지정하여 사용합니다.
- 웹 브라우저(클라이언트)의 주소창에 접속하려는 도메인 주소(www.example.com)를 입력하고 엔터를 치면 이동하게 됩니다.
- 이때 주소창을 다시 확인해보면 내가 입력하지 않은 "http" or "https"가 도메인 주소 앞에 붙어있는 것을 확인할 수 있습니다.
- 브라우저에 도메인 주소를 입력하고 엔터를 치면 도메인에 해당하는 IP와 HTTP 프로토콜을 함께 서버에 요청합니다.
- DNS 서버는 그 도메인에 해당하는 IP(컴퓨터)를 찾고, IP에 도달하면 서버는 어떤 포트로 접속 요청을 했는지 확인합니다.
- HTML 문서를 주고받기 위한 규약이 바로 HTTP 프로토콜이며, 80번 포트입니다. 80번 포트로 접속이 되면 비로소 서버는 HTML 문서를 클라우드(브라우저)에 전송합니다. 

<hr>

## 흐름
> &nbsp;사용 목적에 따라 지정된 논리적 주소인 포트 번호로 연결된 두 개의 컴퓨터 사이에서 네트워크를 이용한 통신 시,
> 발신 컴퓨터에서 출발한 패킷(사용자 데이터)은 TCP/IP의 각 계층을 거치면서 최종 목적지 주소(IP)를 가지고 있는 컴퓨터에 도착합니다.
> 패킷을 수신한 컴퓨터는 패킷 안에 있는 데이터만 응용 프로그램에 전달합니다.

1. 발신 컴퓨터가 패킷을 보냄
2. DNS 서버에 의해 해당 IP주소 컴퓨터(서버)에 패킷 도착
3. 패킷 안에 있는 프로토콜과 포트 번호를 보고 데이터를 응용 프로그램에 전달
   - ex) 프로토콜이 HTTP(포트 번호 80)이라면 사용자가 웹 사이트에 접속하려고 하는구나하고 수신 컴퓨터(서버)는 해당 데이터를 웹 서버에 보낸다.

<hr>

- ### 각각의 응용 프로그램에 이미 정해져 있는 포트 번호를 이용하여, 전송 계층에서 응용프로그램을 구분하느 것이다.

![image](https://user-images.githubusercontent.com/74396651/198957476-5abd0d23-ee97-4680-a438-15d598721267.png)
