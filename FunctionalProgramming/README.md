[돌아가기](https://github.com/LEEJ0NGWAN/CS)

# 프로그래밍 관점

## 명령형 프로그래밍

프로그래밍의 상태, 그 상태를 변경시키는 구문의 관점에서 연산을 설명

- 절차적 프로그래밍

    수행되어야 할 연속적인 루틴으로 프로그램을 구성하는 방식(C, C++, Python)

- 객체 지향 프로그래밍

    데이터를 객체로 나타내고, 객체 간의 상호작용을 통해 프로그램을 구성하는 방식(Java, C++, Python, C#)

## 선언형 프로그래밍

"어떤 방법으로 해야 하는가" 보다, "무엇인가"로 설명

- 함수형 프로그래밍

    순수한 형태의 함수를 조합하여 프로그램을 구성하는 방식

## 명령 vs 선언

- 명령형 → 알고리즘 명시
- 선언형 → 목표 명시

## Javascript 코드 비교

### 명령형

```jsx
// 어떻게 해야 하는가?
function reverseSign(num) {
	let result;
	result = num * -1;
	return result;
}
```

### 선언형

```jsx
// 무엇인가?
function reverseSign(num) {
	return -num;
}
```

# 함수형 프로그래밍의 중요성

### 기존 프로그래밍

→ 생각한 것을 그대로 구현하는 방식

### 함수형 프로그래밍

→기존과 다른 사고방식을 요구

다양한 사고방식으로 프로그래밍을 할 경우, 다양한 문제에 유연하게 해결이 가능하게 된다

→ 문제의 종류, 상황에 따라서 선택 가능한 해결 도구가 늘어나기 때문

## 명령 프로그래밍 vs 함수 프로그래밍

- 프로그램?
    - 명령 → 프로그램은 명령의 수행이다.
    - 함수 → 프로그램은 함수의 계산이다.
- 중점?
    - 명령 → 어떻게 만들어야 하는가?
    - 함수 → 뭐가 나와야 하는가?
- 이론 배경
    - 명령 → 튜링 머신
    - 함수 → 람다 계산식
- 주요 언어
    - 명령 → Java .. 등등 대부분
    - Scheme, Haskell, ML, Erlang ...

# 기본 개념

## 1급 객체 (First Class Object, First Citizen)

변수나 어떤 자료 구조에도 포함시킬 수 있고,

인자로 전달될 수 있으며,

반환 값으로 사용 가능하고,

할당에 사용된 이름에 관계없이 고유 식별이 가능하며,

동적으로 property 할당이 가능한 객체

Javascript의 function은 object 이기 때문에, `1급 함수` 라고 부름

## 고차 함수 (High-Order Function)

함수를 인자로 전달할 수 있고,

함수를 반환 값으로 사용 가능한 함수

고차 함수는 `1급 함수` 의 부분 집합이다.

React의 고차 컴포넌트(HOC)는 컴포넌트를 사용하여 위의 조건을 만족하는 컴포넌트

## 불변성 (Immutability)

데이터가 변할 수 없다는 것을 나타내는 성질

데이터의 변경이 필요한 경우, 원본 데이터의 사본을 변경하고 해당 사본으로 작업을 진행

```jsx
// 가변성
function increaseAge(person) {
	person.age = person.age + 1;
}

// 불변성
function increaseAge(person) {
	return Object.assign({}, person, {age: person.age+1});
}
```

## 순수 함수 (Pure function)

동일한 입력에 항상 같은 값을 반환하고,

프로그램의 실행에 영향을 미치지 않는(Side effect가 없는) 함수

→ Side effect?

함수 내부에서, 입력 받은 인자의 상태를 변경하거나, 외부의 상태를 변경하는 것

```jsx
// 순수하지 않음
function add(num) {
	let e = document.createElement('p');
	e.innerText = num;

	document.body.appendChild(e); // DOM을 변경하는 side effect
}

// 순수 함수
function pMaker = (num) => <p>{num}</p>;
```

## 데이터 변환

함수형 프로그래밍은 불변성에 의해, 기존 데이터의 사본을 수정하는 방식이 요구됨

## 합성 함수 (Function composition)

작은 순수 함수들을 조합하여 계산하는 함수

→ 연쇄적 및 병렬적으로 호출해서 더 큰 함수를 만드는 과정으로 전체 프로그램을 구성

### Method Chaining

```jsx
const composeFunction = (...functions) =>
	functions.reduce(
		(prevFunc, nextFunc) => (...args) => nextFunc(prevFunc(...args)));
```

```jsx
const sub = (a, b) => a-b;
const cmp = (x) => x? (x > 0)? 1 : -1 : 0;

const subCheck = compose(sub, cmp);
subCheck(3, 5);
```

# 함수형 프로그래밍 구현 방법

- 순수 함수를 조합할 것
- 공유 상태(shared state), 가변 데이터(mutable data), 부수 효과(side effect)를 피할 것
- 선언형 프로그래밍으로 진행하며, 애플리케이션이 상태는 순수 함수를 통해 전달할 것
