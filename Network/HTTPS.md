[돌아가기](./README.md)

# HTTPS

기존 http 프로토콜의 보안성을 강화한 프로토콜로 주고 받는 패킷을 암호화하는 TLS를 이용한 프로토콜

→ TLS(Transport Layer Security): 정보를 암호화해서 송수신하는 프로토콜; SSL에 기반한 기술

Port: 443 (HTTP는 80)

# 사용 이유

패킷을 주고 받는 중간에 공격이나 도청과 같은 위험을 방지하고, 안전한 통신을 하기 위해 사용

# HandShaking

1. [Client]: ClientHello 메세지 전송
    - ClientHello

        클라이언트가 사용 가능한 TLS 버전, 서버 도메인, 세션 식별자, 암호 설정

2. [Server]: ServerHello 메세지 전송
    - ServerHello

        클라이언트가 제안한 TLS 버전 중 서버가 선택한 TLS 버전, 세션 식별자, 암호 설정

3. [Server]: Certificate 메세지 전송 및 ServerHelloDone 메세지 전송
    - Certificate

        서버가 CA로부터 발급받은 TLS 인증서를 포함(인증서에는 비대칭 암호에 사용될 공개키 포함)

    - ServerDone

        인증서 전송 끝을 알리는 메세지

4. [Client]: 서버가 보낸 TLS 인증서를 검증(유효 기간과 CA의 유효성 등) 후 신뢰 가능하다면 다음 단계 수행

5. [Client]: ClientKeyExchange 메세지(TLS 공개키로 암호화한 pre-master secret를 포함) 전송
    - pre-master secret?

        세션 키 생성 틀

6. [Server]: 개인키로 pre-master secret을 복호화 후, master secret 및 세션 키 생성
    - master secret?

        클라이언트로부터 받은 pre-master secret를 이용해 만든 세션 키 생성 틀

7. [Client, Server]: 각자에게 ChangeCipherSpec 메세지 전송
    - ChangeCipherSpec?

        pre-master, master secret으로 생성된 세션 키를 앞으로 통신의 대칭키 암호로 사용할 것임을 알림

### HTTPS HandShaking에서 비대칭 키 암호를 한번만 쓰는 이유

비대칭 키 암호의 하드웨어 자원 소비가 심하기 때문

→ 보안 수준 대비 속도를 보장하려면 대칭 키 암호를 사용해야 함

그러므로, handshaking 후에 통신의 대칭 키 암호에 사용될 세션 키 생성을 위해 단 한번 비대칭 키 암호 사용

# HTTPS의 단점

크기가 큰 웹 자원을 전송하는 패킷일수록 TLS 과정의 속도 손해가 있다

→ HTTP/2 도입으로 TLS 속도 향상
