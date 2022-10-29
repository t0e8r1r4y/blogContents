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


