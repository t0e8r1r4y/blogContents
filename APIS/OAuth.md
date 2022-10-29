# OAuth에 대해서

> OAuth는 인가를 제공하는 프로토콜입니다. ( 인증 X )  
> [OAuth 관련 스프링 프로젝트](https://github.com/t0e8r1r4y/NaverAPI), [구글 OAuth 사용 예시](https://github.com/t0e8r1r4y/springframework/tree/main/googleAuth)


## OAuth란?
- OAuth는 인터넷 사용자들이 비밀번호를 제공하지 않고 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수 있는 공통적인 수단으로서 사용되는, 접근 위임을 위한 개방형 표준이다.\

<br/>

## OAuth 참여자
- Resource Server : Client가 제어하고자 하는 자원을 보유하고 있는 서버. 구글 페이스북 트위터 등등
- Resource Owner : 자원의 소유자. Client가 제공하느 서비스를 통해 로그인하는 실제 유저
- Client : Resource Server에 접속해서 정보를 가져오고자 하는 클라이언트


<br/>

## OAuth Flow
1. 클라이언트 등록
  - 등록절차를 통해서 Client ID, Client Secret, Authorized redirect URL을 부여받음
2. 리소스 오너의 승인
3. 리소스 서버의 승인
4. API 호출
5. 토큰 새로고침


<br/>

## 참고자료
- [생활코딩](https://opentutorials.org/course/3405)
