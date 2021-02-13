[돌아가기](./README.md)

# 배열(array)

같은 type의 여러 변수를 연속된 메모리 공간에 저장하여 인덱스로 접근하는 객체

→ 동형 집합(Homogeneous Collection)의 객체

배열도 객체로 힙 메모리에 인스턴스가 생성되고, 스택 메모리에 참조 값을 저장한다

- 객체이므로 new를 이용한 객체 생성 필요
- 크기 고정 (불변)
- 고정된 크기의 자료구조 중에서 가장 빠름 (콜렉션 프레임워크 컨테이너 보다 시간적 유리)

### **배열 종류**

- 원시타입 배열

    배열의 원소가 원시 값

- 참조타입 배열

    배열의 원소가 참조 값

### **Array 없다면**

- 동일 type의 변수 개수와 코드 길이가 증가
- 반복문 적용 및 일괄처리 불가능
- 변수 개수가 동적으로 결정될 경우 사용 불가능

### **Array 장점**

- 변수 개수 감소
- 코드 길이 감소
- 반복문 적용 가능
- 변수 개수가 동적으로 결정될 경우 사용 가능

### **ArrayConstant**

중괄호 {} 를 이용하여 원소 값을 할당한다 → 초기화에만 사용 가능

```jsx
int[] dx =  { 1, 0, -1, 0 }; // ArrayConstant; 초기 배열 생성에만 사용가능
```

# **Local Variables vs Array in Memory**

### **local variables (stack)**

원시타입 지역 변수의 값이 스택에 저장되거나, 객체 타입 변수의 참조값이 스택에 저장

### **array (stack + heap)**

배열의 참조값이 스택에 저장되고, 해당 참조값이 가리키는 메모리 주소로 따라가면

힙 메모리 영역에 배열의 원소값 저장

# 배열의 생성

배열의 선언과 생성으로 이루어짐

- 배열의 선언

    생성될 배열을 다루기 위한 참조변수를 생성

    ```jsx
    // 타입[] 이름;
    int[] scores;
    ```

- 배열의 생성

    실제 같은 타입의 변수들을 연속해서 저장할 배열을 생성

    ```jsx
    // 변수이름 = new 타입[길이];
    scores = new int[5]; // 힙 메모리에 int 타입 배열 객체 인스턴스 생성
    ```

- 배열의 선언과 동시에 생성

    ```jsx
    int[] scores = new int[5]; // 참조 변수 생성 및 객체 인스턴스 생성
    ```

- 배열의 초기화 생성

    ```jsx
    int[] scores = { 100, 95, 90, 95, 85 }; // ArrayConstant
    ```

# 배열의 길이와 인덱스

### 요소(element)

배열의 각 저장공간 및 그 저장 공간에 저장된 변수

### 인덱스(index)

배열의 요소마다 붙여진 일련번호로 0부터 (배열의 길이-1) 까지의 정수를 가짐

e.g., 배열의 길이가 4일 때, 0부터 3까지의 인덱스가 존재

```jsx
int[] scores = int[4];
scores[0] = 90;
scores[1] = 85;
scores[2] = 95;
scores[3] = 90;
```

### 배열의 길이

각 배열의 `length` 라는 속성은 해당 배열의 길이 정보를 포함한다

```jsx
int[] scores = int[5];
int length = scores.length; // scores의 길이는 5
```

### 배열의 길이 변경

배열은 정적인 자료구조로 한번 정해진 메모리 공간을 유연하게 변경할 수 없다

→ 메모리 공간의 크기가 다른, 새로운 배열을 생성하고 그 배열로 대체

길이 변경 작업은 비용이 많이 들기 때문에, 가급적이면 길이 변경 작업이 일어나지 않도록 처음부터 적당한 길이를 설정해야 한다

# 배열의 복사

### System.arrayCopy()

→ 지정 범위의 값들을 한 번에 통째로 복사하기 때문에 비교적 빠른 복사 가능

System.arraycopy(복사할 배열, 복사 시작 인덱스, 붙여 넣을 배열, 붙여 넣기 시작 인덱스, 복사할 요소 개수)

```jsx
char[] abc = { 'a', 'b', 'c' };
char[] num = { '1', '2', '3', '4', '5', '6' };

// abc의 0번째부터 3개 요소를 복사해서 num의 0번째부터 붙여넣기
System.arraycopy(abc, 0, num, 0, abc.length);
```

### Arrays.copyOf(arr, length), Arrays.copyOfRange(arr, index, length)

```jsx
int[] arr1 = {1,2,3,4};
int[] arr2 = Arrays.copyOf(arr,2); // arr2 = {1,2};
int[] arr3 = Arrays.copyOfRange(arr,2,1); // arr3 = {3};
```

# String 배열

String 타입의 여러 변수를 연속으로 저장하는 배열

```jsx
String[] name = new String[3];
name[0] = "Kim";
name[1] = "Lee";
name[2] = "Park";
```

```jsx
String[] name = { "Kim", "Lee", "Park" };
```

# char 배열 vs String 클래스의 차이점

### char 배열

- 단순히 char 타입의 변수를 저장한 배열
- 내용을 변경할 수 있다

### String 클래스

- char 배열에 기능(method)를 추가한 클래스
- 내용의 변경이 불가능하고, 읽는 것만 가능(새로 생성되는 문자열을 다시 가리키는 식으로 동작)

→ 변경 가능한 문자열을 다루기 위해 `StringBuilder` 또는 `StringBuffer` 클래스를 사용해야 한다

# **String vs StringBuilder vs StringBuffer**

### **String**

String은 문자열 상수로 한번 생성되면 문자열 조작 불가능

→ 변경이 필요한 경우, 새로운 String 객체로 concat 방식 필요(비효율적)

### **StringBuilder**

변경 가능한 문자열을 조작하는 객체

- 동기화 지원 X
- 단일 쓰레드에서 성능 상 유리

### **StringBuffer**

변경 가능한 문자열을 조작하는 객체

- 동기화 지원
- 멀티 쓰레드에서 안전성 보장

# String 클래스의 주요 method

- char charAt(int index);

    특정 index에 위치한 문자를 반환

- int length();

    String의 길이를 반환

- String substring(int from, int to);

    from 인덱스 부터 to 인덱스까지의 부분 문자열로 구성된 String을 반환

- boolean equals(Object obj);

    String이 나타내는 문자열의 내용과 obj의 내용이 같은지 확인

- char[] toCharArray();

    String이 나타내는 문자열을 char의 배열로 반환

### char 배열과 String 클래스의 변환

```jsx
char[] arr = { 'a', 'b', 'c' };
String str = new String(arr);   // char 배열 -> String
char[] tmp = str.toCharArray(); // String -> char 배열
```

## **다 차원 배열 효과**

의존 관계를 가지는 어떤 객체에 대한 배열을 만들 때, 다차원 배열과 같은 효과를 가질 수 있음

```jsx
class SetMenu {
	private Hamburger hamburger; // 햄버거 의존성
	private SideMenu sidemenu; // 사이드 메뉴 의존성
	private Drink drink; // 음료 의존성

	// DI
	public SetMenu (...) { }
}

public MenuService {
	public static void main(String[] args) {
		Setmenu[] menus = new SetMenu[10]; // 10개의 세트 매뉴 생성으로 2차원 배열 효과
		for (int i = 0; i < 10; i++)
	    menus[i] = new SetMenu(new Hamburger(), new Drink());
	}
}
```

# **다차원 배열**

array of array로써, 원소로 다른 배열을 참조하는 값을 가지는 참조 타입 배열

```jsx
int[] a1, a2[], a3[][]; // 1차원, 2차원, 3차원 배열

// a1의 원소 타입 = int
// a2의 원소 타입 = int[]
// a3의 원소 타입 = int[][]
```

→ 자바에서 배열은 객체이기 때문에 다차원 배열 구성 시, 내부 배열의 길이는 전부 달라도 상관 X

### 2차원 배열 선언

`타입`[][] `변수이름`;

`타입` `변수이름` [][];

`타입`[] `변수이름` [];

### 2차원 배열의 초기화

```jsx
int[][] arr = { {1,2,3}, {4,5,6} };
```

### **부분 배열 크기 생략**

- 부분 배열 크기가 다를 때

```jsx
int[][] arr = new int[2][];
arr[0] = new int[4];
arr[1] = new int[3];
```

- 부분 배열 모아 배열 생성

```jsx
int[][] arr = new int[2][];
for (int i = 0; i < arr.length; i++)
		arr[i] = new int[3];
```

****foreach****
배열 또는 Iterable 객체의 원소를 하나씩 꺼내어 반복하는 구문

```jsx
int[] arr = {0, 1, 2, 3, 4};
for (int e : arr)
	System.out.print(e);
```
