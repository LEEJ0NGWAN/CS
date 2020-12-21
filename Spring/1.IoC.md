[돌아가기](./README.md)

# IoC (Inversion of Control; 제어의 역전)

기존의 방식과 반대로 프로그램 제어 흐름을 외부에서 통제하는 것

→ 기존: 어떤 객체가 필요로 하는 다른 객체를 내부에서 직접 생성, 연결 및 실행 (개발자가 직접 제어)

→ IoC: 어떤 객체가 필요로 하는 다른 객체를 외부에서 받아옴 (제어의 역전)

# framework vs library

제어권이 개발자에게 있는가 없는가의 차이가 있음

### framework

개발자가 작성한 코드에 대해 제어권을 가져가고 대신 실행

### library

개발자는 작성한 코드를 직접 제어 흐름을 관리하고 실행

# DI (Dependency Injection; 의존성 주입)

### 의존성?

어떤 객체를 구성하기 위해 다른 객체를 필요로 하는 것

e.g., 쇠필통은 필통, 연필, 지우개를 의존한다.

```jsx
// 필통 의존성
public class MetalPencilCase implements PencilCase {

		private Pencil pencil; // 연필 의존성
		private Eraser eraser; // 지우개 의존성
}
```

### 정적 의존성

코드를 보고 의존성을 쉽게 판단할 수 있는 의존 관계

### 동적 의존성

애플리케이션 실행 시점에서 어떤 객체의 생성된 인스턴스를 참조 변수에 연결하는 관계

e.g., 연필이 2B 연필 인지, HB 연필 인지는 실행 전까지 알 수 없다

```jsx
public class MetalPencilCase implements PencilCase {

		private Pencil pencil;

		// 동적 의존 관계에 대한 DI(의존성 주입)
		public MetalPencilCase(Pencil pencil) {
				this.pencil = pencil;
		}
}
```

### DI (의존성 주입)

애플리케이션 실행할 때, 외부에서 어떤 객체의 실제 인스턴스를 의존성으로 전달하여, 의존관계를 연결하는 것

→ 어떤 참조 변수에 실제 인스턴스를 주입

DI를 사용하면 클라이언트 코드를 변경하지 않고, 인스턴스 변경 가능

→ DI를 사용하면 정적 의존관계 변경 없이 동적 의존관계를 쉽게 변경 가능

### IoC 컨테이너 or DI 컨테이너

주입될(DI) 객체를 생성하고 관리하는 관리자

→ 프로그램의 흐름 주도와 제어를 관리하는 것

또는 어샘블러, 오브젝트 팩토리 등으로 불리기도 한다.


