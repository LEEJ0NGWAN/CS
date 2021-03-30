[돌아가기](./README.md)

### java SE vs java EE

- java SE

    순수 자바 (not include web)

- java EE (server side)

    web + java

    → Servlet, JSP

# Web Architecture

### Client

웹 브라우저 해당되고, 데이터를 발생시켜 서버에 요청하고 응답을 받음

- request

    서버로 요청 데이터를 전송

- response

    서버로부터 응답 데이터 수신

### Server

크게 3가지로 구성되어 있다

- Web Server

    정적 웹 서버로 클라이언트의 접속을 처리

- Application Server (WAS)
    - Presentation
    - Business Logic
    - Persistence Logic (DB 접근)
- RDBMS

    데이터 영속성

# Servlet 동작 흐름

1. [client] → [server] 요청 전송
2. [server]
    1. 요청 data get
    2. Logic - Business 수행
    3. DB (with JDBC)
    4. response page 생성
3. [server] → [client] 응답 전송

# Servlet's Life-Cycle

Servlet class는 SE와 다르게 main 메소드가 없다

→ 객체의 생성부터 사용(메소드 호출)의 주체가 사용자가 아닌 Servlet Container에게 있다

Client가 요청하면 Servlet Container는 Servlet 객체를 생성 및 초기화(한번만) 후,

요청에 대한 처리(요청 시 마다 반복)하게 된다

또, Servlet 필요 없어질 때 제거 작업도 컨테이너 담당

### 주요 메소드

- init()

    서블릿 메모리 로드 시 한번 호출

- doGet()

    GET 방식 데이터 전송 시 호출

- doPost()

    POST 방식 데이터 전송 시 호출

- service()

    모든 요청을 받고 doXXX() 메소드로 전달

- destroy()

    서블릿 메모리 해제 시 호출

### 서블릿 객체 생성 순서

- IsServletLoaded?

    No 일 경우 객체 생성을 위해 서블릿의 클래스 파일 적재 단계 이동

- Class File 메모리 로드

    서블릿 객체 생성을 위해 메모리에 클래스 적재

- init() (1번 실행)

    객체 생성 시 딱 한번 실행되는 메소드

- ready (서비스 실행 가능)

    리퀘스트가 올 때까지 대기 상태 진입

- doGet() or doPost()

    리퀘스트가 왔을 때, 메소드 타입에 따라 doGet 또는 doPost 실행

- destroy() (1번 실행)

    해당 서블릿이 필요 없어지면 폐기

# JSP (Java Server Page)

HTML 내부에 자바 코드를 삽입하여, 웹 서버에서 동적으로 웹 페이지를 생성하여 웹 브라우저에 돌려주는 언어

## 선언 (Declaration)

멤버 변수 선언 또는 메소드를 선언하는 영역

`<%! 변수 및 메소드 작성 %>` 형태를 취함

e.g.,

```java
<%!
String name;

public void init() {
	name = "ljw";
}
%>
```

## 스트립트릿(Scriptlet)

클라이언트 요청 시 매번 호출되는 영역으로, 서블릿 변환 시 _jspService() 메소드에 해당하는 영역

request, response 관련 코드 구현

`<% 로직 코드 %>` 형태를 취함

e.g.,

```java
<%
System.out.println("<tr>");
for (int i=0; i<5; i++)
System.out.println("<td>"+i+"</td>");
System.out.println("</tr>");
%>
```

## 표현식 (Expression)

데이터를 브라우저에 출력하는 영역

`<%= 문자열 %>` 형태를 취함

e.g.,

```java
안녕안녕 <%= name %>!!!
```

## 주석 (Comment)

코드 상에 부가 설명을 작성

`<%— 주석 코드 %>` 형태를 취함

e.g.,

```java
<%-- 주석 입니다..%>
```

## JSP 지시자 (Directive)

`<%@ 지시어 속성="값" ... %>` 형태를 가짐

지시어: page, include, taglib ...

속성: contentType, import, file ...

### 1. page Directive

컨테이너에게 현재 JSP 페이지에 대한 정보 제공

`<%@ page attr1="val1" attr2="val2" ... %>`

### 2. include Directive

특정 jsp file을 페이지에 포함

여러 jsp 페이지에서 재사용되는 부분을 jsp file로 모듈화 후, 반복 영역에 include 처리

`<%@ include file="/template/header.jsp" %>`

### 3. taglib Directive

JSTL 또는 사용자가 만든 커스텀 태그 사용시 이용되는 지시자로, jsp 내에서 불필요한 자바 코드를 줄인다

`<%@ taglib prefix="c" url="http://java.sun.com/jsp/jstl/core" %>`

# jsp 기본 객체의 영역 (scope)

- pageContext

    하나의 jsp 페이지 처리 시 사용되는 영역

    → 커스텀 태그에서 새로운 변수 추가 시 사용

- request

    하나의 http 요청 처리 시 사용되는 영역

    → 요청 응답시 사라짐

- session

    웹 브라우저 관련된 영역

- application

    웹 애플리케이션 관련된 영역

## EL (Expression Language)

표현을 위한 언어로, jsp 스크립트 표현식 대신 속성 값을 쉽게 출력하도록 고안됨

표현식 `<%=%>` 을 대체한다

`${ Map or Bean, Map 키 or Bean 프로퍼티}` 또는 `${Map[키]}`

- EL 표현식의 도트 연산자 왼쪽: java.util.Map 또는 Java Bean
- EL 표현식의 도트 연산자 오른쪽: Map의 키 또는 Bean 프로퍼티
- EL 제공 기능
    - JSP 4가지 기본 객체가 제공하는 영역의 속성 사용
    - 자바 클래스 메소드 호출
    - 표현 언어만의 기본 객체
    - 수치, 관계, 논리 연산 제공

e.g.,

`<%= ((model.MemberDto)request.getAttribute("user")).getZipDto().getAddress() %>`

→ `${user.zipDto.address}`
