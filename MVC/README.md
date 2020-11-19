[돌아가기](https://github.com/LEEJ0NGWAN/CS#MVC)

# MVC pattern

애플리케이션을 3개 컴포넌트(Model View Controller)로 구성해서 개발하는 디자인 패턴

# 동작 방식

### 요청(request)

User → Controller

### 응답(response)

User ← View ← Controller ↔︎ Model

# Model

애플리케이션의 정보, 데이터를 나타내고 가공을 책임지는 컴포넌트

→ DB, 상수, 초기 값, 변수 등...

### 규칙

- 사용자가 조작하는 모든 데이터를 소유
- 독립 (view, controller 종속 x)
- 변경 이벤트 핸들링 필요 (model 변경에 대한 이벤트 발신 및 수신 처리)

# View

UI 요소를 나타내는 컴포넌트

사용자로부터 데이터 및 객체 입력과 사용자로 화면 출력을 담당

### 규칙

- 데이터 출력 및 입력의 역할만 수행 (데이터 내부 저장 x)
- 독립 (model, controller 종속 x)
- 변경 이벤트 핸들링 필요 (view 변경에 대한 이벤트 발신 및 수신 처리)

# Controller

데이터와 UI 요소를 이어주는 매개체 컴포넌트

### 규칙

- model, view 파악 (model, view 연결)
- model, view 모니터링 (model, view 변경 이벤트 시 해석 및 전달 + 메인 로직 구성)

# MVC 패턴 사용 이유

유지 보수, 확장, 유연성의 증가

→ 역할 별로 개발 해야할 부분이 분리 되므로, 개발자들은 각각 맡은 바에 집중할 수 있음
