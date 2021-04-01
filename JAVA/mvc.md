[돌아가기](./README.md)

# MVC 디자인 패턴

애플리케이션의 기능을 3가지 컴포넌트(Model, View, Controller)로 나누어 설계하는 디자인 패턴

view와 model 간의 종속성을 controller를 중간에 두는 것을 통해 분리시키는 작업

# Model

- business layer
- data access layer (data access object)

    DB와 직접 접근하는 레이어 (객체)

    → DTO 패턴

## business layer

### service

비즈니스 로직을 처리하는 객체

## data access layer

### DTO

data transfer object

### VO

value object (또는 Domain object, DTO)

비즈니스 도메인에 필요한 항목을 모아놓은 비즈니스 객체

### DAO

data access object

DB 데이터에 접근 및 조회 수정하기 위해 생성하는 객체

→ DB 접근 로직과 비즈니스 로직 분리를 위해 사용

DB 접속 및 데이터 CRUD 작업을 시행하는 클래스

# View

presentation layer (UI layer)

- web

    HTML, JSP

- standalone

    Swing

# Controller

model과 view 사이의 다리 역할

→ view에서 받아올 데이터 형식과 어떤 서비스를 제공하는지 등을 숙지

# Front Controller 디자인 패턴

## Controller 역할

- request parameter 추출
- verify paremeter
    - 성공
    - 실패 view 이동
- service 실행 (Model)

    parameter → VO 로 포장 및 전달

    - 성공 → view(또는 다른 컨트롤러) 이동 (e.g., 회원 가입 성공 → 로그인 컨트롤러)

        view → controller → view 과정이 권장됨

    - 실패 →실패 view 이동

캐싱 금지 응답 헤더 setting 설정 가능

# 프록시 패턴

다양한 요청 들에 대해 공통된 로직을 분리시켜 재사용 가능한 모듈로 독립시키는 것
