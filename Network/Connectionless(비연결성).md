# Connectionless
- Connectionless(비연결성)은 클라이언트가 서버에 요청을 하고 응답을 받으면 TCP/IP 연결을 끊어 연결을 끊어 유지하지 않는 것이다.
- 이를 통해 서버의 자원을 효율적으로 관리하고 수 많은 클라이언트의 요청에도 대응할 수 있게 된다.
- HTTP는 기본적으로 연결을 유지하지 않는 모델이다.

## 한계

![image](https://user-images.githubusercontent.com/74396651/178097183-374ba53a-2fb5-4911-bc68-df3228379ee8.png)

- 연결할 때 마다 TCP/IP 연결을 새로 맺어야 한다. -> 3 way handshake 시간이 추가된다.
- 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 JS, CSS, 추가 이미지 등 수 많은 자원이 함께 다운로드 된다.



## 극복

![image](https://user-images.githubusercontent.com/74396651/178097188-2b976a0b-41aa-47df-94e2-d1de6bce56c0.png)


- 지금은 HTTP 지속 연결(Persistent Connections)로 문제가 해결 되었다.
- HTTP/2, HTTP/3에서 더 많은 최적화를 하고 있다.
