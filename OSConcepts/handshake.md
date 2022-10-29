# TCP의 3-Handshake와 4-HandShake란?

## 3-way handshake의 기본 매커니즘
- TCP 통신은 PAR ( Positive Acknowledgement with Re-transmission)을 통해 신뢰적인 통신을 제공한다.
- PAR은 ACK 전송을 통해서 데이터가 정상적으로 보내 데이터가 맞게 갔는지 확인을하고, 혹시 Nak를 수신하는 경우 재전송을 통해 데이터의 무결성을 확보한다.
- :exclamation: PAR을 사용하는 기기는 ack를 받을 때 까지 데이터 유닛을 재전송한다. 하지만 `무한 재전송은 아니다`.
- 이 과정에서 클라이언트와 서버 사이에는 3개의 Segment가 교환되는 것을 확인할 수 있다. 이것이 3 - handshake의 가장 기본 매커니즘이다.

#### 동작 방식
![3핸드쉐이트](https://user-images.githubusercontent.com/91730236/198835324-5f4f1932-8bad-4948-9be0-3163a0eb344b.jpeg)
- 위 그림에서는 Client가 먼저 요청을 하는 상황입니다.
- 1️⃣ 클라이언트는 서버와 커넥션 연결을 위한 SYN을 보낸다.
  - 송신자가 최초로 데이터를 전송 시, `시퀀스 넘버`를 임의의 숫자로 지정하고, SYN 플래그 비트를 1로 설정한 세그먼트를 전송하다.
  - PORT 상태는 Client : CLOSED -> SYN_SEND로 변환되며 SERVER는 LISTEN 상태이다.
- 2️⃣ 서버가 SYN(x)를 받고, 클라이언트로 받았다는 신호인 ACK와 SYN 패킷을 보낸다.
  - 접속요청을 받은쪽에서 요청을 수락했으며, 접속을 요청한 프로세스도 포트를 열어달라는 메시지를 전송한다.
  - ACK Number 필드를 Sequence Number + 1로 지정하고 SYN와 ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다.
  - PORT 상태 : Client는 CLOSED, Server는 SYN_RCV이다.
- 3️⃣ 클라이언트는 서버에서 보낸 응답인 ACK와 SYN 패킷을 받고 ACK를 서버로 보낸다.
  - 마지막으로 접속 요청 프로세스가 수락 확인을 보내 연결을 맺는다.
  - 이때, 전송할 데이터가 있으면 이 단계에서 데이터를 전송할 수 있다.
  - Port상태는 Client : ESTABLISHED, Server : SYN_RCV -> ACK -> ESTABLISHED

- 위 과정을 통해서 `전 이중화 통신`이 형성이 된다. 통신하는 쌍방은 데이터 송신과 수신을 동시에 할 수 있다.


<br/>
<br/>


## 4-way handshake의 기본 매커니즘
- 연결을 해제하는 과정이다. 여기서는 FIN 플래그를 이용한다.
- `FIN`(finish) : 세션을 종료시키는데 사용되며, 더 이상 보낸 데이터가 없음을 나타낸다.

#### 종료의 방식
- 정상적인 종료방식(Graceful connection release)
- 비정상적인 종료방식(Abrupt connection release)
  - 갑자기 한 TCP 엔티티가 연결을 강제로 닫는 경우
  - 한 사용자가 두 데이터 전송 방향을 모두 닫는 경우
  - 이 경우에 `RST(TCP Reset)` 세그먼트가 전송되면 비정상적인 연결 해제가 수행된다.
    - 존재하지 않는 TCP 연결에 대해 비SYN 세그먼트가 수신된 경우
    - 열린 커넥션에서 일분 TCP 구현은 잘못된 헤더가 있는 세그먼트가 수신된 경우
    - 일부 구현에서 기존 TCP 연결을 종료해야 하는 경우 -> 리소스가 부족할 때, 원격 호스트에  연결할 수 없고 응답이 중지되었을 떄

#### 동작방식 ( 정상적인 종료 방식의 경우 )
![TheFourWayHandshakeProcess](https://user-images.githubusercontent.com/91730236/198836095-5f28d2a5-3ad3-487e-a9ab-43f9c82550e5.jpeg)

> 기본적으로 Half-close 기법을 사용한다.

- 1️⃣ 서버와 클라이언트가 연결된 상태에서 클라이언트가 close()를 호울하여 접속을 끊으려고 한다.
  - 이 시점에서 client는 서버에  연결을 종료한다는 `FIN 플래그`를 보낸다.
  - 이 때 `FIN 패킷`에는 실질적으로 `ACK도 포함`되어 있다.
- 2️⃣ 서버는 FIN을 받고 확인했다는 ACK를 클라이언트에게 보내고 자신의 통신이 끝날때까지 기다린다. `TIME_WAIT` 상태
  - 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보낸다. (TIME_WAIT 상태)
  - 서버는 ACK Number 필드를 시퀀스 번보 + 1로 지정하고 ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다.
  - 서버는 클라이언트에게 응답을 보내고 `CLOSE_WAIT` 상태에 들어간다. 아직 남은 데이터가 있다면 마저 전송을 마친 후에 close()를 호출한다.
  - 클라이언트는 서버에서 ACK를 받은 후에 서버가 남은 데이터를 처리하고 FIN 패킷을 보낼때 까지 기다린다. `FIN_WAIT_2`
- 3️⃣ 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보낸다.
  - 아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT를 통해 기다린다.
  - 이때 TIME_WAIT 상태는 의도치 않은 에러로 인해 연결이 데드락으로 빠지는 것을 방지한다.
  - 만약 에러로 인해 종료가 지연되다가 타임이 초과되면 `CLOSED`로 들어간다.
  - 서버는 ACK를 받은 이후 소켓을 닫는다.
  - TIME_WAIT 시간이 끝나면 클라이언트도 닫는다.


<br/>

#### ❓ 면접 질문1  
Q. TCP의 연결 설정 과정(3단계)과 연결 종료 과정(4단계)이 단계가 차이나는 이유?  
A. Client가 데이터 전송을 마쳤다고 하더라도 Server는 아직도 보낼 데이터가 남아있을 수 있기 때문에 일단 FIN에 대한 ACK만 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기 때문이다.  

#### ❓ 면접 질문2  
Q. 만약 Server에서 FIN 플래그를 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN 패킷보다 늦게 도착하는 상황이 발생하면 어떻게 될까?  
A. 이러한 현상에 대비하여 Client는 Server로부터 FIN 플래그를 수신하더라도 일정시간동안 세션을 남겨 놓고 잉여 패킷을 기다리는 과정을 거친다. ( TIME_WAIT 과정 )  

#### ❓ 면접 질문3
Q. 초기 시퀀스 넘부인 ISN을 0부터 시작하지 않고 난수를 생성해서 설정하는 이유는?
A. 초기 커넥션을 맺을 때 사용하는 포트는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용 된다. 따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용하는 가능성이 존재한다. 서버측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데 난수가 아닌 순차적인 Number가 전송된다면 이전의 Connection으로부터 오는 패킷으로 인식할 수 있다. 이러한 발생가능성을 줄인다.




<br/>

## 참고자료
- [링크1](https://www.geeksforgeeks.org/why-tcp-connect-termination-need-4-way-handshake/)
- [링크2](https://velog.io/@averycode/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-TCPUDP%EC%99%80-3-Way-Handshake4-Way-Handshake#%F0%9F%A5%9A-tcp%EC%99%80-udp)

