[돌아가기](./README.md)
# 컴포넌트 스캔

`@Bean` 이나 `<bean>` 같은 직접적인 빈 등록 과정 없이 자동으로 스프링 빈을 등록하는 기능

의존 관계를 자동으로 주입해주는 `@Autowired` 기능 또한 제공

### @ComponentScan

스캔 대상 애노테이션이 붙은 클래스를 빈으로 자동 등록한다

이때 자동 등록되는 빈의 디폴트 이름은 클래스 이름을 사용하되 앞글자가 소문자가 된다

→ `@Component("이름")` 과 같이 뒤에 임의의 이름 옵션을 줄 수도 있다

### 컴포넌트 스캔 기본 대상

- `@Component`
- `@Contoller` → MVC Controller
- `@Service` → 비즈니스 로직
- `@Repository` → 데이터 접근 계층 (데이터 계층 Exception을 스프링 Exception으로 변환)
- `@Configuration` → 설정 정보

### @Autowired

`@Component`가 붙은 클래스 내에 필요한 의존성을 자동 주입 해준다

디폴트 조회는 getBean과 같은 역할을 한다

## 컴포넌트 스캔 옵션

### basePackages

컴포넌트 탐색할 위치를 지정한다

```jsx
@ComponentScan(
    basePackages = "applicaion.core",
)
```

basePackages = { "applicaion.core", "applicaion.service" } 와 같이 여러 위치도 선정 가능

→ basePackages 옵션 설정이 없으면,

디폴트로 @ComponentScan이 붙은 클래스의 패키지가 기본 패키지로 설정됨

### includeFilters

컴포넌트 스캔에 추가할 필터를 설정한다

```jsx
@ComponentScan(
    includeFilters = @Filter(
                type = FilterType.ANNOTATION, 
                classes = Include.class))
```

### excludeFilters

컴포넌트 스캔에 배제할 필터를 설정한다

```jsx
@ComponentScan(
    excludeFilters = @Filter(
                type = FilterType.ANNOTATION,
                classes = Exclude.class))
```

### FilterType

- ANNOTATION → 디폴트 설정; 애노테이션
- ASSIGNABLE → 지정 클래스와 그 자식 클래스들
- ASPECTJ → AspectJ 패턴
- REGEX → 정규표현식
- CUSTOM → `TypeFilter` 인터페이스의 구현 커스텀

# 중복 등록 및 충돌

### 자동 등록 빈 vs 자동 등록 빈

컴포넌트 스캔으로 자동 등록된 빈 이름이 겹칠 경우 오류 발생

→ `ConflictingBeanDefinitionException`

### 수동 등록 빈 vs 자동 등록 빈

- legacy

    `@Bean` 이나 `<Bean>` 을 통해 수동으로 등록하는 빈이 우선권을 가져서, 자동 등록되는 빈을 오버라이딩

- 최근

    에러가 발생하도록 변경됨 → 수동 등록된 빈은 개발자의 의도가 아닐 가능성이 높기 때문
