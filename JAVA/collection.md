[돌아가기](./README.md)

# <> Generic

Collection을 포함하여, 객체를 담는 컨테이너 만들 때, 담는 객체의 타입을 다이나믹하게 지정하는 방법

```
public class GenericContainer<T> {

	private T object;
	public GenericContainer() {}
	public T getObject() {
		return object;
	}
	public void setObject(T t) {
		object = t;
	}
}

```

→ <>를 통해 들어올 수 있는 객체 타입의 가능성을 열어둔다

# Collections API

Array 보다 편리한 Container의 역할을 수행하는 자료구조 클래스 API

## Collection

Java에서 사용하는 자료구조

### List

순서 O, 중복 O, 인덱스로 관리

- Stack
- ArrayList
- LinkedList (implements List, Queue)

### Set

순서 X, 중복 X, 원소 자체 관리

- HashSet
- TreeSet

### Queue

순서 O, 중복 O

- LinkedList (implements List, Queue)
- PriorityQueue

## Map

순서 X, Key-Value pair 관리, Key 중복 X, Value 중복 O

### HashMap

### TreeMap

### HashTable

## 자주 사용하는 method

- add(E e): boolean
- remove(Object o): boolean
- isEmpty(): boolean
- clear(): void
- size(): int
- contains(Object o): boolean
- toArray(): Object[]
- iterator(): Iterator<E>

## <> generic을 사용하지 않으면

→ 디폴트로 Object 타입, 즉, 모든 객체를 컨테이너에 담을 수 있다

```
ArrayList list = new ArrayList();

```

그러나, 제네릭을 사용해야 컨테이너 객체의 타입을 제한하는 것을 통해 코드의 안정성을 보장할 수 있다

→ 불필요한 형변환 방지, 객체 추가 및 조회 등에서 코드가 수월해진다

# Iterator

iterator Interface를 구현하는 Collection 클래스 객체들에 대해,

Collection 각 객체를 순회할 수 있도록 메소드를 제공하는 클래스

### 기본 사용법

```
List<?> arrayList = new ArrayList<>();

...

Iterator<?> iter = arrayList.iterator();

```

### hasNext()

iterator가 순회할 원소가 아직 남아 있다면 true, 그렇지 않다면 false를 리턴

```
while (iter.hasNext()) {
	...
}

```

### next()

iterator가 가리키는 다음 원소를 리턴

```
Iterator<Integer> iter = integerList.iterator();

while (iter.hasNext()) {
	Integer num = iter.next();
	...
}

```

# Object.equals

Object의 기본 equals 연산은 `==` 로 주소값을 비교하는 연산이다

→ 특정 객체를 의미있게 비교하기 위해 재정의 요구됨

# HashSet

Set 컨테이너의 일종으로, 객체의 중복 여부를 List 컨테이너 계열보다 엄격하게 체크

→ Object.hashCode()를 이용해서 그 값이 같은 경우를 같은 객체로 인식

즉, 객체끼리 의미적으로 같더라도 hashCode가 다르기 때문에 다른 객체로 인식하고 중복 add

```
Set<Hamburger> set = new HashSet<>();

// 의미적 중복이나, hashCode가 다르므로 추가가 됨
Hamburger a = new BigMac();
Hamburger b = new BigMac();

set.add(a);
set.add(b); // a와 b 둘다 set에 추가됨

```

### 의미적 중복 방지

→ HashSet 컨테이너에 담을 객체 타입에서 hashCode를 재정의 (의미적 중복 방지하도록)

# PriorityQueue

Queue 컨테이너의 일종으로, compareTo() 메소드를 통한 우선순위 비교가 가능하다

이때, 우선순위 큐 컨테이너에 담을 객체 타입은 Comparable<?> 인터페이스를 구현해야 한다

→ 컨테이너 객체 타입에서 compareTo() 메소드 재정의 요구됨

```
public class McBurger extends Hamburger implements Comparable<McBurger> {

		private int size;

		@Override
		public int compareTo(McBurger m) {
				return this.size - m.size; // 결과 부호가 음수면 this가 앞, 양수면 m이 앞으로 정렬
		}
}

```

→ compareTo 메소드는  현재 가리키는 객체 기준으로 인자로 받는 다른 비교 대상 객체와 비교한다

return으로 음수가 반환되면 현재 가리키는 객체가 큐의 앞쪽,

양수가 반환되면 인자로 받는 비교 대상 객체가 큐의 앞쪽으로 정렬된다

즉, 현재 기준이 되는 객체 입장에서 결과가 음수면 자신이 왼쪽(앞)으로 가고, 양수면 자신이 오른쪽(뒤)으로 간다

### 정렬

이런 PriorityQueue에 객체를 삽입하면, 객체의 compareTo 메소드를 이용하여 정렬을 수행하게 된다

```
PriorityQueue<Hamburger> que = PriorityQueue<>();
que.add(new Hamburger(5000));
que.add(new Hamburger(2500));
que.add(new Hamburger(3200));

while(!que.isEmpty())
	System.out.println(que.poll());

// 오름차순
// 2500
// 3200
// 5000

```

# Collections.sort

List 컨테이너의 임의 정렬을 위해 제공되는 static method

```
static <T> void sort(List<T> list, Comparator<? super T> c)

```

### 비교를 위해 Anonymous class 이용

```
Collections.sort(list, new Comparator<T>() {

		@Override
		public int compare(T pivot, T target) {
				return pivot.getSomething() - target.getSomething();
		}
});

```

객체 pivot을 기준으로 return에 따라서 다음과 같이 정렬이 수행된다

- 음수 → pivot은 target의 앞
- 양수 → pivot은 target의 뒤
