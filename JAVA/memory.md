[돌아가기](./README.md)

# 메모리

애플리케이션이 구동을 하기 위해서, 데이터와 명령어를 저장할 공간 메모리가 필요

→ OS는 컴퓨터 자원(메모리; RAM)을 애플리케이션이 사용할 수 있도록 할당

### 메모리 관리

OS로부터 할당 받은 메모리를 관리하는 것에 따라 성능이 좌우 됨

### 메모리 할당

OS로부터 할당 받은 메모리는 크게 4가지(코드 실행 영역, static 영역, stack 영역, heap 영역)로 나뉨

→ T 메모리 영역 = static + stack + heap

# T 메모리 영역

## static 영역 (= class area; method area)

**패키지 정보**, **클래스 정보**, **메소드**, **클래스 전역 변수(static이 붙은 자료형)**를 저장하는 메모리 영역

- JVM 시작부터 종료까지 메모리에 유지 (Static 명칭 이유)
- 무분별 사용을 권장하지 않음
- 정적 변수는 초기화 생략 가능
- 메소드는 static 키워드 여부 상관 없이 static 영역에 저장

```jsx
public class Static {

	static int x;
	static String y;

	void foo() {} // 메소드는 static 영역에 저장

}
```

## stack 영역

**스택 프레임**과 **지역 변수**가 저장되는 메모리 영역

- `{` 마다 스택 프레임 생성하고, `}` 마다 스택 프레임 제거 (메소드, if, for 등에서 사용하는 블록)

    → 블록 단위의 스택 프레임 생성

    → 스택 프레임 제거될 때 해당 프레임 내부의 지역 변수 같이 제거

- 외부 스택 프레임은 내부 스택 프레임의 지역 변수 사용 불가능
- 내부 스택 프레임은 외부 스택 프레임의 지역 변수 사용 가능
- 원시 타입 지역 변수의 경우, 값이 stack에 저장
- 참조 타입 지역 변수의 경우, 참조값이 stack에 저장
(참조 변수의 인스턴스 데이터는 heap에 저장)
- 메소드 호출 시 스택 메모리 할당 및 메소드 종료 시 메모리 해제
- 메소드의 지역 변수는 초기화 필요
- 각 쓰레드는 개인 stack 영역 소유 → static 영역과 heap 영역을 쓰레드끼리 공유

    (멀티 프로세스보다 멀티 쓰레드가 메모리 절약되는 이유)

```jsx
public class Stack {

	public static void main(String[] args) {
		int x = 5;
		for (int i = 0; i < 5; i++);
	}

}
```

## heap 영역

참조 변수(객체)의 **인스턴스** 및 **배열**을 저장하는 메모리 영역

- **참조 변수의 메모리 구성**
    - stack 영역

        참조 변수가 가리키는 인스턴스 데이터의 주소와 연결된 참조값(Hash code)을 저장

    - heap 영역

        참조 변수가 가리키는 인스턴스 데이터를 저장

- GC는 주기적으로 어떤 참조 변수도 참조하지 않는 heap 영역의 인스턴스 메모리를 정리
- 하위 타입(상속) 인스턴스 생성 시, 상위 타입(최상단 Object까지) 인스턴스들도 같이 생성

```jsx
public class Heap {

	public static void main(String[] args) {
		int[] arr; // int 배열 선언 및 stack 메모리 할당
		arr = new int[5]; // 5개 연속 공간 heap 메모리 할당 및 arr에 참조값 할당
		Hamburger hambuger; // hamburger 객체 stack 메모리 할당
		hamburger = new BigMac(); // BigMac 인스턴스 heap 메모리 할당 및 참조값 할당
	}
}
```
