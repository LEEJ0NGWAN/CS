[돌아가기](./README.md)

# Lambda (람다)

Functional Interface(함수형 인터페이스)의 인스턴스를 생성하는 표현식

이름이 없는 함수의 형태로, 메소드의 인자 또는 리턴값으로 대입하거나, 변수에 저장하는 일급 객체로 활용 가능

→ 식처럼 보이지만, 실제는 함수형 인터페이스의 구현체 인스턴스가 만들어진다

## 기본 구성

```jsx
(Hamburgur b1, Hamburger b2)->b1.equals(b2)
```

- 인자

    함수 인자로 넘겨줄 변수를 괄호로 감싼다

- 화살표

    함수의 인자와 리턴 바디를 구분

- 바디

    람다의 리턴 값에 해당되는 표현식

## 여러가지 예시

```jsx
b->b.getPrice()>200; //타입 추측형 파라매터 변수 람다

()->new Hamburger(); //파라매터가 없는 람다

(Hamburger b)->{System.out.println("yummy");} //타입 선언형 파라매터 변수 람다

(int x, int y)->x-y // int return 람다
(x,y)->x+y // 타입 추측형 다중 파라매터 변수 람다

// Complex 바디의 람다
() -> {
	System.gc();
	System.out.println("gc");
	return true;
}

()->{}   // void 리턴 람다
()->null // expression 람다
()->6400 // expression 람다
```

# Functional Interface (함수형 인터페이스)

(Object 클래스의 메소드를 제외하고) 구현해야 하는 추상 메소드가 단 하나만 정의된 인터페이스

- 메소드를 일급 객체(First-class citizen)로 사용할 수 없는 자바의 단점을 보완하기 위해 Java8에 도입
- 함수형 인터페이스의 구현체도 결국 Object의 하위타입이기 때문에, Object 메소드를 가짐

### 일급 객체

다른 객체에 적용가능한 연산을 모두 지원하는 객체

일급 객체가 지원하는 연산

- 변수의 값으로 할당
- 객체 또는 어떤 함수의 인자로 대입
- 객체 또는 어떤 함수의 리턴값으로 반환

## @FunctionalInterface

개발자가 작성한 인터페이스가 Functional Interface인지 확인하는 용도의 인터페이스

→ 작성 인터페이스가 Functional Interface 인지 엄격한 검증을 원할 때 사용

# 람다와 함수형 인터페이스

람다식의 평가(해당 코드를 람다 인식) 후, Functional Interface의 인스턴스(구현체)를 생성

→ 즉, 선언된 람다는 함수처럼 보이지만, 실제로는 인터페이스를 구현한 익명 클래스의 객체 인스턴스

### 람다를 이용한 계산기 예시

```jsx
@FunctionalInterface
public interface Operator {
	public int op(int a, int b);
}
```

```jsx
public class Calculator {

	public static int cal(int a, int b, Operator op) {
		return op.op(a,b);
	}

	public static void main(String[] args) {

		int x = 2, y = 3;

		int addResult = Caculator.cal(x,y,(x,y)->x+y); // 5
		int subResult = Caculator.cal(x,y,(x,y)->x-y); // -1
		int mulResult = Caculator.cal(x,y,(x,y)->x*y); // 6
		int divResult = Cacularot.cal(x,y,(x,y)->x/y); // 0
	}
}
```

# Functional Package

### Consumer<T>

- accept(T):void
- 입력된 T type 데이터에 별도의 리턴 없이 어떤 작업을 수행
- 또는 call by reference를 통해, 입력 데이터 내부 속성 변경

```jsx
Consumer<int[]> arrInitializer = 
	arr->{for(int i=0, l=arr.length; i<l; i++)arr[i]=0;};

arrInitializer.accept(new int[]{1,2,3,4,5}); // 0,0,0,0,0
```

### Function<T, R>

- apply(T):R
- 입력된 T type 데이터에 일련의 작업 수행 후 R type 데이터 반환
- 입력된 데이터 변경도 가능

```jsx
Function<String,NPC> npcMaker = name->new NPC(name);

npcMaker.apply("이종완"); // new NPC
npcMaker.apply("쫑왠");  // new NPC
```

### Predicate<T>

- test(T):boolean
- 입력된 T type 데이터의 특정 조건 검사 결과  boolean 반환

```jsx
Predicate<Hamburger> bigMacChecker = burger->burger.getClass()==BigMac.class;

bigMacChecker.test(new Whopper); // false
bigMacChecker.test(new BigMac); // true
```

### Supplier

- get():T
- 매개변수 없이 T type 데이터 반환

```jsx
Supplier<Integer> dummyCreator = ()->{
	int num = (int)(Math.random()*10)+1;
	return (num>5)? num: 5;
};

dummyCreator.get(); // 5~10
dummyCreator.get(); // 5~10
```

### Lambda + Stream

java8에서 제공되는 stream api와 람다를 같이 사용하면 효율적이고 간결한 코드 작성이 가능해진다
