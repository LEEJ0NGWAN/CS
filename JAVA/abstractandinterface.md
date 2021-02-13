[돌아가기](./README.md)

# 추상클래스

미완성 설계도로, 상속을 통해 자식 클래스에서 구현하도록 유도하는 클래스

→ `new` 를 통해 인스턴스 생성 불가능

→ 추상메소드를 가진 클래스가 일반적인 의미

그러나, 추상 메소드가 없어도 추상 클래스로 선언할 수 있다

### 추상 메소드가 없는 추상 클래스가 가지는 의미

상속할 하위 타입에 대해, **선택적으로** 구현해야할 숙제를 남겨 놓는다 (Helper의 역할을 수행)

**선택적으로?**

→ 상속 받는 입장에서 구현하고 싶은 메소드는 선택적일 수 있다

만약, 모든 메소드가 추상 메소드라서 전부 구현하도록 강요받으면 곤란하다

```
abstact class Foo {

	public void a() {}
	public void b() {}
	public void c() {}
}

class A extends Foo {
	@Override
	public void a() {
		...
	}
}

class B extends Foo {
	@Override
	public void b() {
		...
	}
}

```

## 자식 클래스 입장

### 추상 메소드가 있는 경우

→ 반드시 재정의 해야 하는 책임이 생김 (자신 또한 추상 클래스가 되기 싫다면)

### 추상 메소드가 없는 경우

→ 선택적으로 재정의 할 수 있는 자유가 생김

# Adapter

하위 타입에서 필요한 메소드만 선택적으로 재정의할 수 있도록 기반이 되어 주는 추상 클래스

```
abstract class MyAdapter implements IA, IB, IC {

	public void ia() {}

	public void ib() {}

	public void ic() {}

}

```

# 인터페이스 vs 추상클래스

### 상태의 차이점

- 인터페이스

    stateless (필드는 전부 public statc final)

- 추상클래스

    non-static, non-final 가능 → stateful

### 상속의 차이점

- 인터페이스

    다중 상속

    클래스에서 다중 구현 가능→ public class C implements IA, IB, ...

    인터페이스끼리 다중 상속 가능→ public interface IC extends IA, IB, ...

- 추상 클래스

    단일 상속

### 접근 제어자 차이점

- 인터페이스

    public으로 한정됨

- 추상 클래스

    모든 접근 제어자 가능

**탬플릿 메소드 패턴에서 차이점**

- 인터페이스

    public으로 제한되어 있어, 탬플릿 메소드 내부에서만 동작할 hook 메소드가 public으로 노출될 가능성

- 추상클래스

    java는 단일 상속으로, 탬플릿 메소드 구현을 위해 추상클래스 상속하면, 다른 클래스 상속 불가능

### 사용 용도에서 차이점

- 인터페이스
    - 주로 has-a 관계에서 이용 (또는 is-a)
    - 구현 객체가 어떤 동작을 무조건 수행할 수 있다는 것을 보장하기 위해 사용
    - 동작의 구현 강제
- 추상클래스
    - 주로 is-a 관계에서 이용
    - 기능 확장에 초점을 둠
    - 여러 클래스의 공통점을 찾아 추상화 시켜 사용

# Tagging Interface

구현해야하는 동작을 기술하지 않았지만 객체가 어떤 성질이 있음을 나타내기 위해 사용하는 인터페이스

```
// Tagging Interface
public interface Curable { }

```

```
public class Marine extends Unit implements Attackable, Curable {
	...
}

```

```
public void heal(Curable unit) {
	unit.increaseHP(100); // 치료가능한 유닛의 체력 100 회복
}

```
