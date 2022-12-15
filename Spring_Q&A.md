# Spring Framework
<details>
<summary>왜 프레임워크를 사용할까?</summary>

<br>

- 체계적인 코드관리로 유지보수가 용이하다.
- 기본설계 및 기능 라이브러리를 제공하여 개발 생산성이 높다
- 코드에 대한 재사용성이 높다
- 추상화된 코드 제공을 통해 확장성이 좋다.

</details>

<details>
<summary>왜 스프링을 사용할까?</summary>

<br>

1. **대중적인 언어인 Java 기반의 프레임워크이다.**
2. **시간이 흐르며 프레임워크가 단단해지고 있다.**
3. **다양한 개발사례와 문서, 레퍼런스가 제공되고 있다.**
4. **POJO기반의 구성(Plain Old Java Object)**
5. **DI를 통한 객체 관계 구성**
6. **AOP 지원**
7. **편리한 MVC 구조**
8. **WAS에 독립적인 개발 환경**
9. **개발자가 기본적으로 DI, AOP, 서비스 추상화와 같은 디자인 패턴을 강제적으로 사용하게끔 함으로서 코드 구조 퀄리티의 최소한을 보장한다.**

[[Spring] 우리는 왜 스프링을 사용하는가?](https://seongwon.dev/Spring/20220627-%EC%9A%B0%EB%A6%AC%EB%8A%94-%EC%99%9C-%EC%8A%A4%ED%94%84%EB%A7%81%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C/)

</details>

<details>
<summary>Spring과 Spring Boot의 차이점은 뭘까요?</summary>

<br>

- Starter의존성을 제공한다.
- WAS서버를 내장으로 갖고 있어 배포가 편해졌다.
- XML로 관리하던 설정들을 [application.properties/yml로](http://application.properties/yml로) 쉽게 할 수 있다.

[[Spring] Spring과 Spring Boot의 차이는 무엇일까?](https://seongwon.dev/Spring/20220628-Spring-vs-SpringBoot/)

</details>

<details>
<summary>Spring의 3대 요소는 무엇이 있을까?</summary>

<br>

AOP, DI, PSA
Spring이 위의 3가지 요소를 통해 어떤 것을 추구할까?

- POJO를 통해 비즈니스 로직에 집중할 수 있도록 하는 것이다.

</details>

<details>
<summary>DI, IoC는 무엇일까요?</summary>

<br>

**DI**는 외부에서 의존 관계를 주입해 결합도를 낮추고 유연성을 높여주는 기술이다.

스프링의 DI는 스프링 컨테이너에 필요한 객체(Bean)들을 싱클턴으로 생성하고 생성한 객체에 의존을 주입하며 제공한다.

DI는 스프링에서 IoC를 구현한하는데 사용하는 패턴이다.

IoC는 객체 또는 프로그램의 제어 권한을 프레임워크에 넘기는 기술이다. 스프링에서 빈을 생성, 소멸의 작업들을 수행하고 의존 주입의 대상까지 스프링이 해주는데 이것이 바로 스프링의 IoC이다.

IoC의 장점

- 유연성 증가 → 다른 구현체로 변경하기 쉽다.
- 객체간 결합도 감소 → 프로그램을 모듈들로 나누기 쉽다.
- 작업의 실행과 구현을 분리할 수 있다.
- 컴포넌트를 격리하거나 의존성을 mocking하는 등의 작업을 통해 테스트를 하기 쉽다.

> 스프링이 DI를 제공하여 이점을 느낀 경험에 대해 설명하라 할 수 있다.

[[Spring] DI,IoC란 무엇일까?](https://seongwon.dev/Spring/20220614-%EC%8A%A4%ED%94%84%EB%A7%81-DI-IoC/)

</details>

<details>
<summary>IoC의 2가지 분류, Spring 외부에서 의존성을 할당해주는 방법 2가지</summary>

<br>

- 의존 주입 방법은 `DL`, `DI`이 있다.
- DL(Dependency Lookup)은 프로그램이 실행되며 동적으로 빈을 바꾸고 싶을 때 사용
    - DL은 의존관계가 있는 객체를 외부에서 주입해주는 것이 아니라 의존 관계가 필요한 객체에서 직접 컨테이너가 제공하는 API를 통해 검색하는 방식이다.
    - 클라이언트 객체(의존관계가 필요한 객체)에서는 의존하고자 하는 인터페이스 타입만 지정해서 검색할 뿐 해당 인터페이스를 구현한 구체적인 클래스 객체에 대한 결정과 해당 객체에 대한 생명 주기는 IoC 컨테이너에서 책임집니다.

</details>

<details>
<summary>DIP(Dependency Inversion Principle)란 무엇일까?</summary>

<br>

- **저수준 모듈이 고수준 모듈에 의존하게 되는 것을 DIP(의존관계 역전 원칙)라 한다.**
- 추상화에 의존하고 구체화에 의존하면 안 된다. 즉, 하위 모듈이 상위 모듈에서 정의한 추상 타입(인터페이스)에 의존하여야 한다.

코딩 실천법

1. 변동성이 큰 구체 클래스를 참조하지 말고 추상 인터페이스를 참조하라
2. 변동성이 큰 구체 클래스로부터 파생하지 말아라
3. 구체 함수를 오버라이드 하지 말아라

</details>

<details>
<summary>Bean이란 무엇일까?</summary>

<br>

스프링을 사용하다보면 DI/IoC에 의해 스프링에게 객체의 생명주기를 맡기게 된다. 이때 스프링은 IoC를 위해 스프링 컨테이너를 만들고 생성한 객체들을 컨테이너에서 관리하는데 해당 객체들을 Bean이라고 한다.

스프링이 빈을 등록하고 관리하는 방법은 xml, Annotation-based configuration, Java-based configuration 방법이 있다.

[[Spring] Bean이란 무엇일까?](https://seongwon.dev/Spring/20220616-%EC%8A%A4%ED%94%84%EB%A7%81-Bean/)

</details>

<details>
<summary>Bean의 라이프사이클에대해 설명해주세요</summary>

<br>

- **객체 생성**
- **의존 결정**: 의존 자동 주입을 통한 의존 설정과 설정 클래스에 있는 의존 주입들이 모두 수행된다.
- **초기화**: 의존 결정이 완료되면 스프링 빈은 빈 객체의 지정된 메서드를 호출하여 빈을 초기화해 준다.
- **소멸**: 스프링 컨테이너가 종료되면 스프링 컨테이너가 빈 객체를 소멸시킨다.

</details>

<details>
<summary>Bean의 Scope는 무엇이 있을까요?</summary>

<br>

- Singleton, Prototype, Request, Session, Global Session
- 프로토타입 빈은 매번 새로운 객체를 생성한다.
- 📌 프로토타입 빈을 사용하면 빈은 객체 생성, 프로퍼티 설정 및 초기화 작업까지는 수행하지만, 컨테이너를 종료한다고 해서 생성한 빈의 프로토타입 빈의 소멸 메서드를 실행하지는 않는다. 즉, 소멸 과정이 실행되지 않아 프로토타입 범위의 빈을 사용할 때는 빈 객체의 소멸 처리를 코드에서 직접 해줘야 한다.

[[Spring] Spring Bean의 개념과 Bean Scope 종류 - Heee's Development Blog](https://gmlwjd9405.github.io/2018/11/10/spring-beans.html)
</details>

<details>
<summary>@Bean, @Configuration을 통해 빈을 등록하는 상황은 어떤 상황이 있을까?</summary>

<br>

- 개발자가 직접 제어가 불가능한 라이브러리를 사용할 때
    - Gson과 같이 외부에서 가져다쓰는 클래스인 경우 싱글톤으로 사용해야지 메모리상의 이점을 얻을 수 있다. 하지만 외부 클래스들은 우리가 직접 제어를 할 수 없기에 `@Bean`으로 수동 등록하여 사용해야 한다.
- 애플리케이션 전범위적으로 사용되는 클래스를 등록할 때
- 다형성을 활용하여 여러 구현체를 등록해줘야 할 때
    - `@Bean`을 통해 등록을 해주면 어떤 구현체들이 빈으로 등록되었는지를 `@Configuration`클래스만 보면 되어서 한 눈에 파악하기 쉽고 유지보수하기 좋다.

</details>

<details>
<summary>스프링의 의존 자동 주입 방법</summary>

<br>

- `@Autowired` - 필드, 생성자, 세터 메서드에 해당 어노테이션을 붙여주면 스프링은 **타입**이 일치하는 빈 객체를 찾아서 주입을 해준다.
- 생성자 주입
    - 호출 시점에 1회 호출된다는 보장이 있다. 주입을 받는 객체들이 변하지 않는다는 보장이 되고 필드에 final을 붙일 수 있다
    - 생성자가 1개만 있을 경우 `@Autowired` 어노테이션이 생략 가능하다.
- Setter주입
    - Setter 주입 방법은 주로 주입 받는 객체가 변경될 가능성이 있는 경우에 사용을 한다.
    - 개발자가 실수로 의존 객체를 올바르게 주입하지 않을 경우, 사용 시점에 `NullPointerException`이 발생할 수 있다는 단점이 있다.
    - Setter를 열어둬야 한다.
- 필드 주입
    - 필드에 `@Autowired`를 붙여 바로 의존 관계를 주입하는 방법이다.
    - 필드 주입 방법은 코드가 간결해져 과거에는 많이 사용하였지만 외부에서 접근이 불가능하여 테스트의 어려움이 있다.
    - 스프링과 같은 DI를 제공하는 프레임워크에서만 동작하여 프레임워크의 변경이 있을 시 많은 문제를 초래할 수 있다.

> 📌 필드 주입은 빈의 생성자가 실행된 바로 직후에 실행이 되게 된다.

</details>

<details>
<summary>@RequestParam, @RequestBody, @ModelAndAttribute 차이</summary>

<br>

`@RequestParam`

- Query Parameter나 form data 형식의 데이터들을 컨트롤러의 method argument로 변환해준다.

`@RequestBody`

- Http request body의 값을 읽어오기 위해 사용되는데 이를 `HttpMessageConverter`를 통해 객체로 역직렬화해준다
- JSON 데이터를 객체로 반환할 때 Spring에 등록되어있는 Jackson라이브러리의 `MappingJackson2HttpMessageConverter`를 사용하여 Reflection을 통해 역직렬화를 하기 때문에 DTO에는 기본 생성자와 getter/setter등이 필요하다.

  > 역직렬화는 stream→객체, 직렬화는 객체→ stream
>

`@ModelAttribute`

- ModelAttribute는 RequestBody와 다르게 MessageConverter를 통해 Json을 객체로 변환해주는 방법이 아닌 생성자나 Setter를 통한 데이터 주입을 시켜 객체를 생성한다. 만약 값을 주입해주는 생성자나 setter함수가 없다면 매핑을 시키지 못하고 필드는 null값을 갖게 된다.

</details>

<details>
<summary>Servlet이란?</summary>

<br>

- 서블릿은 동적 웹 페이지(Dynamic Web Page)를 만들 때 사용되는 **자바 기반의 웹 애플리케이션 컴포넌트**이다.
- Sevlet은 하나의 Process로 만들어지고 그 안에 Thread Pool을 만들어 Thread로 처리한다.
    - Servlet이전에 사용하던 CGI는 요청이 왔을 때 요청을 처리하기 위해 Process를 매번 만들어 처리 비용이 비쌌다. 이전 구현체의 재사용이 아닌 새로운 CGI 구현체를 생성하여 사용하여 낭비가 발생했다.
- 서블릿 컨테이너에서 서블릿의 생명주기를 관리한다. (IoC → 서블릿 컨테이너에게 제어를 넘긴다.)

- Servlet의 생명주기
    - `init()`메서드: 서블릿 생성시 초기화 작업을 수행하며 맨 처음 한 번만 수행한다.
    - `service()` 메서드: 서블릿이 요청에 응답하도록 컨테이너에서 실행되는 메서드이다.
    - `destroy()`메서드: 서블릿이 기능을 수행하고 메모리에서 소멸될 때 호출된다.
- Servlet 컨테이너란?

  서블릿 컨테이너는 구현되어 있는 Servlet 클래스들의 규칙에 맞게 서블릿을 관리해주는 컨테이너이다. 서블릿 컨테이너는 서블릿들의 생명 주기를 관리해주며 클라이언트가 요청을 보내면 HttpServletRequest, HttpServletResponse 두 객체를 생성하여 post, get 여부에 따라 동적인 페이지를 생성하여 응답을 보낸다.

  이점

    - **서블릿의 생명주기 관리 (IoC)**
    - **웹 서버와의 통신 지원**
    - **멀티스레딩 지원 및 관리**
    - **선언적인 보안관리**
- 문제점
    1. 1대1 매핑 구조를 갖고 있어 공통 로직에 대해 중복 로직이 발생한다.
    2. 모든 요청들이 서블릿에 의존적이어서 Servlet에 종속적인 프로그램을 작성하게 된다.

[[Spring] Servlet이란?](https://seongwon.dev/Spring/20220620-Servlet%EC%9D%B4%EB%9E%80/)

</details>

<details>
<summary>Dispatcher Servlet이란? + MVC 동작방식에 대해 설명해주세요</summary>

<br>

Servlet의 단점을 보완하기 위해 만들어진 것이 FrontController Pattern을 적용한 Dispatcher Servlert이 만들어졌다. 요청이 오면 Dispatcher Servlet에서 요청을 처리해줄 Servlet을 찾는 해준다. 요청에 따라 Servlet을 1대1로 생성하는 구조에서 Front Controller가 올바른 핵심 비즈니스 로직을 수행하게 변하여 생성해야하는 Servlet의 개수가 1개로 줄어들었다.

![Untitled](Spring/img/SpringMVC.png)

[[Spring] MVC 동작 방식 이해하기](https://seongwon.dev/Spring/20220621-%EC%8A%A4%ED%94%84%EB%A7%81MVC-%EB%8F%99%EC%9E%91%EB%B0%A9%EC%8B%9D/)

</details>

<details>
<summary>Apache Tomcat이란?</summary>

<br>

톰켓은 JAVA EE 기반으로 만들어졌으며 JSP와 Servlet을 구동하기 위한 서블릿 컨테이너 역할을 수행한다. 아파치서버와는 다르게 DB연결, 다른 응용프로그램과 상호 작용 등 동적인 기능들을 사용할 수 있다.

아파치 톰캣은 무엇일까? 톰캣이 아파치의 기능 일부를 가져와 제공해주는 형태이기에 합쳐서 아파치 톰캣이라고 부르고 있다.

</details>

<details>
<summary>Application Context와 Servlet Context의 차이가 무엇인가요?</summary>

<br>

Application Context는 Spring내에서 Bean들이 저장되는 context이고 Servlet은 Dispatcher Servlet의 context이다.

</details>

<details>
<summary>AOP란 무엇일까??</summary>

<br>

AOP(Aspect Oriented Programming)은 관점 지향 프로그래밍으로 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어 보고 그 관점을 기준으로 모듈화하는 기술을 의미한다.

흩어진 관심사를 Aspect로 모듈화하고 핵심적인 비즈니스 로직에서 분리하여 재사용하겠다는 것이 AOP의 취지이다.

**스프링 AOP의 특징**

- 프록시 패턴 기반의 AOP 구현체, 프록시 객체를 쓰는 이유는 접근 제어 및 부가기능을 추가하기 위해서임
- 스프링 빈에만 AOP를 적용 가능
- 모든 AOP 기능을 제공하는 것이 아닌 스프링 IoC와 연동하여 엔터프라이즈 애플리케이션에서 가장 흔한 문제(중복코드, 프록시 클래스 작성의 번거로움, 객체들 간 관계 복잡도 증가 ...)에 대한 해결책을 지원하는 것이 목적

**대표적인 예시**

- 스프링의 Transaction

</details>

<details>
<summary>Spring Event에 대해 설명해주세요</summary>

<br>

이벤트는 말 그대로 애플리케이션 내에서 어떠한 상황이 발생했을 때 발생시킬 수 있는 것이다.

스프링은 기본적으로 Event메커니즘을 제공하고 있다.

이러한 이벤트는 트리거 용도와 시스템간의 동기화 역할에 사용된다. 그리고 잘 사용하면 클래스, 패키지간 의존성 제거에 도움을 줄 수 있다.

</details>

<details>
<summary>Spring이 어떻게 Filter를 이용할까?</summary>

<br>

#### Spring

  과거에는 Spring Context외부에 있는 Filter는 직접 이용할 수 없었다. 하지만 DelegatingFilterProxy가 생기며 이용할 수 있게 되었다.

  DelegatingFilterProxy는 서블릿 컨테이너에서 관리되는 프록시용 필터로써 우리가 만든 필터를 가지고 있다. 필터에 관련한 빈 등록이 요청이 오면 DelegatingFilterProxy가 요청을 받아서 우리가 만든 필터(스프링 빈)에게 요청을 위임한다.

  1. Filter 구현체가 스프링 빈으로 등록됨
  2. ServletContext가 Filter 구현체를 갖는 DelegatingFilterProxy를 생성함
  3. ServletContext가 DelegatingFilterProxy를 서블릿 컨테이너에 필터로 등록함
  4. 요청이 오면 DelegatingFilterProxy가 필터 구현체에게 요청을 위임하여 필터 처리를 진행함

#### Spring Boot

  SpringBoot라면 DelegatingFilterProxy조차 필요가 없다. 왜냐하면 SpringBoot가 내장 웹서버를 지원하면서 톰캣과 같은 서블릿 컨테이너까지 SpringBoot가 제어가능하기 때문이다. 그래서 SpringBoot에서는 ServletContext에 필터(Filter) 빈을 DelegatingFilterProxy로 감싸서 등록하지 않아도 된다. SpringBoot가 서블릿 필터의 구현체 빈을 찾으면 DelegatingFilterProxy 없이 바로 필터 체인(Filter Chain)에 필터를 등록해주기 때문이다.

</details>

---

# JPA
<details>
<summary>JPA에서 영속성 컨텍스트에 대해 설명해주세요</summary>

<br>

- **엔티티를 영구 저장하는 환경**이라는 뜻을 가진 **논리적인 개념**으로 어플리케이션과 DB사이에서 객체를 보관하는 가상의 DB같은 역할을 한다. 즉, 애플리케이션에서 DB에 저장하기 전에 사용을 하는 임시 저장 공간이라고 이해를 하면 편할 것이다.
- 장점
  - **1차 캐시**
  - 영속성 컨텍스트 내의 영속 엔티티는 **동일성 보장**
  - 트랜잭션을 지원하는 **쓰기 지연**
  - **변경 감지(Dirty Checking)**

</details>

<details>
<summary>Dirty Checking에 대해 설명해주세요.</summary>

<br>

영속성 컨텍스트는 엔티티의 수정이 일어났을 때 개발자가 영속성 컨텍스트에 따로 알려주지 않아도 알아서 변경 사항을 체크해준다. 이것을 Dirty checking이라고 한다.

1차 캐시에 entity를 저장할 때, 스냅샷 필드도 따로 저장하여 commit이나 flush를 할 때 해당 entity와 스냅샷을 비교하여 변경사항이 있으면 알아서 UPDATE SQL을 만들어서 DB에 전송한다.

</details>

<details>
<summary>N+1문제를 해결할 수 있는 방법은 무엇이 있을까요?</summary>

<br>

Fetch join, EntityGraph, Batch size

**JoinFetch는 Inner Join, Entity Graph는 Outer Join**

→ 두 방법은 1:N관계에서 데이터가 증가하는 문제가 발생한다.

→ Fetch Join은 OneToMany관계에서 페이징을 하지 못한다

→ 데이터 뻥튀기 때문에 둘 이상의 컬렉션을 페치할 수 없다. (카테시안 곱으로 만들어진다)

> Hibernate 사용 시, 둘 이상의 컬렉션을 사용한 Fetch Join은 오류를 발생시킨다.

</details>
