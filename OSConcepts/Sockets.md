# Socket에 대해서

> 네트워크 소켓은 컴퓨터 네트워크를 경유하는 프로세스 간 통신의 EndPoint
> Socket은 End Point일뿐. 통신 방식은 별개입니다.

<br/>


## ✅ Socket Programming이란?
- 소켓 프로그래밍은 두 노드를 연결하여 통신하는 방법입니다.
- 서버 소켓, 클라이언트 소켓으로 구분하며, 각각의 연결 형성 방식은 차이가 있습니다.

![소켓  프로그래밍](https://user-images.githubusercontent.com/91730236/198833555-4e659cb7-a931-45dd-a411-092c38554c44.png)



#### [서버 사이드 소켓](https://github.com/t0e8r1r4y/C-CPLUS/blob/main/AsynchronousCProgramming/server/Server.c)
```C
static SockType_t 
listenSocket( int portNum, struct sockaddr_in *servAddr )
{
	SockType_t serverSocketFd = INVALID_SOCKET; // fd 초기화
	BaseType_t socketOption;
	struct sigaction action;

	int errsv = 0;

	action.sa_handler = SIG_IGN;
	sigemptyset( &action.sa_mask );
	action.sa_flags = 0;

	if( sigaction( SIGPIPE, &action, NULL ) < 0 ) return INVALID_SOCKET; // SIGPIPE 시그널 무시


	if( ( serverSocketFd = socket( AF_INET, SOCK_STREAM, 0 ) ) < 0 ) // open TCP socket
	{
		printf("fail : can't open stream socket\n");
		return INVALID_SOCKET;
	}

    // 클라이언트 재접속 시 소켓 재사용 옵션 
	socketOption = 1; // Set Socket Option
	if( setsockopt( serverSocketFd, SOL_SOCKET, SO_REUSEADDR, ( char * )&socketOption, ( int )sizeof( socketOption ) ) < 0 )
	{
		printf("fail socket option apply. option name is SO_REUSEADDR.");
		close(serverSocketFd);
		return INVALID_SOCKET;
	}

    // Adreess init
	memset( servAddr, 0, sizeof(struct sockaddr_in) );
	servAddr->sin_family = AF_INET;
	servAddr->sin_addr.s_addr = htonl( INADDR_ANY );  // 어느 IP건 접속 허용
	servAddr->sin_port = htons( portNum );
	

    // Bind Socket
	if( bind( serverSocketFd, ( struct sockaddr * )servAddr, sizeof(struct sockaddr_in) ) == -1 )
	{
		errsv = errno;
	    printf( "fail to bind local address(%s)\n", strerror(errsv));
		close(serverSocketFd); 
		return INVALID_SOCKET;
	}

	if( listen( serverSocketFd, 15 ) < 0 )  // Listening, connection queue is 15
	{
        printf("fail to liten for connection\r\n");
		close(serverSocketFd); 
		return INVALID_SOCKET;
	}

	return serverSocketFd;
}
```

- create socket
  - socket fd(file descriptor)에 end point를 생성
  - domain : 
  - communication type : SOCK_STREAM(TCP) VS SOCK_DGRAM(UDP)
  - protocol : Protocol value for Internet Protocol(IP), which is 0.
- set socket option
  - 서버에서는 주로 소켓 재사용 이런 옵션을 지정해줌
- Binding
  - 소켓이 IP주소와 포트번호에 바인딩하도록 하는 것
- Listening
  - 클라이언트의 접속을 기다림.
- Accepting
  - 외부의 소켓 접속이 있으면 이를 수락하고, 연결을 형성하는 단계.
  - 서버와 클라이언트 간 연결이 형성되고, 데이터를 주고 받을 수 있는 준비가 됨.


#### [클라이언트 사이드 소켓](https://github.com/t0e8r1r4y/C-CPLUS/blob/main/AsynchronousCProgramming/client/ClientSocketCtl.c)

```C
static SockType_t
tcpCreateClient(int ip, unsigned short port )
{
	int res = 0;			// function retrun;
	int socketFd  =  -1;
	int	buffSize;
	int lValue = 1;			// set NODELAY 옵션

	struct sockaddr_in	nSin;

	// socket
	socketFd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP );

	if( socketFd == INVALID_SOCKET )
	{
		printf("Socket Command error[%s-%d]\n", strerror(errno), errno );
		return (-1);
	}

	int temp = sizeof(int);
	// socket option get
	if(getsockopt(socketFd, SOL_SOCKET, SO_RCVBUF, &buffSize, (socklen_t *)&temp) < 0)
	{
		return -1;
	}

	// socket option set
	res = setsockopt(socketFd, IPPROTO_TCP, TCP_NODELAY, (char*)&lValue, sizeof(int));

	if(res == -1)
	{
		return -1;
	}


	nSin.sin_family 	= AF_INET;
	memcpy(&nSin.sin_addr, &ip, sizeof(ip));
	nSin.sin_port		= htons(port);


	// socket Connection

    res = connect(socketFd, (const struct sockaddr*)&nSin, sizeof(nSin));

    if( res < 0 )
	{
		printf("connection fail\r\n");
		return (-1);
	}

    
    // On Success to Connection.
    printf("Client Socket connect OK Server Socket[%d] IP[%s, %i] \n", socketFd, inet_ntoa(nSin.sin_addr), nSin.sin_port);

    // Non-Blocking setting
    res = fcntl( socketFd, F_SETFL, O_NONBLOCK);
    if( res < 0 )
    {
        printf("(HOST) : Error fcntl() %d - %s\n", errno, strerror(errno));
        tcpCloseSocket((int *)socketFd);
        return (-1);
    }
		

    return socketFd;
}
```

- create socket
- connect


<br/>


## ✅ 소켓통신이 중요한 이유
- 기본적으로 웹이든 뭐든 소켓통신을 베이스로 이루어진다는 점에서 매우 중요함.
- TCP/IP 통신은 OS Layer의 3번째 단계로, 그 상위 단계에서 이루어지는 데이터 전송은 모두 3레이어를 통해서 이루어진다.

<br/>

## ✅ㅣ 소켓 통신 방식 TCP/UDP 차이점
- TCP와 UDP 통신 프로토콜은 같은 네트워크 레이어에서 이루어지는 방식이지만, 통신의 연결방식, 패킷 교환 방식, 수신 여부 확인 방식의 차이로 속도와 데이터 신뢰성에서 차이를 가지고 있습니다.
- TCP 통신 방식은 데이터 신뢰성을 확보에 목적성이 강하며 아래 세가지 특징을 가지고 있습니다.
    - :exclamation:[3-way handshaking과 4-way handshaking](https://github.com/t0e8r1r4y/blogContents/blob/main/OSConcepts/handshake.md)을 사용하여 통신 연결상태를 체크하고 송신과 수신의 주체를 명확하게 합니다.
    - 데이터를 수신하면 ACK 혹은 NAK를 전송하여 수신 여부를 체크하여 정확성을 확보합니다.
    - 패킷을 교환하는 과정에서는 TCP HEADER 프레임에 흐름 제어와 혼잡제어에 필요한 데이터를 표시하여 데이터의 신뢰성을 확보합니다.
    - 단, 데이터의 신뢰성을 확보하는 과정이 UDP에 비해 더 단계가 많기 때문에, 처리 지연이 발생(속도 저하)하고, 통신과 관련하여 CPU 사용에 대한 컴퓨팅 비용이 추가되기 됩니다.
- UDP 통신 방식은 데이터 전달 목적의 최소한의 처리과정만 거침으로서 TCP 방식에 비해 속도는 빠른 특성이 있습니다. TCP 통신에 비해 속도가 빨리지는 특징은 아래와 같습니다.
    - UDP는 소켓과 같은 연결 매커니즘이 없이 IP 기반으로 데이터를 전송하기에 연결과 관련된 컴퓨팅 비용과 처리 지연을 줄 일 수 있습니다.
    - 수신 여부확인, 흐름과 혼잡제어 대한 처리 과정이 없습니다. UDP 데이터 프레임 헤더를 보면, 최소한의 체크섬만 확인을 하여 데이터를 전송합니다.
    - 단, 통신의 순서나, 데이터 무결성이 보장되지 않기 때문에 신뢰성이 떨어집니다.
    - 동일한 OS 환경에서 프로세스간 주요 설정 정보를 공유하는 기능에서 UDP 통신을 사용해본 경험이 있는데, 여러 설정 정보를 수신하는 과정에서 순서가 상관이 없었고, 미수신시 재송신 요청 처리 로직만 추가하면 되는 정도에서 사용한 경험이 있습니다.


<br/>

## ✅ 웹소켓과의 차이점
- 웹소켓은 7Layer에서 생성되는 연결인데, 통신 연결을 위한 3-handshakes와 4-handshakes가 http 프로토콜로 7Layer에서 이뤄진다는 것이 일반 소켓통신과 차이점이다.
