[돌아가기](./README.md)

# Enum

어떤 연관성을 가진 정보를 나열하기 위해 사용하는 class

내부에 선언된 열거 상수들은 각각 내부적으로 `public static final` 필드인 것과 동시에 객체로 제공된다

→ static 이기 때문에, 클래스 로더가 해당 enum 로드 시점에 JVM static memory(method area)에 해당 열거 상수들(클래스 변수)의 주소 공간을 확보 (단, 호출 전까지 힙 메모리에 인스턴스 할당 x)

```jsx
public enum GenderType {
	Male, Female
}
```

enum은 class를 상속 받았기 때문에, 파라매터로 넘겨주는 등 다양한 방식으로 사용할 수 있는 장점이 있다

```jsx
public class Person {

	private String name;
	private GenderType gender;

	public Person (String name, GenderType gender) {
		this.name = name;
		this.gender = gender;
	}
}
```

# 메모리 초기화

클래스처럼 `new` 키워드를 사용하지 않지만, 

참조 되기 시작하면 힙 메모리에 java.lang.Enum 클래스를 상속 받는 고유 객체 인스턴스를 생성

(이때, 모든 열거 상수들의 인스턴스가 일괄 생성된다)

```jsx
GenderType gender = GenderType.Female; // 힙 영역에 Male, Female 인스턴스 생성
```

인스턴스 생성 후, 기존 static 영역에 할당한 열거 상수들의 참조 변수에 해당 인스턴스들의 참조값 자동 할당

# 장점

- 문자열과 비교하기 때문에, IDE의 적극적인 지원을 얻을 수 있다

    → 자동완성, 오타검증, 텍스트 리팩토링..

- 허용 가능한 값을 제한
- 리팩토링 시 변경이 필요한 범위의 최소화

    → 내용의 추가가 있더라도, Enum 이외 코드 수정 필요 x

# Method

### name(): String

열거 상수의 String 파싱을 리턴

```jsx
GenderType.Male.name(); // Male
```

### ordinal(): int

열거 상수의 위치 인덱스 값 리턴

```jsx
GenderType.Female.ordinal(); // 1
```

### compareTo(): int

열거 상수의 상대 위치 값 리턴 (-1은 왼쪽, 0은 같은 값, 1은 오른쪽을 나타냄)

```jsx
GenderType.Male.compareTo(GenderType.Female); // -1
GenderType.Male.compareTo(GenderType.Male); // 0
GenderType.Female.compareTo(GenderType.Male); // 1
```

### valueOf(String): Enum

입력 스트링과 일치하는 열거상수 리턴

```jsx
GenderType.valueOf("Male"); // GenderType Male
```

### values(): Enum[]

열거상수 배열 리턴

```jsx
GenderType.values(); // GenderType[]
```

# 추가 메서드

enum 내부에 메서드 선언 가능

```jsx
public enum GenderType {
	MALE, FEMALE

	public void print() {
		System.out.println("성별: "+this);
	}
}

GenderType.MALE.print(); // 성별: MALE
```

# 추가 속성과 생성자

Enum은 클래스이기 때문에 속성을 추가하여 커스텀 생성자 선언가능

→ 단, enum은 고정된 상수의 집합이기 때문에 컴파일 시 값을 가지기 위해 private으로 선언

```jsx
public enum Color {

	R("빨강",255,0,0), G("초록",0,255,0), B("파랑",0,0,255);

	private String name;
	private int r, g, b;

	private Color (String name, int r, int g, int b) {
		this.name = name;
		this.r = r;
		this.g = g;
		this.b = b;
	}
}
```

# 메소드 오버라이딩

```jsx
public enum Gender {

	MALE {
		@Override
		public void print() {
			System.out.println("나는 남자야");
		}
	},
	FEMALE {
		@Override
		public void print() {
			System.out.println("난 여자");
		}
	};

	public abstract void print();
}

Gender.MALE.print();    // 나는 남자야
Gender.FEMALE.print();  // 난 여자
```
