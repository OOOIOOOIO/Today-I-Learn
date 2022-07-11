# 목차

- ## HTTP 개념
- ## HTTP 작동방식
- ## HTTP 속성
- ## HTTP 헤더
- ## HTTP Request
- ## HTTP Method
- ## HTTP Response
- ## HTTP Error
- 


# HTTP(HyperText Transfer Protocol)

<br>

<img src="https://mdn.mozillademos.org/files/13673/HTTP%20&%20layers.png" style="width:700px; "/>

<br>

- &nbsp;초기에는 HTML과 같은 하이퍼미디어 문서를 주로 전송했지만, 최근에는 Plain text, JSON, XML 등 다양한 형태의 정보도 전송하는 애플리케이션 레이어 프로토콜이다.

- &nbsp;일반적으로 안정적인 TCP/IP 레이어를 기반으로 사용하는 응용 프로토콜이다.

- &nbsp;HTTP는 클라이언트가 요청을 생성하기 위한 연결을 연 후 응답을 받을 때까지 대기하는 전통적인 클라이언트-서버 모델을 따른다.

- &nbsp;HTTP는 무상태 프로토콜이며, 이는 서버가 자원을 절약하기 위해 모든 사용자의 요청마다 연결과 해제의 과정을 거치기 때문에 어떠한 상태나 데이터를 유지하지 않음을 의미한다.

<br>
<hr>
<br>

# HTTP 작동 방식

#### &nbsp;클라이언트가 어떠한 요청(서비스)를 URI를 통해 서버에 요청(Request)을 하게 되면 서버에서는 해당 요청에 대한 결과를 응답(Response)하는 형태로 작동한다.

- 클라이언트
   - 서버에게 요청을 보내는 리소스 사용자 
   - ex) 웹 브라우저, 모바일 애플리케이션, IOT, ...

- 서버
   - 클라이언트가 보낸 요청에 대한 응답을 제공하는 리소스 관리자

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdcUnst%2FbtqWXaFbg2p%2F86WwcX7OsOvnkoO71T0RbK%2Fimg.png" width=800px height=600px>

<br>
<hr>
<br>

## HTTP 속성

### Idempotent : 멱등성
- 여러번 수행해 같은 결과를 도출한다는 뜻. 호출로 인해 데이터의 변형이 없다는 뜻이다. 
- GET : 한 번 조회하든, 두 번 조회하든 같은 결과가 조회된다.
- PUT : 기존 것을 날리고 새로운 데이터를 덮어 씌우기 때문에 같은 요청을 여러번 해도 최종 결과는 같다.
- DELETE : 같은 요청을 여러번 해도 삭제된 결과는 똑같다.
- POST : 멱등이 아니다!!!! 두 번 호출하면 같은 결제가 중복해서 발생할 수 있다! 
- 자동 복구 메커니즘 등에서 사용하며, 중간에 리소스를 변경할 경우 멱등하지 않으며 멱등은 그것까지 고려하지 않는다.

<br>

### 안전(Safe)
- 호출해도 리소스를 변경하지 않는다.(GET, HEAD)

<br>

### Cacheable(캐시가능)
   - 응답 결과 리소스를 캐시해서 사용해도 되는가?
   - GET, HEAD, POST, PATCH 캐시 가능하다.
   - 실제 GET, HEAD 정도만 캐시로 사용한다.
   - POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 이는 구현하기가 쉽지 않다.

<br>
<hr>
<br>

# HTTP 헤더

<br>
<hr>
<br>

# HTTP 요청(Request)

<br>

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc7mI3U%2FbtqWX45M76d%2FgGoVLK6rcUJhekrxMcq6a1%2Fimg.png">

### <code> ex) GET/search?q=hello&hl=ko HTTP/1.1</code>
- Method : 서버가 수행해야 할 동작 --> GET
- Path : 절대경로 "/"로 시작하는 경로이다. --> /search?q=hello&hl=ko
- Version of the Protocol : HTTP의 버전
- header에서 한 줄 띄고 "본문"이라는 것이 적혀 있는데, 본문엔 요청을 할 떄 같이 보낼 데이터가 담겨져있다.

<br>


## HTTP 메서드(Method) : 서버가 수행해야 할 동작 과정

<br>

![](https://user-images.githubusercontent.com/4013025/48322141-cf7af680-e604-11e8-8a76-ae4d92a83793.png)

<br>

![](https://static.packt-cdn.com/products/9781838983994/graphics/image/C15309_01_02.jpg)

<br>


### 일반적으로 웹에서 REST API를 작성할 때 HTTP Methods를 이용해 CRUD를 표현한다. REST API, REST 방식은 따로 정리하겠다.

<br>

## [REST 방식 정리 보러가기](https://github.com/OOOIOOOIO/Study_Web_development/blob/master/Network/REST.md)

<br>

## 종류

- ### GET
   - 주로 데이터를 읽거나(Read) 검색(Retrieve)할 때에 사용되는 메소드이다. 만약  GET 요청이 성공적으로 이루어진다면 XML이나 JSON과 함께 200 HTTP 응답 코드를 리턴한다. 에러가 발생하면 주로 404(Not found) error 혹은 400(Bad request) 에러가 발생한다.
   - HTTP 명서에 의하면 GET 요청은 오로지 데이터를 읽을 때에만 사용된다. 수정, 삭제와 같은 데이터를 조작하는 연산에 사용하면 안된다
   - GET Method는 idempotent하다
   - cache
```
ex) url

GET /polite/1998 HTTP/1.1
```

- ### POST
   - 주로 새로운 리소스를 생성(Create)할 때 사용된다. 조금 더 구체적으로 POST는 하위 리소스들을 생성하는데 사용된다. 성공적으로 Creation을 완료하면 201(Created) HTTP 응답을 반환한다.
   - Post Method는 idempotent하지 않다.
```
ex) json 형식

POST /polite HTTP/1.1
body : {"name" : "SeongHo Kim"}
Content-Type : "application/json"

```

- ### PUT
   - 변경 가능한 리소스를 업데이트하는 데 사용되며 항상 리소스의 식별 정보를 포함해야 한다.
   - 리소스가 있으면 대체, 없으면 생성한다. 중요한 점은 완전 덮어버린다는 것이다.
   - POST와 다른 점은 클라이언트가 리소스 위치를 알고 URI를 지정한다.
   - Put Method는 idempotent하다.
```
ex) json 형식

PUT /polite/1998 HTTP/1.1  or PUT /polite HTTP/1.1
body : {"name" : "SEONGHO KIM", "age" : 99}
Content-Type : "application/json" // 없어도 됨

```

- ### PATCH
   -  변경 가능한 리소스의 부분 업데이트에 사용되며 항상 리소스 식별 정보를 포함해야 한다.(잘 사용하지 않는다. PUT을 사용해 전체 객체를 업데이트하는 것이 관례라고 한다.)
   -  부분 리소스 변경
```
ex) json 형식

PUT /polite/1998 HTTP/1.1
body : {"name" : "SEONGHO KIM", }
Content-Type : "application/json" // 없어도 됨
```

- ### DELETE
   - 특정 리소스를 제거하는 데 사용한다.(일반적으로 Request body가 아닌 URI경로에 제거하려는 리소스의 ID를 전달한다.)
   - 데이터를 삭제하는 것이기 때문에 요청 시 Body와 Content-Type이 비워져 있다.
```
ex) url

DELETE /polite/1998

```

- ### HEAD
   - 클라이언트가 본문 없이 리소스에 대한 헤더만 검색하는 경우 사용한다.(일반적으로 클라이언트가 서버에 리소스가 있는지 확인하거나 메타 데이터를 읽으려는 때만 GET 대신 사용한다.)

- ### OPTIONS
   - 클라이언트가 서버의 리소스에 대해 수행 가능한 동작을 알아보기 위해 사용한다.(일반적으로 서버는 이 리소스에 대해 사용할 수 있는 HTTP 요청 메서드를 포함하는 Allow 헤더를 반환한다. CORS에 사용한다고 한다.)

- ### CONNECT

- ### TRACE

<br>

## 참고
- ### RFC(Request for Comment)
   - 비평을 기다리는 문서라는 의미로, 컴퓨터 네트워크 공학 등에서 인터넷 기술에 적용 가능한 새로운 연구, 혁신, 기법 등을 아우르는 메모를 나타낸다.

<br>
<hr>
<br>

# HTTP 응답(Response)
>&nbsp;마찬가지로 응답에도 본문(body)이 존재한다. 요청에 대한 데이터가 담겨있으며 브라우저는 응답 메세지에 담겨있는 HTML을 받아 화면에 렌더링을 한다.

<br>

![image](https://user-images.githubusercontent.com/74396651/178242102-9b82c923-4c80-4783-a53e-6423a35191c7.png)

<br>

## 1XX : Information responses
>&nbsp;상태코드가 "1"로 시작하는 경우는 서버가 요청을 받았으며, 서버에 연결된 클라이언트는 작업을 계속 진행하라는 의미이다. 해당 코드는 HTTP 1.0에서 지원되지 않는다.

<br>

- 100 : continue
   - 작업이 진행 중임을 나타내는 응답코드이다. 현재까지의 진행상태에 문제가 없으며, 클라이언트가 계속해서 요청을 하거나 이미 요청을 완료한 경우 무시하라는 것을 의미한다.

- 101 : Switching Protocol
   - 클라이언트에 의해 보내진 업그레이드 요청 헤더에 대한 응답으로 보내진다. 서버에서 프로토콜을 변경할 것임을 알려줌 해당 코드는 Websocket 프로토콜 전환 시에 사용된다.

- 102 : Processing(WebDAV)
   - 서버가 요청을 수신하였으며 이를 처리하고 있지만, 아직 제대로 된 응답을 알려줄 수 없음을 나타낸다.
   
<br>   
   
## 2XX : Successful responses

<br>

- 200 : OK
   - 요청이 성공적으로 되었으며 요청에 따른 응답을 해준다.
<br>

![image](https://user-images.githubusercontent.com/74396651/178243946-d5ed1b7c-f457-4d4f-9704-ea39f51cf22b.png)

<br>

- 201 : Created
   - 요청이 성공적으로 되었으며, 그 결과로 새로운 리소스가 생성되었다는 뜻이다. 일반적으로 POST or PUT 메소드 이후에 따라온다.

<br>

![image](https://user-images.githubusercontent.com/74396651/178243895-96991ddc-9a2c-489a-a49a-0f443dd5c86d.png)

<br>

- 202 : Accepted
   - 요청이 접수되었으나 처리가 완료되지 않았다는 뜻.
   - 배치 처리 같은 곳에서 사용한다.(요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리한다.)
   
- 203 : Non-Authoritative Information

- 204 : No Content
   - 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없다.
   - save 버튼을 눌러도 같은 화면을 유지한다.(웹 문서의 편집기에서 save 버튼)

- 205 : Reset Content

- 206 : Partial Content

- 207 : Multi-Status

- 208 : Already Reported

- 226 : IM Used

<br>

## 3XX : Redirection messages 
> 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동한다.<br>
> <code>대부분의 애플리케이션에서 302를 기본값으로 사용한다.</code>

<br>

![image](https://user-images.githubusercontent.com/74396651/178244028-f5d19fe2-2688-4bb3-8dd4-ee5e52a58f11.png)

<br>

### Redirection의 종류
- 영구 리다이렉션 : 특정 리소스의 URI가 영구적으로 이동하였을 경우
   - 301, 308 
   - 예시) /members -> /users
   - 예시) /event -> /newEvent

<br>

- 일시 리다이렉션 : 일시적인 변경
   - 302, 307, 303 
   - 예시) 주문 완료 후 주문 내역 화면으로 이등
   - PRG : POST / Redirection / GET 으로의 흐름. 새로고침해도 다시 주문이 안되고 결과 화면만 조회

![image](https://user-images.githubusercontent.com/74396651/178251156-c03c18be-8129-4e0a-9bab-7b7185c22b03.png)

<br>

### RPG 사용 전
![image](https://user-images.githubusercontent.com/74396651/178251176-aa87818f-0115-43d7-8aca-07283ddd6088.png)

<br>

### RPG 사용 후
![image](https://user-images.githubusercontent.com/74396651/178251204-34d69d2d-782a-4190-a727-7742eaeab668.png)

<br>

- 특수 리다이렉션 
   - 300, 304
   - 결과 대신 캐시를 사용

<br>

- 300 : Multiple Choices
   - 안쓴다.

- 301 : Moved Permanently
   - Redirect시 요청 메서드가 GET으로 변하고 본문이 제거될 수도 있다.(MAY)

![image](https://user-images.githubusercontent.com/74396651/178250778-dc057dee-c4d6-4bb2-b91f-bb2b24b0fbd2.png)


- 302 : Found
   -  Redirect시 요청 메서드가 GET으로 변하고 본문이 제거될 수도 있다(MAY) / 대부분의 애플리케이션에서 302를 기본값으로 사용한다.

- 303 : See Other
   - Redirect시 요청 메서드가 GET으로 변경된다.

- 304 : Not Modified
   - 캐시를 목적으로 사용한다.
   - 클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 클라이언트는 로컬PC에 저장된 캐시를 재사용한다.(캐시로 리다이렉트함)
   - 304 응답은 응답에 메시지 바디를 포함하면 안된다.(로컬 캐시를 사용해야 하므로)
   - 조건부 GET, HEAD 요청시 사용한다.


- 307 : Temporary Redirect
   - Redirect시 요청 메서드와 본문 유지(요청 메서드를 변경하면 안된다. MUST NOT)


- 308 : Permanent Redirect
   - Redirect시 요청 메서드와 본문 유지(처음 POST로 보내면 Redirect도 POST 유지)

<br>

![image](https://user-images.githubusercontent.com/74396651/178250799-359610c6-728b-45cc-ba73-9c79493ef72b.png)

<br>

### 4XX : Client error responses
> 클라이언트 오류<br>

- 클라이언트의 요청에 잘못된 문법 등으로 서버가 요청을 수행할 수 없을 때
- 오류의 원인이 클라이언트에 있다.
- 클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에 똑같은 시도를 할 경우 무조건 실패한다!(5xx 오류와 다른 점)

<br>

- 400 : Bad Request
   - 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없는 경우
   - 요청, 구문, 메시지 등등 오류
   - 클라이언트는 요청 내용을 다시 검토하고 보내야한다.
   - 예시) 요청 파라미터가 잘못 되거나 API 스펙이 맞지 않을 경우

- 401 : Unauthorized
   - 클라이언트가 해당 리소스에 대한 인증이 필요한 경우
   - 인증(Authentication) 되지 않았다는 뜻
   - 401 오류 발생시 응답에 WWW-Authenticate 헤더와 함께 인증 방법을 설명한다.
   - 참고
      - 인증(Authentication) : 본인이 누구인지 확인(로그인)
      - 인가(Authorization) : 권한부여(ADMIN 권한처럼 특정 리소스에 접근할 수 있는 권한, 인증이 있어야 인가가 있다)
      - 오류 메세지가 Unauthorized지만 인증 되지 않았다는 뜻이다.

- 403 : Forbidden
   - 서버가 요청을 이해했지만 승인을 거부한 경우
   - 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
   - 예시) Admin 등급이 아닌 사용자가 로그인인 했지만 Admin 등급의 리소스에 접근하는 경우

- 404 : Not Found
   - 요청 리소스를 찾을 수 없는 경우
   - 오청 리소스가 서버에 없다.
   - 또는 클라이언트가 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을 때 사용한다.

<br>

### 5XX : Server error responses
> 서버 오류<br>

- 서버 문제로 오류 발생
- 서버에 문제가 있기 때문에 재시도 하면 성공할 수도 있다.(복구가 되거나 ... 4xx과 다른 점)

<br>

- 500 : Internal Server Error
   - 서버 문제로 오류 발생, 애매하면 500 오류

- 503 : Service Unavailable
   - 서비스 이용 불가
   - 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없다.
   - Retry-After 헤더 필드로 얼마 뒤에 복구되는지 보낼 수도 있다.






