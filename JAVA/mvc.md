[돌아가기](./README.md)

# MVC 디자인 패턴

애플리케이션의 기능을 3가지 컴포넌트(Model, View, Controller)로 나누어 설계하는 디자인 패턴

view와 model 간의 종속성을 controller를 중간에 두는 것을 통해 분리시키는 작업

# Model

- business layer
- data access layer (data access object)

    DB와 직접 접근하는 레이어 (객체)

    → DTO 패턴

### DTO

data transfer object

### VO

value object (또는 Domain object)

비즈니스 도메인에 필요한 항목을 모아놓은 비즈니스 객체

# View

presentation layer (UI layer)

- web

    HTML, JSP

- standalone

    Swing

# Controller

model과 view 사이의 다리 역할

→ view에서 받아올 데이터 형식과 어떤 서비스를 제공하는지 등을 숙지
