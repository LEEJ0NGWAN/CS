[돌아가기](./README.md)

# 예외처리 (Exception handling)

예기치(예상치) 못한 상황에 대한 처리

# 오류

## Error

시스템 차원에서 발생하는 복구 불가능한 오류

e.g., StackOverflowError, XXXError ...

## Exception

애플리케이션 차원에서 발생하는 복구 가능한 오류

→ 예외 처리 상황에 따라서 프로그램 종료되지 않고 실행 재개 가능

e.g., NullPointerException, ArrayIndexOutOfBoundsException

# 예외 유형

컴파일러의 사전 예외 감지 여부에 따른 유형 분류 가능

### Checked Exception (확인된 예외)

- 예외 처리 강요됨
- IOException 계열의 예외 클래스들

### Unchecked Exception (미확인 예외)

- 예외 처리 선택적
- RuntimeException 계열의 예외 클래스들

# 예외 처리 방법

### try-catch-finally

예외를 직접 처리

- `try` 블록

    예외 발생 가능한 코드를 담는다

- `catch` 블록

    예외 발생 시 처리하는 로직을 담는다

    없어도 되고, 1개 이상 있어도 된다

- `finally` 블록

    예외 발생 여부 상관 없이 항상 실행할 로직을 담는다

    없어도 되고, 최대 1개까지 있어도 된다

    **`주의`**

    catch 내부에 return 으로 종료하는 부문이 있어도 finally 블록을 무조건 실행하고 return으로 간다

```
try {} 
catch (<ExceptionType> e) {} 
catch (<ExceptionType> e) {} 
...
finally {}

```

### try-with-resources

AutoCloseable를 구현하는 객체를 try 시작 파라매터로 설정하면,

finally 블록 같은 곳에서 굳이 close하지 않아도 try가 끝나면 자동으로 close 처리가 될 수 있다

```
try (BufferedReader br = new BufferedReader(new FileReader(src))) {
		...
} catch (Exception e) {
		...
}

```

### throws

- 예외를 caller에게 전달
- 메소드 선언부에 throws 키워드를 추가 한다

```
public static void main(String[] args) throws IOException {}

```

### throw

- 예외를 caller에게 전달
- 메소드 내부에서 throw 를 통해 예외 객체를 caller에게 전달한다

```
public static void main (String[] args) {

		foo();
}

public static void foo() {

		throw new IOException();
}

```

# 상황에 따른 예외 처리 방법

### 직접 예외 처리 o + 보고 x

→ try ~ catch (+ finally)

### 직접 예외 처리 o + 보고 o

→ try ~ catch + throw new <ExceptionType>();

### 직접 예외 처리 x + 보고 o

- 명시적 예외 전달

    throw new <ExceptionType>();

- 암묵적 예외 전달

    메소드 선언부에 예상 가능한 예외 throws 구문 추가

# Exception - method overriding

- 하위 클래스가 throws하는 예외는 상위 클래스가 throws하는 예외보다 범위가 같거나 작거나 없어야 한다
- 하위 클래스는 Runtime(Unchecked) 예외를 상위 클래스 상관 없이 throws 할 수 있다

### Access modifier - method overriding

- 하위 클래스에서 선언하는 접근 제어자는 상위 클래스에서 정의한 접근 제어자보다 범위가 크거나 같다

# Custom Exception

임의의 사용자 예외 생성 → Exception을 상속 받아 생성자 내부에서 super() 호출

```
public class MyException extends Exception {

		public MyException(String msg) {
				super(msg);
		}
}

```
