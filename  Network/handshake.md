## TCP/UDP 헤더

### TCP 헤더
![TCP](https://user-images.githubusercontent.com/64240637/131625126-1773b733-3985-46e6-969a-6daf373ac082.png)

source port : 출발지 포트번호    
destination port : 목적지 포트번호     
checksum : 헤더와 데이터의 에러를 확인하기 위한 필드   
flags(NS ~ FIN) : 혼잡 제어 기능의 향상을 위해 해당 플래그들이 사용된다   
ACK : 승인번호 필드에 값이 채워져 있음을 알리는 플래그, 해당 값이 0이면 승인이 무시된다 (상대방의 통신 응답을 나타낸다)  
SYN : 상대방과 연결을 생성할때 시퀀스 번호의 동기화를 맞추기 위한 세그먼트이다 (상대에 대한 접속 요청을 나타낸다)
FIN : 상대방과의 연결을 종료하고 싶다는 요청인 세그먼트이다 (접속을 종료하는 것을 나타낸다)    

<br>

### UDP 헤더

![udp-header](https://user-images.githubusercontent.com/64240637/131624293-739ceb3d-80de-447d-aeb7-22056265b38e.png)

source port : 출발지 포트번호
destination port : 목적지 포트번호
checksum : 선택항목, 헤더와 데이터의 에러를 확인하기 위한 필드

<br>

## TCP 3-Way-HandShake
TCP 3 Way-HandShake는 tcp/ip 프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 먼저 __정확한 전송을 보장하기 위해서 상대방 컴퓨터와 사전에 세션을 수립하는 과정을 말한다__     
- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장한다.    

#### TCP 3-Way-HandShake 과정
![SYN](https://user-images.githubusercontent.com/64240637/131626291-51fde236-016b-4bb1-943f-e086c5396628.png)

1. 클라이언트가 서버에 접속을 요청하기 위해 SYN패킷을 보낸다. 이때 클라이언트는 SYN/ACK응답을 기다리는 SYN_SENT상태가 된다
2. 서버는 SYN요청을 받은 뒤 클라이언트에게 요청을 수락한다는 ACK와 SYN flog가 설정된 패킷을 전송한다. 이후 ACK에 대한 응답을 기다린다. 이때 서버는 SYN_RECEIVED 상태가 된다
3. SYN+ACK를 받은 클라이언트는 서버에게 ACK를 보내고 이후 연결이 성립되어 데이터를 주고받게 된다. 이때 서버의 상태는 ESTABLISHED이다   
 
#### TCP 4-Way-HandShake 과정
TCP 3-Way-HandShake는 tcp의 연결을 초기화 할때 사용하고 TCP 4-Way-HandShake는 세션을 종료하기 위해 실행된다(즉, 통신 종료)
![4HAND](https://user-images.githubusercontent.com/64240637/131627793-aa40532c-ef27-4264-a11f-8909d69c3dfc.png)

1. 클라이언트가 연결을 종료하겠다는 FIN플래그를 서버에 보낸다
2. 서버는 일단 확인 메시지를 보내고 통신이 완전히 끝날때까지 TIME_WAIT 상태를 유지한다
3. 이후 서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN플래그를 전송한다
4. 클라이언트는 확인했다는 ACK를 보낸다
5. 이후 클라이언트와 서버의 통신은 CLOSED된다


#### Q1. 서버에서 FIN을 전송하기 전에 클라이언트 쪽에서 전송한 패킷이 라우팅 지연이나 패킷 유실로 인한 재전송으로 인해 FIN패킷보다 늦게 도착하는 상황이 발생하면 어떻게 하는가?
A1. 클라이언트쪽에서 세션을 종료시킨후 뒤늦게 패킷이 도착하면 해당 패킷은 DROP되고 데이터는 유실된다. 이러한 상황을 대비하여 클라이언트는 서버로부터 FIN을 수신하더라도 일정시간동안(디폴트 240초) 세션을 남겨놓고 패킷을 기다리는 과정을 거친다 == __TIME_WAIT__   