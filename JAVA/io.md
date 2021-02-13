[돌아가기](./README.md)

# java.util.Scanner

편리한 입출력을 위해 자바에서 제공하는 API

다양한 타입으로 파싱하여 데이터를 제공하는 편리한 기능을 제공하지만, 성능 상 불리하다

```java
import java.util.Scanner;

class Test {

	public static void main(String[] args) {
		Scanner s = new Scanner(System.in);

		int x = s.nextInt();
		String str = s.nextLine();
		...
	}
}
```

# java.io.BufferedReader

IOException 처리 및 파싱을 사용자가 처리해야하지만 빠른 성능을 가질 수 있다

→ BufferedReader 차원에서 입력 노드의 데이터를 한번에 많은 양을 가져와 버퍼에 보관하는 것을 통해 전체적인 입력 횟수를 줄이는 것에 의의를 두고 있다

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

class Test {

	static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

	public static void main(String[] args) throws Exception {

		String s = br.readLine();
		...
	}
}
```

# java.io.BufferedWriter

BufferedWriter 차원에서 출력 노드에 한번에 많은 양의 데이터를 쓰기 위해 버퍼에 보관하는 것을 통해 전체적인 출력 횟수를 줄이는 것에 의의를 두고 있다

```java
import java.io.BufferedWriter;
import java.io.OutputStreamWriter;

class Test {

	static BufferedWriter bw
		= new BufferedWriter(new OutputStreamWriter(System.out));

	public static void main(String[] args) {

		String s1 = "play";
		String s2 = "game";

		bw.write(s1);
		bw.write(s2);
		bw.flush(); // 버퍼에 저장된 데이터 한번에 출력 노드로 출력
	}
}
```

# **Stream**

자바와 외부 세계에 오고 가는 데이터의 흐름을 추상적으로 부르는 말

### **단방향**

Stream은 단방향의 성질을 가진다

- 입력 스트림

    외부에서 자바로 데이터를 읽어들이는 스트림

- 출력 스트림

    자바에서 외부로 데이터를 내보내는 스트림

### **데이터 단위**

스트림에 전송되는 데이터의 단위는 바이트 또는 캐릭터로 구성

- byte

    InputStream, OutputStream

- character

    Reader, Writer

## **노드 스트림**

입/출력 대상 노드에 직접 맞물리는 기본 스트림 → 필수

데이터를 주고 받는 단말 노드(외부 입출력 발생 지점; 키보드라던가..파일이라던가..)에 직접 장착이 된다

e.g., [System.in](http://system.in/)

## **필터 스트림(프로세싱 스트림)**

부가적인 목적의 기능 추가하는 선택 스트림 → 선택적

노드 스트림에 부가적 기능 및 필터링을 제공하는 고수준의 스트림

노드 스트림을 인자로 입력 받아 부착된다

e.g., BufferedReader, InputStreamReader

### **노드 + 필터(프로세싱) 스트림 예시**

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
```

## **표준 스트림**

JVM이 실행되면 자동으로 열리는 기본 Stream

- System.in
- System.out
- System.err

### **System.setIn();**

표준 입력 스트림의 source를 바꿀 수 있다

# 객체 직렬화

객체의 상태 값(인스턴스의 변수)을 일렬로 나열하며 바이트로 쓰는 작업

→ 객체 단위로 읽고 쓰기 위한 수단으로써 필요

직렬화 하고자 하는 객체는 태깅 인터페이스 Serializable을 구현한다

### ObjectInputStream/ObjectOutputStream

입/출력 데이터를 객체 단위로 처리하는 필터 스트림

- readObject():Object o
- writeObject(Object o)

## 객체 역직렬화

직렬화(parsing)된 객체의 상태값을 기반으로 바이트를 읽어 들여 객체로 복원시키는 작업

→ 객체 인스턴스의 상태값과 메타 정보 등을 읽어들여 객체 인스턴스를 생성

### 주의 사항

- 객체 자체가 직렬화/역직렬화 되는 것이 아니라, 객체의 상태 값을 토대로 인스턴스를 재구성하는것이다
- Serializable 객체 내부에 어떤 의존 객체가 Serializable이 아니면 직렬화를 할 수 없다
- 상위 타입이 Serializable 일 때, Serializable 구현 없이 하위 타입도 직렬화 가능
- readObject()로 재구성한 인스턴스는 원하는 특정 하위 타입으로 형변환을 취해야 함
