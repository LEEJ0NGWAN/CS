[돌아가기](./README.md)

# 빈 스코프

빈이 존재할 수 있는 범위

→ `@Scope` 애노테이션을 이용하여 범위를 설정한다

### 싱글톤 스코프

기본 스코프로, 스프링 컨테이너의 시작부터 종료까지 유지되는 가장 넓은 범위의 스코프

### 프로토타입 스코프

스프링 컨테이너가 프로토타입 빈 생성 및 의존관계 주입까지만 관여를 하는 매우 짧은 범위의 스코프

### 웹 관련 스코프

- request 스코프 → 웹 리퀘스트가 처리될 때까지 유지되는 스코프
- session 스코프 → 웹 세션이 생성부터 종료될 때까지 유지되는 스코프
- application 스코프 → 웹 서블릿 컨텍스와 같은 범위의 스코프

# 프로토타입 스코프

스프링 컨테이너에 조회할 때마다 새로운 프로토타입 빈이 생성됨

→ 스프링 컨테이너가 필요 의존관계 주입 및 초기화까지 처리해줌

클라이언트에 빈을 반환한 뒤 스프링 컨테이너는 생성한 프로토타입 빈을 관리하지 않는다

→프로토타입 빈을 관리할 책임은 전적으로 클라이언트에게 있음 (@PreDestroy 먹히지 않음)

### 싱글톤 빈과 함께 사용 시 문제점

스프링 컨테이너는 프로토타입 빈 요청 시 새로운 인스턴스를 생성해서 반환하지만,

싱글톤 빈과 함께 사용 시 의도한 동작을 하지 않는다

**싱글톤 빈 내부에서 프로토타입 빈을 의존성으로 주입받는 경우**

싱글톤 빈 생성 시 의존관계 주입 받는 과정에서 스프링 컨테이너가 프로토타입 빈을 생성하는데

그 프로토타입 빈은 enclosure처럼 싱글톤 빈이 소멸하기 전까지 계속 가지게 되는 것이다

그러므로, 해당 싱글톤 빈의 로직을 사용하는 과정에서 프로토타입 빈이 계속 새로 생성되는 일이 발생할 수 없다

→ 즉, 프로토타입 빈을 주입 받는 시점을 다양하게 설정하는 것이 중요하다

### Provider

싱글톤 빈과 프로토타입 빈 함께 사용 시, 사용할 때마다 새로운 프로토타입 빈을 가져오기 위한 방법

→ 프로토타입 빈 뿐만이 아니라 DL이 필요한 모든 경우에 사용 가능!

- ObjectProvider::getObject

    지정한 빈을 컨테이너에서 대신 찾아주는 DL 서비스 제공

    ```jsx
    @Scope("prototype")
    @Component
    class PrototypeBean {
    	...
    }

    @Component
    class ClientBean {

    	private ObjectProvider<PrototypeBean> provider;

    	@Autowired
    	public ClientBean (ObjectProvider<PrototypeBean> provider) {
    		this.provider = provider;
    	}

    	public void logic() {
    		PrototypeBean pb = provider.getObject();
    		
    		...
    	}
    }
    ```

    getObject() 메소드를 통해 DL(스프링 컨테이너에서 해당 빈을 찾는 것) 수행

    - ObjectFactory
        - 기능이 단순
        - 별도 라이브러리 x
        - 스프링 의존
    - ObjectProvider
        - ObjectFactory 상속
        - Optional, stream 처리 등의 편의 기능이 많음
        - 별도 라이브러리 x
        - 스프링 의존

- javax.inject.Provider::get (JSR-330 Provider)

    ```jsx
    @Autowired
    private Provider<PrototypeBean> provider;

    public void logic() {
    	PrototypeBean pb = provider.get();
    	...
    }
    ```

    - 자바 표준 라이브러리로 스프링이 아닌 컨테이너에서도 가능
    - 단순한 기능을 제공
    - mock 코드나 단위 테스트 작성에 용이
    - DL 서비스를 제공
    - 라이브러리 추가를 요구

## 프로토타입 빈 사용 시기

→ 사용할 때마다 매번 DI 완료된 새로운 인스턴스가 필요할 때 사용

그러나, 대부분은 싱글톤 빈으로 해결
