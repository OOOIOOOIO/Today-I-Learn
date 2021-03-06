# MIME 유형이란
> &nbsp;&nbsp;MIME(Multipurpose Internet Mail Extensions)는 다목적 인터넷 메일 확장이라는 뜻이다.
> MIME 유형은 데이터 유형을 식별하는데 사용되는 레이블이며 인터넷 미디어 유형(Content-type)과 동일하다.
> 오늘날 MIME는 다른 많은 프로토콜에서 사용되므로, 새로운 명명 규칙인 "인터넷 미디어 유형"이라고 사용된다.

<br>
<hr>
<br>

# MIME 유형의 역할
- 인터넷에서 파일 유형을 분류하는 표준 방식을 형성한다.
- 소프트웨어가 데이터를 처리하는 방법을 알 수 있게 한다.
- 웹 서버 및 브라우저와 같은 인터넷 프로그램에는 모두 MIME 유형 목록이 있다. 따라서 작업중인 운영 체제에 관계 없이 동일한 유형의 파일을 동일한 방식으로 전송할 수 있다.

<br>
<hr>
<br>

# MIME 유형의 작동 방식

![image](https://user-images.githubusercontent.com/74396651/170238473-ca650449-e61f-4a8b-882f-9a60c565c82f.png)


- 서버는 HTTP 응답 헤더에 MIME 유형을 삽입한다.
- 클라이언트는 응답이 나타내는 데이터 유형에 적합한 "플레이어" 애플리케이션을 선택한다.
- 이러한 플레이어 중 일부는 웹 클라이언트 또는 브라우저에 내장되어 있다.

<br>


### 예시
> &nbsp;&nbsp;브라우저는 HTTP응답에 정의된 헤더의 Content-Type 값을 사용하여 적절한 확장자, 플러그인으로 파일을 열 수 있다.
> 이러한 플레이어 중 일부는 브라우저에 내장되어 있다.(브라우저는 GIF, JPEG 이미지 플레이어와 HTML 파일 처리 기능을 가지고 있다.)<br>
> &nbsp;&nbsp; 브라우저는 파일 확장자가 아닌 MIME 유형을 사용하여 URL을 처리하는 방법을 결정한다.
> 그러므로 웹 서버가 응답 헤더의 Content-Type에 올바른 MIME 유형을 전송하는 것이 중요하다. Content-Type이 올바르게
> 구성되어 있지 않으면 브라우저가 파일의 내용을 잘못 해석하고 사이트가 제대로 작동하지 않으며, 다운로드한 파일이 잘못 처리 될 수 있다. 

<br>
<hr>
<br>

# MIME 유형의 구성

![image](https://user-images.githubusercontent.com/74396651/170237715-0b5c4b0e-09fc-4dc1-8ea7-61d50c8502eb.png)


- 유형과 하위 유형의 두 부분으로 구성되고 "/(슬래쉬)"로 구분된다.
- 예를 들어 Ajax를 통해 서버와 통신할 때 contentType : "application/json" 을 살펴보면
   - 유형 : "application"
   - 하위 유형 : "json"
   - 전체 MIME 유형 : "application/json"이다. 
- MIME 유형의 전체 목록이 있지만 파일과 관련된 확장자나 파일 유형에 대한 설명은 나열하지 않는다.
- 즉 특정 종류의 파일에 대한 MIME 유형을 찾으려면 어려울 수 있으므로 MIME 유형의 목록을 살펴보고 추측할 줄 알아야 한다.





> 참조 
> https://dololak.tistory.com/130<br>
> https://hanamon.kr/%eb%84%a4%ed%8a%b8%ec%9b%8c%ed%81%ac-mime-%ec%9c%a0%ed%98%95%ec%9d%b4%eb%9e%80/
