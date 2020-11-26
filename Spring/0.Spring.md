[돌아가기](./README.md)

# 스프링이란?

객체 지향의 특징을 살려서 SOLID를 지키는 객체 지향 애플리케이션을 만들 수 있게 도와주는 프레임 워크

# 객체 지향의 특징

### 추상화

상태나 기능의 일반화 및 단순화 (인터페이스)

### 캡슐화

관련된 상태나 기능을 한 곳에 모으는 것 (클래스, 인터페이스)

### 상속

기존 클래스를 상속하여 기존의 특성을 재 정의하거나 확장

### 다형성

같은 자료 형에 여러가지 객체를 대입하여 다양한 결과를 얻어내는 성질

→ 어떤 역할(인터페이스, 슈퍼 클래스)에 대해 다양한 구현(클래스 및 객체)이 존재하는 것

e.g.,

```jsx
Hamburger burgerA = new BigMac();
Hamburger burgerB = new Whopper();
```

**오버라이딩과 오버로딩**

다형성을 실현시키는 기술

→ 이런 특징들을 통해 객체 지향 프로그래밍은 변경 및 확장, 유지 보수가 쉬운 소프트웨어 개발이 가능

- 즉, 전체 프로그램을 구성하는 일부 컴포넌트를 쉽게 교체하며 부분적으로 유지 보수 및 확장 가능

    → 교체할 컴포넌트를 의존하는 다른 컴포넌트, 즉, 클라이언트의 입장에서는 어떤 코드의 변경도 없도록 다형성을 이용하는 것이 중요

# 좋은 객체 지향 프로그래밍

객체 지향 설계 5가지 원칙(SOLID)를 잘 지키는 것

## SOLID

### SRP (Single Responsibility Principle)

한 클래스는 하나의 책임만 가진다

→ 다른 변경이 있을 때 파급 효과(side effect)가 없다면 단일 책임 원칙을 잘 따른 것

### OCP (Open Closed Principle)

확장에 열려 있으나 변경에는 닫혀 있다

→ 다형성 이용; 인터페이스를 구현하는 새로운 클래스를 통해 확장

**OCP 문제점**

클라이언트 입장에서, 다형성을 이용해도 OCP를 지킬 수 없다

```jsx
// 어떤 역할(인터페이스)에 대한 구현을 바꾸려면 다음과 같이 클라이언트 코드가 무조건 변경됨

// Hamburger burger = new BigMac();
Hamburger burger = new Whopper();
```

→ 객체를 생성하고, 연관 관계를 맺게 하는 별도의 조립 및 설정 모듈이 필요(제 3자의 개입)

### LSP (Liskov Substitution Principle)

어떤 의존 관계에서, 하위 타입의 개체로 바꿔도 프로그램의 정확성이 깨져서는 안된다

→ 다형성 지원하기 위한 원칙

단순히 구현이 컴파일 성공하는 것에 그치지 않고, 실제 인터페이스가 의도하는 것처럼 동작 해야 함

### ISP (Interface Segregation Principle)

클라이언트를 기준으로 삼아서, 여러 인터페이스로 상세하게 분리하는 것

e.g.,

세트 메뉴 인터페이스 → 햄버거 인터페이스, 감자튀김 인터페이스, 음료수 인터페이스

### DIP (Dependency Inversion Principle)

하위 타입(구현 클래스 및 객체)이 아니라 상위 타입(인터페이스 및 슈퍼 클래스)에 의존해야 한다

즉, 어떤 클라이언트 코드에서 DIP를 지킬 수 있는 형태는 다음이 이상적이다

```jsx
public class Client {

		// DIP 위반 (구현 클래스 BigMac을 의존하고 있음)
		// private Hamburger burger = new BigMac();

		// DIP 만족 (인터페이스만 의존)
		private Hamburger burger;

		public Client(Hamburger burger) {
				this.burger = burger;
		}
}
```

# 스프링의 DI

기존 객체 지향에서 OCP, DIP를 가능하도록 도와주는 기술

- DI(Dependency Injection): 의존 관계, 의존성 주입
- DI 컨테이너 제공

→ 클라이언트 코드의 변경 없이 확장 가능하도록 도와줄 수 있게 됨

즉, Spring은 OCP, DIP를 포함한 5가지 설계 원칙을 지키는 객체 지향 애플리케이션을 만들 수 있게 도와주는 프레임 워크
