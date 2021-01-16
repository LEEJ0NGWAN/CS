[돌아가기](./README.md)
# HTTP (HyperText Transfer Protocol)

하이퍼텍스트같은 웹 자원을 빠르고 간단하게 교환하기 위한 프로토콜

클라이언트와 서버가 메세지를 주고 받기 위해 정해 놓은 규칙(클라이언트-서버 프로토콜)

### 하이퍼텍스트(HyperText)

기존 텍스트와 달리, 비선형적인 flow를 가진 텍스트

→ 기존 텍스트(책을 포함한 물리적 인쇄물)의 흐름은 단방향의 선형적인 flow를 가지고 있음

그러나, 하이퍼텍스트의 경우 하이퍼링크를 통해 각 텍스트들이 비 선형적 구조로 연결되어 있다

### 하이퍼링크(HyperLink)

컴퓨터 상에 존재하는 자원들의 주소를 비선형적으로 연결해 주는 인터페이스

# 특징

### Connectionless

클라이언트의 요청에 해당하는 응답을 한 뒤, 서버가 연결을 끊는 성질

### Stateless

어떤 클라이언트와 어떤 정보를 주고 받았는지, 어떤 상태에 있는지를 유지하지 않는 성질

→ 사용자 Authentication과 같은 작업을 위해 cookie + session을 이용

- **Cookie**

    클라이언트의 상태를 저장하기 위해 웹 브라우저에서 보관하는 데이터

    → 서버가 발급해주는 쿠키를 클라이언트 사이드의 웹 브라우저에 저장

    key-pair 구조로 이루어져 있으며, 

    서버로부터 발급 받은 쿠키는 추후 헤더에 실어서 서버에 전송

- **Session**

    클라이언트의 상태를 저장하기 위해 서버에서 관리하는 데이터

    웹 브라우저(클라이언트)마다 각각 고유 세션 ID를 가지는 별도의 세션 발급

    → 웹 브라우저는 할당받은 세션 ID를 쿠키로 보관

- **Cookie + Session**

    사용자의 상태를 유지하기 위해, 서버에서 세션을 생성

    그 후 생성된 세션의 ID를 쿠키로 웹 브라우저로 발급

    웹 브라우저는 할당받은 세션 ID를 헤더에 실어서, 추후 요청마다 세션 ID 제시

    서버는 요청 때 헤더에 실린 세션 ID를 이용하여 사용자의 상태를 조회

# 구조

### 요청(Request)

클라이언트가 서버에 데이터 수신을 위해 보내는 메세지

**요청 구조**

```jsx
{Method} {Path} {HTTP Version}
{HTTP Headers}

[HTTP Body]
```

**요청 메소드**

- HEAD: URL에 해당되는 웹 자원의 헤더만 요청
- GET: URL에 해당하는 웹 자원 요청 (주소창에 메세지 표시됨)
- POST: 서버로 어떤 데이터 전송 (HTTP BODY에 메세지 포함)
- PUT: 서버로 어떤 데이터 저장 요청
- DELETE: 서버로 어떤 데이터 삭제 요청
- PATCH: 서버로 어떤 데이터 수정 요청
- TRACE: 서버에 송신한 리퀘스트 내용 반환 요청
- CONNECT: 특정 프록시 서버 연결 요청
- OPTIONS: 해당 URL의 웹자원이 제공하는 HTTP 메소드 목록 요청

### 응답(Response)

서버가 클라이언트 요청에 알맞는 데이터를 송신하기 위해 보내는 메세지

**응답 구조**

```jsx
{HTTP Version} {Status code} {Status message}
{HTTP Headers}

[HTTP Body]
```

**스테이터스 코드**

- 1XX: 요청을 받았고, 서버가 현재 서비스 작업 중에 있다는 것을 의미
- 2XX: 요청을 받았고, 작업을 성공했다는 의미
- 3XX: 리디렉션을 의미
- 4XX: 클라이언트 측에 문제가 있다는 의미
- 5XX: 서버 측에 문제가 있다는 의미