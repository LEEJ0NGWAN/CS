[돌아가기](./README.md)

# Spring 컨테이너

스프링 애플리케이션 동작을 위해 `ApplicationContext` 객체가 필요한데

이때 이 `ApplicationContext` 객체를 일반적으로 스프링 컨테이너라고 한다

```jsx
// @Configuration 애노테이션이 붙은 클래스로 구현한 ApplicationContext
ApplicationContext applicationContext = 
		new AnnotationConfigApplicationContext(AppConfig.class);
```

- 스프링 컨테이너를 생성하기 위해 applicationContext의 구성정보 `AppConfig.class` 를 입력

### **ApplicationContext**

- `@Configuration` 을 가지고 있는 클래스
- `@Bean` 을 가지는 내부 메서드를 통해 Spring 컨테이너에 Bean(스프링이 관리하는 객체) 등록

### Bean

- 스프링이 관리하는, 스프링 컨테이너에 등록된 객체
- `@Bean` 을 가지는 메서드의 이름을 해당 Bean의 이름으로 지정

    → `@Bean(name="beanName")` 을 이용하여 Bean의 이름을 임의로 지정할 수도 있다

    Bean의 이름은 각자 고유해야하며, 중복될 경우 덮어 씌어진다 (옛날에는 튕겼음)

    ```jsx
    @Configuration
    public class AppConfig {

    		// PencilCase 타입의 pencilCase 빈
    		@Bean
    		public PencilCase pencilCase() {
    				return new MetalPencilCase();
    		}

    		// Pencil 타입의 pencil 빈
    		@Bean
    		public Pencil pencil() {
    				return new HBPencil();
    		}

    		// Pen 타입의 pen 빈
    		@Bean
    		public Pen pen() {
    				return new BallPen();
    		}

    } 
    ```

- ApplicationContext.getBean() 메서드를 통해 컨테이너에 등록된 빈을 찾는다

### 빈 의존관계 설정

- 스프링 컨테이너는 설정 정보를 참고하여 빈 생성 후, 의존성 주입(의존 관계 설정)을 함
- 단순히 자바코드를 호출하는 것 이상으로 차이가 존재

# 빈 반환 관련

- `getBeanDefinitionNames()` → String[] : 스프링에 등록된 모든 빈의 이름 조회
- `getBean(String)` → Bean: 빈 이름으로 빈 인스턴스를 반환
- `getBeanDefinition(String)` → BeanDefinition: 빈 이름으로 빈 정의(설정) 객체 반환
- `beanDefinition.getRole()` → int: 빈 종류를 확인

### 등록된 빈이 없을 때

NoSuchBeanDefinitionException 발생

### 동일 타입의 빈이 두개 이상일 때

NoUniqueBeanDefinitionException 발생

### 상속 관계에 있는 빈 조회

→ 어떤 부모 타입에 대해 조회를 한다면, 상속하는 모든 자식 타입의 빈 모두 반환

# BeanFactory와 ApplicationContext

### BeanFactory?

스프링 컨테이너의 최상위 인터페이스

→ 스프링 빈 관리 및 조회 기능을 명세

getBean, etc ...

### ApplicationContext

→ BeanFactory 기능을 모두 상속한 하위 클래스

빈 관리 및 조회(BeanFactory 제공) 뿐만이 아니라 애플리케이션 개발에 필요한 수 많은 부가 기능 구현

## ApplicationContext가 제공하는 부가 기능

- 메세지 소스를 활용한 국제화
- 환경변수

    로컬, 개발, 운영과 같은 스테이징 처리

- 애플리케이션 이벤트

    이벤트 발행 및 구독 모델을 편리하게 지원

- 편리한 리소스 조회

    파일, 클래스 패스, 외부 등에서 리소스를 편리하게 조회

BeanFactory와 ApplicationContext 모두 스프링 컨테이너이지만, 

BeanFactory를 직접 사용하는 일은 없고 부가 기능을 제공하는 ApplicationContext를 사용

# XML을 이용한 스프링 컨테이너

레거시에 사용된 방식

컴파일 없이 빈 설정 정보를 변경 가능한 장점이 있음

`GenericXmlApplicationContext` 사용

# BeanDefinition

스프링 빈 설정 메타 정보

`@Bean`, `<bean>` 당 하나의 빈 메타 정보를 생성

→ **스프링 컨테이너는 이 메타 정보를 기반으로 스프링 빈 생성**

### BeanDefinition가 가지고 있는 정보

- BeanClassName
- factoryBeanName
- factoryMethodName
- Scope
- lazyInit
- initMethodName
- DestoryMethodName
- Constructor arguments, Properties

이론적으로 BeanDefinition을 직성 생성해서 스프링 컨테이너에 등록 가능하나 비 효율적이다
