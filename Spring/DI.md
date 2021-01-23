[돌아가기](./README.md)
# 다양한 의존관계 주입 방법

- 생성자 주입
- 수정자 주입(setter)
- 필드 주입
- 일반 메서드 주입

# 생성자 주입

클래스 생성자를 통해서 의존관계를 주입하는 방법

```jsx
public class Something {

    private Other other;

    @Autowired
    public Something(Other other) {
        this.other = other;
    }
}
```

### 특징

- 생성자 호출 시 딱 1번만 호출이 되는 것이 보장됨
- 필수로 주입이 되어야 하고, 한번 주입된 후에 불변을 유지하는 의존관계에 사용됨
- 생성자가 하나일 경우, 등록된 빈에 한해서 `@Autowired` 없어도 자동 주입 가능

# 수정자 주입

setter를 통해서 의존관계를 주입하는 방법

```jsx
public class Something {

    private Other other;

    @Autowired
    public void setOther(Other other) {
        this.other = other;
    }
}
```

### 특징

- 선택적으로 주입되고, 변경 가능성이 있는 의존관계에 사용됨
- 관례적인 setter를 통한 주입

# 필드 주입

필드에 바로 의존관계를 주입하는 방법

```jsx
public class Something {

    @Autowired private Other other;

}
```

### 특징

- 간결하지만 외부 변경이 불가능해서 테스트가 어려운 단점이 있음

    → DI 기술이 없는 경우 사용 불가; 즉 순수 자바에서 사용 불가능함

    (권장되지 않는 주입 방법)

- 스프링과 관련된 `@Configuration`과 같은 곳에서 간단한 테스트 용도로만 사용하자

# 일반 메서드 주입

일반 메서드에 의존관계를 주입하는 방법

```jsx
public class Something {

    private Other other;

    @Autowired
    public void foo(Other other) {
        this.other = other;
    }
}
```

### 특징

- 한번에 여러 필드 주입 가능

# 주입 옵션 처리

주입할 빈이 없어도 동작해야하는 경우에 옵션을 줄 수 있다

`@Autowired` 의 `required` 옵션이 디폴트로 `true` 이기 때문에, 빈이 없으면 오류가 발생한다

`false` 로 바꿔준다면, 주입할 빈이 없어도 동작하도록 설정할 수 있다 

### @Autowired(required=false)

자동 주입할 빈이 없다면 메서드 자체가 호출되지 않음

# 생성자 주입이 권장되는 이유

### 불변성 보장

→ 관례적으로, 애플리케이션 주기 동안 의존관계가 변경되는 일이 없다;

오히려 애플리케이션 종료까지 안전성의 이유로 불변성이 요구됨

### 누락 사전 방지

→ 순수 자바 코드로 단위 테스트에 필요한 의존관계를 컴파일 단계에서 미리 확인할 수 있음

### final 사용 가능

→ 의존 관계로 주입받을 빈이 설정되지 않을 경우를 컴파일 단계에서 미리 확인할 수 있음

(생성자 주입 방법 외에는 전부 final을 사용할 수 없다)

⇒ 즉, 필수 의존관계는 생성자 주입을 사용하고, 가끔 있을 선택적 의존관계는 수정자 주입 방법을 이용

# 롬복

반복적인 작업을 애노테이션을 통해 자동으로 처리할 수 있도록 지원하는 라이브러리

### lombok의 대표적 기능

- Getter & Setter 자동 생성

    `@Getter` `@Setter` 애노테이션을 통해 필드들의 getter와 setter를 자동 생성

- 생성자 자동 생성

    `@NoArgsConstructor` 같은 생성자 애노테이션을 통해 생성자 자동 생성

- ToString 자동 생성

    `@ToString` 애노테이션을 통해 필드들의 ToString 자동 생성

- final 필드 생성자 주입 자동 생성

    `@RequiredArgsConstructor` 애노테이션을 통해 final 필드들의 자동 생성자 주입 생성

# 중복 빈 문제 (NoUniqueBeanDefinitionException)

어떤 상위 타입에 대해, 2개 이상의 하위 타입이 빈으로 등록될 때 Exception 발생

→ 타입 당 싱글턴 빈을 요구함

하위 타입을 직접 빈으로 지정하는 것은 DIP 위반이므로 피해야하는 해결책

# 중복 빈 해결 방법

### @Autowired 필드 이름 매칭 방법

타입 중복이 발생하면, 차선책으로 `@Autowired`가 부착 되는 참조변수의 이름을 두번째 매칭 기준으로 선택

```jsx
@Autowired
private Hamburger bigMac; // Hamburger 빈이 여러개일 경우, BigMac 타입 빈을 선택
```

→ 단, 변수 이름이랑 매칭되는 빈이 있을 때 적용됨

### @Qualifier 사용하는 방법

`@Qualifier` 를 이용하여 추가 구분자를 부여하는 방법

→ 빈 이름의 변경이 아니라, 추가적인 별명을 부여하는 것

```jsx
@Component
@Qualifier("mainHamburger")
public class BigMac implements Hamburger {
    ...
}
```

```jsx
@Component
public class SetMenu {

    private final Hamburger hamburger;
    private final Drink drink;
    private final SideMenu sideMenu;

    @Autowired
    public SetMenu(@Qualifier("mainHamburger") Hamburger hamburger, ...) {
        this.hamburger = hamburger;
        ...
    }
```

구분자를 추가할 컴포넌트 클래스에 `@Qualifier` 애노테이션을 추가하고,

의존성 주입 당시에 다시 한번 `@Qualifier` 애노테이션을 이용

→ 구분자를 못찾으면 구분자 이름에 해당하는 스프링 빈을 추가로 찾는다

**NoSuchBeanDefinitionException**

→구분자를 가진 빈을 못찾거나, 구분자 이름에 해당하는 빈이 없는 경우 발생

### @Primary 사용하는 방법

빈에 최우선 순위를 부여하는 방법 → 중복되는 빈들 가운데 가장 높은 우선 순위를 부여하게 된다

**우선 순위**

→ `@Primary` 보다 `@Qualifier`가 더 우선순위가 높다

### 중복 빈이 모두 필요한 경우

Map, List 이용 → 중복되는 빈을 전부 자동 주입해줌

```jsx
public class HamburgerService {

    private final Map<String, Hamburger> hamburgerMap;
    private final List<Hamburger> hamburgers;

    @Autowired
    public HamburgerService(
        Map<String, Hamburger> hamburgerMap, 
        List<Hamburger> hamburgers) {

        this.hamburgerMap = hamburgerMap;
        this.hamburgers = hamburgers;
    }
}
```

# 빈 자동 주입과 수동 주입 선택 시점

대체적으로 컴포넌트 스캔과 자동 주입을 이용하는 것이 편하고, 권장된다

자동 빈 등록 또한 OCP, DIP를 지킬 수 있으므로 자동 주입이 크게 단점이 없다

### 수동 빈 등록이 필요한 경우

업무 로직 빈은 자동 주입을, 기술 지원 빈은 수동 주입으로 관리할 필요가 있다

→ 기술 지원 빈 상대적으로 수가 적고, 직접 손이 가는 경우가 크기 때문
