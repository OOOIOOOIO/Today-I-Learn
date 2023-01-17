# Stateless & Stateful
- Stateless와 Stateful은 클라이언트와 서버간의 네트워크 통신이 어떻게 이루어지는지에 대한 개념이다.
- 즉 네트워크 프로토콜이다.
- Stateless와 Stateful을 이해하기 위해선 세션 상태와 세션 정보에 대한 개념을 알아야 한다.
- 세션 상태
   - 클라이언트와 서버간 통신 인증이 된 상태를 의미한다.
   - 인증된 상태에서 데이터 송수신이 가능하다.

- 세션 정보
   - 한 세션 내에서 클라이언트가 서버에 전송할 데이터 정보를 의미한다.
   - 서버는 세션 유지 시간이 지나거나 클라이언트가 전송하려던 데이터를 모두 수신할 때까지 클라이언트와의 세션 상태를 유지한다.

<br>
<hr>
<br>

# Stateless
- 서버가 클라이언트의 세션 상태 및 세션 정보를 저장하지 않는 네트워크 프로토콜이다.
   - 요청에 대한 응답만 처리하는 방식이다.
   - 각 통신은 선행되거나 후속으로 따라오는 통신과 관련이 없다.
   - 클라이언트가 송신하려 했던 모든 데이터가 서버쪽에 제대로 수신되었는지 확인하지 않는다.(보내고 끝)
   
### 예시
- UDP 프로토콜
   - UDP 서버가 클라이언트의 세션 상태 및 세션 정보 없이, 요청에 대한 응답만을 수행하는 네트워크 프로토콜이다.
   - HTTP/3의 기반 프로토콜이 UDP이다.
- 온라인 검색(검색창에 질문을 입력하고 엔터키를 누르는 형식)
   - 검색창에 질문을 입력하다가 요청이 중된되어도 다시 검색하면 된다.


### 장점
- 확장성이 좋다.
   - 서버가 클라이언트의 세션 상태 및 세션 정보를 저장하지 않기 때문에 확장성이 좋다.(scale-out)

### 단점
- 서버가 세션 상태 및 세션 정보를 저장하지 않기 때문에 클라이언트 측에서 송신할 데이터의 양이 많아진다.

<br>
<hr>
<br>


# Stateful
- 세션이 종료될 때까지 클라이언트의 세션 정보를 저장하는 네트워크 프로토콜이다.
- 항상 같은 서버가 유지 되어야 한다.
- 상태 유지는 최소한만 사용해야 한다.

### 예시
- TCP 프로토콜
   - TCP는 클라이언트와 서버간 3-way-handshaking(연결 확정, 데이터 전송, 연결 종료)로 이루어져 있다.
   - 클라이언트와 서버간 연결 확정 후, 데이터를 전송하고 데이터 전송이 끝나면 연결이 종료된다.
   - HTTP/1.1, HTTP/2의 기반 프로토콜이 TCP이다.

### 장점
- 서버는 클라이언트의 세션 정보를 저장하므로 갑자기 통신이 중단되더라도 중단된 곳부터 다시 시작할 수 있다.

### 단점
- 확정성이 좋지 않다.
   - 클라이언트의 세션 정보가 새로 scale out 된 서버에 저장되어 있지 않다. -->
   - 따라서 scale out시 클라이언트의 세션 정보를 새로운 서버에 옮겨주는 등 부수적인 관리가 요구된다.


<br>
<hr>
<br>

# Stateful, Stateless 차이

<br>
<hr>

![image](https://user-images.githubusercontent.com/74396651/178096807-93310ce1-180b-43aa-b2fa-958827416b66.png)

<hr>

![image](https://user-images.githubusercontent.com/74396651/178096810-72d2b0a9-9720-4725-af08-de8cae018337.png)

<hr>

![image](https://user-images.githubusercontent.com/74396651/178096812-7a6c2ee7-78c6-432f-84bb-c6bf46fdaed6.png)

<hr>

![image](https://user-images.githubusercontent.com/74396651/178096815-9788ef04-45af-41cb-9898-fc330a4df42c.png)

<hr>

![image](https://user-images.githubusercontent.com/74396651/178096820-7af60c31-702d-4643-b7ed-06bf926cdfc0.png)

<hr>

![image](https://user-images.githubusercontent.com/74396651/178096825-388c9b52-52ef-40ef-9065-d34a589af16e.png)

<hr>

![image](https://user-images.githubusercontent.com/74396651/178096826-1deb5b79-0bb1-47eb-9545-40c353f38b8e.png)

<hr>

![image](https://user-images.githubusercontent.com/74396651/178096829-2667774b-f405-49b2-a64a-833a883ff551.png)

<hr>

![image](https://user-images.githubusercontent.com/74396651/178096831-f49fd8f9-68bf-4a66-b7b4-6d27442db2c4.png)

<hr>

![image](https://user-images.githubusercontent.com/74396651/178096834-03e742ae-c45e-456a-acf6-46681770ece8.png)

<br>
<br>
<br>

참조 : 인프런 김영한님 강의
