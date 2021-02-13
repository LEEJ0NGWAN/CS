[돌아가기](./README.md)

# 멤버 변수 vs 지역 변수

### 멤버 변수

→ 자동 초기화가 이루어짐

### 지역 변수

→ 선언 후 직접 초기화를 하지 않으면 사용할 수 없다

# 연산자

### 쉬프트 연산자

쉬프트 연산은 가장 빠르게 수행할 수 있는 비트 단위 연산

- `>>`

    쉬프트 후 빈 공간 부호비트로 초기화

- `>>>`

    쉬프트 후 빈 공간 0으로 초기화

### 삼항 연산자

- C/C++ 계열과는 달리 statement로써 사용 불가능
- 무조건 변수 값 대입을 위한 expression만 사용 가능

```
(true)? System.out.println("쫑왠"): System.out.println("쭈꾸미"); // Java에서 불가능

String name = (true)? "쫑왠": "쭈꾸미"; // 정상 동작

```

### 증감 연산자

무조건 별도의 계산이 없는 어떤 하나의 변수에 대해서만 증감 연산자 가능

```
int i = 2;
++(i-2);  // ERROR!
(i+2)++;  // ERROR!
++i; // 정상 동작

```

### 비교 연산자

- &&, ||

    첫 조건 검사를 만족하지 못하면 나머지 조건문은 그냥 무시하고 건너뜀

```
int a = 0, b = 0;
if (a++ != 0 && b++ == 0)
		System.out.println("hi");

System.out.println(a); // 1
System.out.println(b); // 0

```

- &, |

    java에서는 연산 대상으로 boolean이 들어오면 &&, || 처럼 비교 연산을 수행하게 되는데,

    &&, || 와 달리 첫 조건 검사를 만족하지 못해도 나머지 조건문도 끝까지 검사

```
int a = 0, b = 0;
if (a++ != 0 && b++ == 0)
		System.out.println("hi");

System.out.println(a); // 1
System.out.println(b); // 1

```

# switch

→ `byte`, `short`, `char`, `int`, `String` 만 case 변수로 사용 가능

# 메소드 동적 바인딩

상위 타입 참조변수로 하위 타입 객체를 참조할 때

- 메소드

    오버라이딩 된 하위 타입의 메소드 호출

- 멤버변수

    상위 타입의 멤버변수 사용

```
class A {
	int a = 10;
	public int foo() {
		return a;
	}
}

class B extends A {
	int a = 10;
	public int foo() {
		return a;
}

A a = new B();

a.foo() // 20;
a.a     // 10;

```

# 오버라이딩

- 부모 메소드 static & 자식 메소드 static

    되긴 되던데, 정말 오버라이딩일까?

    → 노노! 오버라이딩은 런타임에 자식 인스턴스의 메소드로 동적 바인딩하는 것으로,

    애초에 staic 메소드는 컴파일 시점에서 부모의 static 메소드를 hiding하고, 자식의 메소드를 호출한다.

    즉, "런타임 시점"에서 바인딩 되는 것이 아니기 때문에, static 메소드끼리는 오버라이딩 된 것이 아니다.

- 부모 메소드 static & 자식 메소드 non-static

    → 오버라이딩 불가능

- 부모 메소드 non-static & 자식 메소드 static

    → 오버라이딩 불가능

# 오버로딩

- 매개변수 완전 똑같고 리턴 타입만 다를 때

    → 오버로딩 아니고 그냥 오류임

- 매개변수 다르고 리턴타입 다를 때

    → 오버로딩 인정

# 상속 범위

### 오버라이딩 접근 제어자 범위

부모 접근 제어자 ≤ 자식 접근 제어자

### 오버라이딩 throws 범위

부모 throws ≥ 자식 throws (아예 없어도 됨)

# try-catch-finally

### catch vs finally

catch 에서 return으로 빠져나가는 구문이 있더라도 무조건 finally를 실행하고 return 됨

### 중복 catch

catch 블록이 여러개 있다면, 제일 범주가 큰 Exception을 밑으로 해야함 (안그러면 컴파일 에러)

# 생성자

### 디폴트 생성자

자식 생성자에서 명시적으로 부모 생성자를 호출하지 않으면 부모의 "디폴트" 생성자를 자동호출

→ 부모에 디폴트 생성자가 없다면 오류가 발생한다

### this

this를 통해 자신의 오버로딩된 다른 생성자 호출 가능

단, 생성자 내부에서 맨 앞에 선언해야 함 (super와 같이 사용 x)

### super

super를 통해 부모의 생성자를 명시적으로 호출

단, 생성자 내부에서 맨 앞에 선언해야 함 (this와 같이 사용 x)

# java.lang

명시적 import 가 없어도 자동으로 불러오는 패키지

### java.lang.Object

모든 객체의 최상위 타입

→ toString() 메소드를 가지고 있다 (디폴트 출력은 클래스 이름 + @해쉬코드)

# String

new 없이 선언한 String은 힙 메모리의 스트링 풀에 생성

String은 변경이 불가능 → concat과 같은 변경 연산은 사실 새로운 String을 생성하여 반환하는 것

# StringBuffer StringBuilder

둘 다 가변적 문자열을 생성할 때 사용

### StringBuffer

동기화 O, 다중 쓰레드 환경에서 동기화 지원

### StringBuilder

동기화 X, 단인 쓰레드 환경에서 높은 성능 제공

# Collection

### List

순서 O, 중복 O

### Set

순서 X, 중복 X

# Map

순서 X, 키 중복 X, 값 중복 O

→ null 도 키로 받을 수 있다

# Hash Series

HashMap, HashSet 처럼 Hash가 붙은 자료구조들은 `equals`, `hashCode`를 이용하여 키 중복 여부를 검사

→ 즉, `equals`, `hashCode` 둘 다 동일해야 완전히 같은 키로 인식

# Stream

### 바이트

InputStream,OutputStream

### 캐릭터

Reader, Writer

# Integer Pool

Wrapper 클래스 Integer는 -127 ~ 128 까지 정수를 캐싱하는 풀을 가지고 있다

→ 즉, -127~128 까지 정수는 명시적 new Integer(int) (java9 부터 deprecated)가 없는 이상 새로운 Integer 인스턴스를 생성하지 않음

# 소수의 연산 결과는 부정확하다

### (0.1 * 3) ≠ 0.3

소수의 연산 결과는 명시적으로 선언된 어떤 소수와 결과가 같지 않다고 판단

### 0.30000 == 0.3

이것은 걍 같더라;;

# initializer와 클래스 생성자 실행 순서

static initializer → 생성자 내부 super → 클래스 내부 instance initializer → 생성자 나머지 내용

# length vs length()

배열의 경우 길이는 멤버 변수 length

String의 경우 길이는 메소드 length()
