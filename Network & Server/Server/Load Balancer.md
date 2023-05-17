# Load Balancer란
여러 서버를 증설하는 Scale-out 방식을 채택할 경우 각 Server에 균등하게 Traffic을 분산시켜주는 역할을 하는 것이 바로 Load Balaceer이다.

## Load Balancing이란
- 하나의 인터넷 서비스에서 발생하는 트랙픽이 많을 때 여러 대의 서버 분산처리를 통해 서버의 로드율 증가, 부하량, 속도저하 등을 고려하여 적절히 분산처리하여 해결해주는 서비스이다.
- 비용절감, 무중단 서비스 제공 등 장점이 있다.

## 주요기능
- NAT(Network Address Translation)
  - 사설 IP주소를 공인 iP주소로 바꾸는 데 사용하는 통신망의 주소 변조기
- Tunneling
  - 인터넷상에서 눈에 보이지 않는 통로를 만들어 통신할 수 있게 해주는 개념
  - 데이터를 캡슐화하여 연결된 상호 간에만 캡슐화된 패킷을 구별해 캡슐화를 해제할 수 있다.
- DSR(Dynamic Soorce Routing protocol)
  - 로드 밸런서 사용 시 서버에서 클라이언트로 되돌아가는 경우 목적지 주소를 스위치의 IP 주소가 아닌 클라이언트의 IP 주소로 전달해 네트워크 스위치를 거치지 않고 바로 클라이언트를 찾아가는 개념

## 구조

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/3be563b1-f3c5-4243-b6ef-7a97e3701e29)

## Load Balancing 종류
- L2
  - mac주소를 바탕으로 Load Balancing 
- L3
  - IP주소를 바탕으로 Load Balancing
- L4
  - Transport Layer(IP, Port) Level에서 Load Balancing
  - TCP, UDP
![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/7ab8be22-8abb-4e3e-8b94-99e4a794181f)

- L7
  - Application Layer(사용자의 Request) Level에서 Load Balacing
  - HTTP, HTTPS, FTP
![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/68ac3448-3f00-4c05-af17-25bbc39f588c)

- HTTP
![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/5a301532-ab52-4382-b15f-94d8c929f506)

  - X-Forwarded-For
    - HTTP 또는 HTTPS 로드 밸런서를 사용할 때 클라이언트의 IP 주소를 식별하는 데 도움을 줍니다.
  - X-Forwarded-Proto
    - 클라이언트가 로드 밸런서 연결에 사용한 프로토콜(HTTP 또는 HTTPS)을 식별하는 데 도움을 줍니다.
  - X-Forwarded-Port
    - 클라이언트가 로드 밸런서 연결에 사용한 포트를 식별하는 데 도움을 줍니다. 

## Load Balancer가 분산하는 기준
- Round Robin
  - 단순히 Round Robin으로 분산하는 방식입니다.
- Least Connections
  - 연결 개수가 가장 적은 서버를 선택하는 방식입니다.
  - 트래픽으로 인해 세션이 길어지는 경우 권장하는 방식입니다.
- Source
  - 사용자의 IP를 Hashing하여 분배하는 방식입니다.
  - 사용자는 항상 같은 서버로 연결되는 것을 보장합니다.

## 장애 발생 시

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/112cee94-4208-45a0-8247-8f9c74b37ce8)

- Load Balancer를 이중화하여 장애를 대비할 수 있다.
- 이중화된 Load Balancer들은 서로 Health Check를 한다.
- Main Load Balancer가 작동하지 않으면 가상 IP(VIP)는 여분의 Balancer로 변경된다. 
- 이후 여분의 Load Balancer로 운영하게 된다.

<hr>

## AWS에서 Load Balancing 둘러보기

## Target Group
- 타겟그룹이란 EC2 인스턴스를 오토스 케일링할 수 있는 단위로 사용된다.
- 각각의 타겟그룹에 있는 인스턴스들은 정의된 health Check(상태 확인)를 수행할 수 있게 된다.

## Auth Scailing
- 오토 스케일링은 미리 정의한 용량 정책에 따라 EC2 인스턴스의 용량을 확대하거나 축소할 수 있다.
- EC2와 오토 스케일링을 결합해 고가용성 아키텍처를 구현할 수 있으며, 언제든 원하는 수만큼의 인스턴스를 운용할 수 있다.
- 서버의 과부하, 장애 등과 같이 서비스 불능 상황 발생시 자동으로 서버를 복제하여 서버 대수를 늘려주는 작업을 해주는 AWS 서비스라고 생각하면 된다.

## Health Check
- 로드밸런서에는 Health Checks를 할 수 있다. Health Checks는 타겟그룹에 원하는 경로와 포트를 설정하여 HTTP 응답이 정상적으로 오는지 확인하고, 오지 않는다면 비정상 상태의 인스턴스를 제외한 다른 인스턴스로만 트래픽을 분산한다.
  - InService (정상적으로 응답)
  - OurOfService (응답 실패)

## ELB(Elastic Load Balancer)
![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/e2065614-7c78-4a37-953d-5e026b6d7a94)
- ELB의 경우 네트워크 레이어 4와 네트워크 레이어7에 대한 부하를 제어할 수 있다.
- 서버의 기본주소가 바뀌면 로드밸런서를 새로 생성해야하며 하나의 주소에 하나의 타겟그룹으로 보내게 된다. 따라서 타겟그룹이 많아질수록 더 많은 수의 로드밸런서가 필요하고 비용도 그만큼 더 들아가게 된다.


## ALB(Application Load Balancer)
![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/cff8dc7a-99c7-4fa8-abd0-b2177d261936)
- ALB의 경우는 네트워크 레이어7의 프로토콜에 대한 부하만 처리할 수 있다. 
- ELB와 다르게 경로나 포트등에 따라 다른 타겟그룹으로 맵핑할 수 있다. 포트 단위로 연결해줄 수 있기 떄문에 도커에서 유용하게 작동할 수 있고 하나의 대상그룹에 더 많은 컨테이너를 넣을 수 있어 비용을 최적화할 수 있다.
- EC2 인스턴스, AWS 람다, IP로도 연결이 가능하고 특정한 요청에 대해서는 서버 없이 응답메세지를 작성할 수 있다. 
- ALB에는 리스너를 포트와 프로토콜별로 분기처리할 수 있습니다. 하단에 있는 룰은 패스별 혹은 AWS_ARN별로 다른 분기를 처리할 수 있다.
- 하지만 ALB는 IP가 끊임없이 변화하기 때문에 ALB의 Public IP를 목적지로 삼아 접근 제어(ACL)를 실시하는 네트워크 장비에겐 매우 난감할 수도 있다.

 ## NLB(Network Load Balancer)
 ![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/58c69fe2-0a18-4722-a8b7-2bca686b4a9d)
- NLB는 L4 로드 밸런싱을 하는 로드 밸런서이다. L4 로드 밸런싱이기 떄문에 TCP와 UDP에 대한 트래픽을 처리할 수 있고, TLS(SSL Offload)까지 가능한 로드밸런서입니다.
- NLB는 사용자와 인스턴스간의 논리적인 연결이 생성될 수 있도록 돕는다. 
- 부하분산을 함과 동시에 사용자와 인스턴스의 커넥션을 생성하도록 돕고 자신 또한 커넥션을 가지며 관리한다. 
- 무엇보다 NLB의 가장 큰 특징은 ALB와 다르게 고정 IP를 갖는다는 것아다. Private IP뿐만 아니라 Public IP까지 고정된 IP로 제공합니다. 

## 각 기능 별 지원여부

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/45650d62-26be-414d-8b68-0f959145b4f1)


<br>
<br>
<br>
<br>
[참고](https://yoo11052.tistory.com/63)
[참고](https://nesoy.github.io/articles/2018-06/Load-Balancer)










 











