[돌아가기](https://github.com/LEEJ0NGWAN/CS)

# Aspect Oriented Programming

어떤 객체를 핵심 로직과 비핵심 로직으로 나누어 보고, 다른 컴포넌트와 비교했을 때 공통 모듈화 할 수 있는 부분을 추출하여 재사용하는 프로그래밍 기법

### 핵심 로직 (Core Concern)

객체를 구성하는 로직에서, 해당 컴포넌트만이 수행하므로 차별화 될 수 있는 로직

### 공통 로직 (Cross Cutting Concern; 횡단 관심사)

여러 객체에서 공통적이면서 부가적으로 나타나는 로직

# 장점

### 공통 기능 모듈화

애플리케이션 전체에 걸쳐 흩어진 공통 기능을 하나의 장소에 보관하고 관리할 수 있다

### 서비스 모듈의 개발 향상

다른 서비스 모듈들은 각각 목적에 맞는 핵심 로직에만 책임을 가지게 되어 테스트에 용이하고 변경이 쉽기 때문에  개발이 수월해진다

# 주요 개념

### Target

핵심 로직을 구현하는 클래스로, 공통 로직을 부여하는 대상을 의미

### Advice

특정 JoinPoint에 삽입 되어져 동작할 수 있는 기능을 정의한 코드 (구현체)

- 독립된 클래스의 메소드 형태로 작성
- 순수하게 부가기능(비 핵심 로직 기능)에만 집중 가능한 메소드 코드

e.g., 수행시간을 기록하는 Advice

```java
@Around( ... )
public Object calculatePerformanceTime(ProceedingJoinPoint proceedingJoinPoint) {
	...
}
```

→ @Around JoinPoint에 대해, calculatePerformanceTime 기능을 수행

### JoinPoint

Advice가 핵심 로직에 적용될 수 있는 위치(Point)를 정의

- Spring에서는 메소드 조인포인트만 제공
- 적용 되는 시점
    - Before
    - After
    - AfterReturning
    - AfterThrowing
    - Around (위 4가지 전부 커버)

### PointCut

Advice를 적용할 JoinPoint를 선별하는 기능을 정의하는 모듈

- JoinPoint 필터링 조건 (타입 필터링, 메소드 필터링)
- JoinPoint의 부분집합
- 복수의 JoinPoint를 하나로 묶은 것

e.g., 수행시간기록 Around Advice에 대해, 타겟 BoardService.getBoards를 JoinPoint로 설정한 포인트 컷

```java
@Around("execution(* com.example.demo.BoardService.getBoards(..))")
public Object calculatePerformanceTime(ProceedingJoinPoint proceedingJoinPoint) {
	...
}
```

### Aspect

핵심 로직을 가지는 클래스에 부가되어 의미를 갖게 되는 모듈

→ Aspect = Advice + PointCut

e.g., 수행시간기록 Around Advice와 PointCut을 가지는 Performance Aspect

```java
@Aspect
@Component
public class Performance {

	@Around("execution (* com.example.demo.board.BoardService.getBoards(..))")
	public Object calculatePerformanceTime(ProceedingJoinPoint proceedingJoinPoint) {
		...
	}

	...
}
```

### Proxy

Target을 감싸서 Target으로 오는 요청을 가로채는 Wrapping 오브젝트

- 클라이언트(호출자)에서 Target을 호출하면 Target을 감싸는 프록시가 호출 됨

### Introduction

Target의 코드 변경 없이 신규 메소드나 맴버 변수를 추가하는 기능

# Wieving

지정된 객체에 Aspect를 적용해서 새로운 프록시 객체를 생성하는 과정

- 컴파일 위빙
    - 컴파일 되는 핵심 로직 클래스에 공통로직 호출 코드 삽입
- 메모리 로드 시 위빙
    - 메모리에 로드 된 바이트 코드 조작하여 공통 로직 호출 코드 삽입
- 런타임 위빙 (Spring 채택 방식)
    - 핵심 로직 캡슐화 한 프록시 생성 후 공통 로직 호출 코드 삽입

# PointCut 문법

`어드바이스When`("`포인트컷 표현식`")

e.g., getBoards JoinPoint에 대한 포인트컷과 어드바이스

`@Around("execution(* com.example.demo.board.BoardService.getBoards(..))")`

- `@Around`

    Advice의 "언제"를 나타내는 애노테이션.

    후에 이어지는 메소드 정의는 Advice의 "무엇"을 나타내게 된다

- `execution`

    포인트 컷 지정자

- `*`

    모든 리턴 타입

- `...BoardService.getBoards(..)`

    필터링 된 타겟 메소드

## 포인트컷 지정자

### args()

메소드의 인자 타입을 통해 Target 조건 필터링

e.g., 하나의 파라매터를 인자로 갖는데, 그 인자가 Hamburger 타입인 모든 메소드를 JoinPoint로 설정

`@Before("args(com.example.demo.domain.Hamburger)")`

### @args()

메소드의 인자 애노테이션 타입을 통해 Target 조건 필터링

e.g., 하나의 파라매터를 인자로 갖는데, 그 인자가 Drink 애노테이션을 갖는 모든 메소드를 JoinPoint로 설정

`@After("@args(com.example.demo.domain.Drink)")`

### execution()

접근 제한자, 리턴 타입, 인자 타입, 클래스/인터페이스, 메소드명, 파라미터 타입, 예외 타입과 같은 부분을 전부 조합 가능한 포인트 컷 지정자

e.g., User의 모든 메소드를 JoinPoint로 설정

`@Around("execution(* com.example.demo.domain.User.*(..))")`

### within()

클래스/인터페이스를 지정하여, 해당 객체의 모든 메소드를 JoinPoint로 지정하는 포인트컷 지정자

e.g.,

`@AfterReturning("within(com.example.demo.domain.SideMenu")`

`@AfterReturning("within(com.example.demo.domain.*")`

`@AfterReturning("within(com.example.demo.*")`

### @within()

지정된 애노테이션을 사용하는 어떤 타입을 리턴하는 모든 메소드를 JoinPoint로 지정하는 포인트컷 지정자

### this()

특정 메소드를 가지는 빈 타입의 인스턴스에 대해 JoinPoint로 설정

### target()

특정 메소드를 가지는 빈 타입이 아닌 인스턴스에 대해 JoinPoint로 설정

### @target()

특정 애노테이션을 가지는 클래스에 대해 JoinPoint로 설정

### @annotation

특정 애노테이션을 가지는 메소드를 JoinPoint로 설정
