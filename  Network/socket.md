## 소켓 
소켓이란 프로그램이 네트워크 상에서 데이터를 송신과 수신을 하기위한 연결부이다. 일반적으로 tcp/ip프로토콜을 사용하거나 웹 소켓을 이용한다

> 프로토콜    
> 어떤 시스템이 다른 시스템과 통신을 원활하게 수용하도록 해주는 통신 규약이다


### 소켓 통신의 흐름

![쏘켓](https://user-images.githubusercontent.com/64240637/133592555-52a41f5c-9e58-43a3-9b2c-92ffa326852c.png)

소켓의 흐름은 서버소켓과 클라이언트소켓으로 이야기 할 수 있다

#### 클라이언트

1. socket()함수로 소켓을 연다
2. connect() 함수를 이용해 통신 할 서버의 ip, port번호에 통신을 시도한다
3. 통신을 시도 할때 서버가 accept()함수를 사용해 클라이언트의 socket descriptor를 반환한다
4. 클라이언트와 서버가 서로 read(), writer()를 하며 통신한다(반복)

#### 서버
1. socket()함수를 이용하여 소켓을 생성한다
2. bind()함수로 ip와 port번호를 설정한다
3. listen()함수로 클라이언트의 접근 요청에 수신 대기열을 만들어서 몇 개의 클라이언트를 대기 시킬지를 결정한다
4. accept()함수를 사용하여 클라이언트와의 연결을 기다린다


소켓통신은 http통신과는 다르게 서로 연결을 유지하는 양방향 통신이다. 서버와 클라이언트가 실시간으로 데이터를 주고받는 상황이 필요한 경우에 주로 사용된다    

## 웹 소켓
웹소켓은 서버와 클라이언트간의 socket connection을 유지해 언제든 양방향 통신이나 데이터 전송이 가능하게 하는 기술이다    
즉 http통신의 한계(단방향, 재접속)를 보완하는 기술이다. 

### 웹 소켓 이전 비슷한 기술

### Polling 
서버로 일정 주기마다 요청을 송신한다   
![polliing](https://user-images.githubusercontent.com/64240637/133594391-1c7fc979-b632-4a51-90a9-0a3abae7f1ef.png)

real time통신에서는 언제 통신이 발생할지는 예측이 불가능하다. 그렇기에 불필요한 request와 connection이 발생한다.

> real time = 실시간   

### Long Polling
서버에 요청을 보내고 이벤트가 발생하여 응답을 받을 때까지 연결을 종료하지 않는다. 응답을 받으면 연결을 끊고 다시 재요청을 한다
![longpolling](https://user-images.githubusercontent.com/64240637/133594388-498189c6-6de4-482a-99b9-6db4eb994474.png)   
많은 양의 메시지가 전송 될 경우 polling과 똑같다    


### Streaming   
서버에 요청을 보내고 연결을 유지하며 데어터를 수신한다      
![스트리밍](https://user-images.githubusercontent.com/64240637/133594384-d2b2bf4b-981c-451d-b125-d83ec768a919.png)    
 클라이언트에서 서버로의 데이터 송신이 어렵다   
 
 __즉 위의 방법들은 모두 HTTP를 통해 통신하기 때문에 request, response 둘 다 header가 불필요하게 크다__   
 
 ### 웹 소켓의 핸드 쉐이크
 웹 소켓도 tcp의 핸드 쉐이크처럼 연결을 하는 과정이 존재한다. 이때 웹 소켓의 핸드 쉐이킹은 http(80)나 https(443)의 프로토콜을 통해서 이루어진다.    
![웹소켓](https://user-images.githubusercontent.com/64240637/133595432-4a2d221b-8264-4741-945a-bc4056f4dfc3.png)

 1. 클라이언트에서 아래와 같은 표준적인 http 요청 header를 보낸다 (이때 http버전은 반드시 1.1 이상이여야하며 get방식이여야 한다 )
 ```text
GET /chat HTTP/1.1 
Host: example.com:8000 # 웹 소켓의 서버 구조
Upgrade: websocket # 현재 클라이언트. 서버 전송 프로토콜 연결에서 다른 프로토콜로 업그레이드/변경하기 위한 규칙
Connection: Upgrade # upgrade헤더가 명시되어 있는 경우 송신자는 반드시 connection헤더 필드도 함께 전송해야 한다
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ== # 양쪽 통신자의 신원을 확인하는 키라고 생각하면 된다
Sec-WebSocket-Version: 13
 ```
 2. 서버가 클라이언트에게 웹소켓 프로토콜로 업그레드 하는 것을 승인하면 아래의 헤더를 전송한다
 ```text
 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: hsBlbuDTkk24srzEOTBUlZAlC2g=
 ```
 
 핸드 쉐이킹이 완료되면 http프로토콜은 __ws__ 프로토콜로 변경된다 (wss -> https처럼 데이터 보안을 위해서 ssl을 적용한 프로토콜)
 이후 서로 messge를 주고받는다 (message : 여러 프레임이 모여 구성하는 하나의 논리적 메시지 단위)
 
 > 프레임(frame)   
 커뮤니케이션에서 가장 작은 단위의 데이터이다 (작은헤더 + payload로 구성)
 
> 페이로드(payload)   
데이터와 함께 전송되는 데이터중, 헤더와 메타데이터와 같은 데이터는 제외한 전송의 근본적인 목적이 되는 데이터의 일부분이다   

### 웹 소켓 프로토콜 특징
- 최초 접속할때 http 프로토콜 위에서 핸드쉐이킹을 하기 때문에 http header를 사용한다
- 웹 소켓을 위한 별도의 포트는 없으며 기존포트(80, 443)를 사용한다
- 프레임으로 구성된 메시지라는 논리적 단위로 송수신된다
- 메시지에 포함될 수 있는 교환 가능한 메시지는 텍스트와 바이너리이다  

## socket.io
socket.io란 WebSocket과 같이 클라이언트와 서버의 양방향 통신을 가능하게 해주는 모듈이다. WebSocket은 HTML5이후에 나왔기 때문에 엊ㄴ의 기술로 구현된 서비스에서 WebSocket처럼 사용할 수 있도록 도와주는 기술이다.     

socket.io는 통신을 시작할때 각 브라우저에 대해서 webSocket, streaming등등에서 가장 적절한 방법을 찾아 메시지를 보내준다. 

<br>


##### reference
 
https://duckdevelope.tistory.com/19
https://rubberduck-debug.tistory.com/123
https://velog.io/@y1andyu/WebSocket-%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC%EC%99%80-%ED%95%B4%EA%B2%B0%ED%95%98%EB%8A%94-%EB%AC%B8%EC%A0%9C
https://www.youtube.com/watch?v=MPQHvwPxDUw
