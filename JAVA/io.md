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

입출력의 기초가 되는 저수준의 스트림

데이터를 주고 받는 단말 노드(외부 입출력 발생 지점; 키보드라던가..파일이라던가..)에 직접 장착이 된다

e.g., [System.in](http://system.in/)

## **필터 스트림(프로세싱 스트림)**

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
