[돌아가기](./README.md)

# 다형성

다양한 형태를 가질 수 있는 성질

크게 봤을 때, 자바에서 실현한 다형성은 메소드 다형성과 타입 다형성으로 나눌 수 있다

## Method Polymorphism

같은 이름의 메소드가 다양한 동작을 하는 성질

→ Overloading과 Overriding 기술을 이용한다

### Overloading

어떤 메소드의 파라매터(변수의 개수, 타입, 순서)를 다르게 설정하여 여러 메소드를 만드는 것

```jsx
public void foo(int a) {}
public void foo(char a) {}
```

단, return 타입만 다르게 설정하는 것은 오버로딩이 아니며, 메소드 중복 선언 오류 발생

```jsx
public void foo(int a, int b) {}
public int foo(int a, int b) {} // 오류
```

### Overriding

상위 타입에 정의한 메소드를 하위 타입에서 재정의하는 것

```jsx
class A {
		public void foo() {}
}

class B extends A {

		@Override
		public void foo() {}
}
```

단, 재정의하는 메소드의 접근 제어자(visibility)는 기존 메소드의 접근 범위보다 크거나 같아야 한다

## Type Polymorphism

상위 타입 참조 변수에 다양한 하위 타입 객체 인스턴스를 참조하는 것

### 다른 참조변수, 같은 인스턴스

참조 변수 타입에 따라 같은 인스턴스의 사용 방법이 달라질 수 있다

```jsx
Object a = new Genesis(); // 해당 인스턴스는 Object 기능으로 제한됨
Car b = new Genesis(); // 해당 인스턴스는 Car 기능으로 제한됨
Genesis c = new Genesis(); // 해당 인스턴스는 Genesis 고유 기능 전부 사용 가능
```

### 같은 참조변수, 다른 인스턴스

하위 타입에 따라 같은 동작의 결과가 달라질 수 있다

단, 정확한 동작을 위해 하위 타입 인스턴스는 SOLID의 LSP(리스코프 치환 법칙)를 준수해야 한다

```jsx
Hamburger a = new BigMac();
Hamburger b = new Whopper();

a.favor(); // 빅맥 맛
b.favor(); // 와퍼 맛
```

# 다형성 사용 이유

OOP가 추구하는 개발(성능보다 유지보수와 높은 확장성 및 이식성 추구)을 실현하는 가장 강력한 특징이기 때문

### 유지보수 및 변경 용이

여러 하위 타입 객체 인스턴스를 하나의 상위 타입으로 관리할 수 있기 때문

### 높은 확장성과 낮은 결합도

상위 타입 참조 변수로 확장 또는 변경된 하위 타입을 참조할 수 있기 때문

### 코드의 유연성(코드의 재사용성)

메소드의 파라매터나 리턴을 상위 타입으로 지정한 후,

실제 다양한 하위 타입의 객체들로 유연하게 사용될 수 있기 때문

# 여러가지 다형성 활용

다형성을 통해 코드의 유연성(여러 상황에 대처 가능한 성질)이 증가한다

→ 이런 코드의 유연성은 관리하고 작성해야하는 코드의 길이를 줄일 수 있다 (다양한 타입에 대처 가능하기 때문)

### 이형 집합 다형성

다양한 하위 타입 객체를 하나의 컨테이너에 담는 것이 가능해진다

```jsx
Hamburger[] hamburgers = new Hamburger[5];

hamburgers[0] = new BigMac();
hamburgers[1] = new Whopper();
...
```

### 매개 변수 다형성

다양한 하위 타입 객체를 메소드 파라매터로 넘겨주는 것이 가능해진다

```jsx
public void eat (Hamburger hamburger) {
		// foo
}
```

```jsx
eat(new BigMac());
eat(new Whopper());
eat(new PsyBurger());
```

### 리턴 타입 다형성

다양한 하위 타입 객체를 리턴 해주는 것이 가능해진다

```jsx
public Hamburger getBurger(boolean isBigMac) {

		return (isBigMac)? new BigMac(): new Whopper();
}
```

# 자바에서 다형성이 가능한 이유

자바에서는 메소드 동적 바인딩을 이용하여, 하위 타입에서 재정의한 메소드를 상위 타입에서 호출할 수 있기 때문

## 메소드 동적 바인딩

컴파일 타임이 아닌, 런타임 동안 실행될 메소드가 바인딩 되는 것

→ 하위 타입에서 재정의된 메소드가 상위 타입에서도 호출 되는 이유는 메소드 동적 바인딩 때문이다

(단, 메소드에 대해서만 동적 바인딩이 이루어지기 때문에, 멤버 변수는 타입을 따른다)

```jsx
class A {
	int a = 10;

	public static int foo() {
		return a;
	}
}

class B extends A {
	int a = 20;

	public static int foo() {
		return a;
	}
}

A obj = new B();

obj.a;     // 10
obj.foo(); // 20
```
