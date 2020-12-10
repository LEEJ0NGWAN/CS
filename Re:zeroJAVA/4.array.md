[돌아가기](README.md)

# 배열(array)

같은 타입의 여러 변수를 **연속된 메모리 공간**에 저장하는 선형 자료구조

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
    scores = new int[5];
    ```

- 배열의 선언과 동시에 생성

    ```jsx
    int[] scores = new int[5];
    ```

- 배열의 초기화 생성

    ```jsx
    int[] scores = { 100, 95, 90, 95, 85 };
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

`System.arraycopy()` 를 이용한다

→ 지정 범위의 값들을 한 번에 통째로 복사하기 때문에 비교적 빠른 복사 가능

System.arraycopy(복사할 배열, 복사 시작 인덱스, 붙여 넣을 배열, 붙여 넣기 시작 인덱스, 복사할 요소 개수)

```jsx
char[] abc = { 'a', 'b', 'c' };
char[] num = { '1', '2', '3', '4', '5', '6' };

// abc의 0번째부터 3개 요소를 복사해서 num의 0번째부터 붙여넣기
System.arraycopy(abc, 0, num, 0, abc.length);
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

→ 변경 가능한 문자열을 다루기 위해 `StringBuffer` 클래스를 사용해야 한다

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

# 다차원 배열

### 2차원 배열 선언

`타입`[][] `변수이름`;

`타입` `변수이름` [][];

`타입`[] `변수이름` [];

### 2차원 배열의 초기화

```jsx
int[][] arr = { {1,2,3}, {4,5,6} };
```

### 가변 배열

2차원 이상의 배열들은 내부 배열의 크기를 다양하게 적용할 수 있다

```jsx
int[][] arr = new int[3][];
arr[0] = new int[3];
arr[1] = new int[5];
arr[2] = new int[8];

// arr 배열의 할당된 공간 형태는 다음과 같다

// arr[0]: 0 0 0
// arr[1]: 0 0 0 0 0
// arr[2]: 0 0 0 0 0 0 0 0
```
