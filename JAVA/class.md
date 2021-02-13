[돌아가기](./README.md)

# **OOP 특징**

### **Encapsulation**

데이터와 기능을 하나의 클래스 안에 정의 및 중요 데이터나 기능에 대한 정보 은닉 제공

### **Inheritance**

기존에 존재하던 객체의 속성과 기능을 상속받아 새로 정의하는 것

### **Polymorphism**

같은 타입 또는 같은 기능의 호출로 다양한 효과를 가져오는 것

### **(Abstraction)**

현실 세계에 존재하는 객체의 주요 특징을 추출하는 과정

# **Object**

시스템의 대상이 되는(표현할 수 있는) 모든 데이터

모든 Object는 구체적인 표현 대상 존재

- 속성 → 상태값
- 행위 → 동작, 기능

# 클래스

만들고자 하는 객체 인스턴스의 설정 정보를 정의하는 물리적인 파일

JVM이 Class를 참고하여금 인스턴스를 생성하도록 함

### **클래스 설계**

1. 다양한 현실 객체들에 대해, 어떤 기준을 바탕으로 클래스를 분류하는 작업 필요(클래스 분류; 객체 식별)
2. 식별한 객체에 대해, 정적인 특성(attribute)와 동적인 특성(behavior) 파악 필요

### **객체 후보군**

분류한 클래스에 대해, 채택될 가능성이 높은 객체

**객체 선택 방법**

- 명사기법 (객체, 객체 속성)
- CRC 기법(Class, Responsibility, Cooperation)
    - Class
    - Responsibility

        외부에 제공하는 기능(행위, 메소드..)

    - Cooperation

        다른 객체와의 의존관계

### **객체 생성**

`new` 키워드를 이용한 객체 생성자 호출

### **객체 생성자**

객체 생성 시 딱 1번 호출되는 클래스 이름과 같은 이름의 특수한 메소드

`Hamburger hamburger = new Hamburger();`

### **배열의 경우**

배열은 동형 집합의 특수한 객체로 클래스 정의 없이 배열 객체 생성 문법을 이용해서 객체 생성 가능

`int[] arr = new int[5]; //클래스 정의가 없다!`

JRE = JVM + API(재사용 가능한 자바 라이브러리 클래스)

# 생성자 (**Constructor)**

객체 생성 시 호출되는 특별한 메소드

- 커스텀 생성자 없다면, 컴파일러가 디폴트 생성자를 만듦
- 커스텀 생성자 있다면, 컴파일러가 디폴트 생성자를 안 만듦
- 클래스 이름과 같다
- 리턴 x
- 오버로딩 가능 (파라매터 타입과 개수, **배치 순서**를 다르게 설정)
- 상속 x (super를 통한 우회)

# 멤버 변수 (**Member variables)**

클래스 내부에서 객체의 상태를 표현하는 변수

- 객체 변수(non-static)
- 클래스 변수(static)

# 메소드 (**Method)**

- 객체 메소드(non-static)
- 클래스 메소드(static)

### **Setter**

변수의 값을 바꿀 수 있도록 제공하는 메소드

### **Getter**

변수의 값을 조회할 수 있도록 제공하는 메소드

### **이유**

Setter와 Getter 구조를 가져야만 이후 변화되는 처리 로직에 쉽게 대응 가능

의존 관계에 있는 객체들의 파급효과를 최소화 하기 위한 노력의 일환

# 내부 클래스 (**InnerClass)**

- 외부 클래스와 내부 클래스가 밀접한 관계가 있을 때
- 클래스를 은닉하고 싶을 때 (클래스는 내부 클래스만 private 키워드 가능)

### **innerclass에서 지정 가능한 키워드 비교**

- 일반 class → (default), public
- inner class → private, (default), protected, public + static

### **effective JAVA에서 inner class에 static 선언이 권장되는 이유**

외부 참조 장점에도 불구하고 더 치명적인 단점이 존재하기 때문

- non-static inner class의 this처럼 외부 참조가 존재하면 gc에서 메모리 회수 불가 → 메모리 누수
- 매번 외부 인스턴스 참조에 의존하게 되면 성능 상 비효율적이다

# **Static Initializer**

클래스가 JVM에 로드될 때 자동으로 최초 한번만 실행되는 블럭

→ 요긴하게 사용할 수 있다

```java
static {

}
```

### **Initializer**

인스턴스 생성 시 자동으로 매번 실행되는 블럭

→ 생성자가 거의 모든 역할을 하므로 잘 사용하지 않는다

```java
{

}
```

# **java.lang 패키지**

명시적으로 import 하지 않아도 기본적으로 제공되는 패키지로 import 처리가 되어 있음

→ System.out.println 같은 메소드

# **Access Modifier**

### **private**

클래스 내부에서만 접근 가능

### **(default)**

같은 패키지에서만 접근 가능

### **protected**

같은 패키지거나, 상속받은 클래스만 접근 가능

### **public**

외부 모든 곳에서 접근 가능

# **Instantiation**

### **클래스**

공통된 속성과 행위를 가지는 어떤 객체 종류를 일컫는 용어

→ 붕어빵 틀과 붕어빵 관계에서 클래스는 붕어빵 틀

### **인스턴스**

어떤 객체 종류의 각 개체를 지칭하는 용어

→ 붕어빵 틀과 붕어빵 관계에서 인스턴스는 붕어빵

# **메모리에 대해**

자바에서 논하는 메모리는 실제 물리적 자원 메모리를 뜻하는 것이 아니다

JVM이 운영체제로부터 할당 받아 소프트웨어적으로 관리되는 가상 메모리 공간을 뜻함

→ JVM은 주로 3가지 메모리 영역을 가지고 있음

### **Class Area(=Method area; Static area)**

클래스 및 패키지 정보, 메소드, 클래스 맴버(static)를 저장하는 메모리

### **Heap**

생성된 객체 인스턴스의 데이터를 저장하는 메모리

### **Stack**

메소드 호출 시 스택 프레임, 지역 변수 정보(원시 타입은 값, 참조 타입은 참조값)를 저장하는 메모리

→ 쓰레드 당 하나의 스택 메모리 공간이 할당 된다

# **클래스의 관계**

### **상속 관계 (is a; 일반화; generalization)**

상속 (일반화) 관계를 뜻한다

e.g., BigMac -▷ Hamburger

```java
public class BigMac extends Hamburger {
		...
}
```

### **연관 관계 (의존 관계; has a; 영속적; association)**

영구적 소유 관계를 뜻한다

→ 맴버 변수로 표현

- 집합 연관 관계 (전체 부분을 나타내는 관계; aggregation)

    e.g., BookManager ◇- Book

- 복합 연관 관계 (생명 주기가 같은 관계; composition)

    e.g., Tree ◆- Leaf

e.g., SetMenu → Hamburger

```java
public class SetMenu {

		private Hamburger hamburger;

		public SetMenu(Hamburger hamburger) {
				this.hamburger = hamburger; // 연관 관계
		}
}
```

### **사용 관계 (use a; 일시적; dependency)**

일시적 소유 관계를 뜻한다

→ 지역 변수로 표현

e.g., Lion ⁃⁃⁃> Claw

```java
public class Lion extends Animal {

		public void attack() {

				Claw claw = new claw();  // 의존 관계

				...
		}

}
```

# **디자인 패턴**

목적을 달성하기 위해 정형화 시킨 전형적인 설계 방법

# **Singleton Design Pattern**

객체를 1개만 생성해서 사용하는 패턴

→ 접근 제어자와 getter를 이용한다

### **private 생성자**

private 키워드를 이용하여 스스로 인스턴스를 1번만 생성하도록 설정한다

```java
public class BookManager {
		private BookManager() {}
}
```

### **클래스 내부 객체 생성**

클래스 내부에서 딱 1번 객체를 생성 후 참조값을 저장

→ static 이용

```java
public class BookManager {
		private static BookManager instance = new BookManager();

		private BookManager() {}
}
```

class area의 참조변수 instance는 힙 메모리에 생성된 BookManager 인스턴스의 참조 값을 저장

### **외부 리턴 getter**

외부에서 해당 싱글톤 패턴 인스턴스의 참조 값을 사용하도록 getter 메소드 생성

```java
public class BookManager {

		private static BookManager instance = new BookManager();

		private BookManager() {}

		public static BookManager getInstance() {
				return instance;
		}
}
```

→ BookManager.getInstance() : BookManager
