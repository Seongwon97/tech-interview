# Java
<details>
<summary>다른 언어와 비교하였을 때 Java의 장점에 대해 설명해주세요.</summary>

<br>

- 플랫폼에 구애받지 않고 JVM이 설치된 모든 장치에서 동작한다.
    - 운영체제의 영향이 없이 동작하며 멀티 스레드를 지원하지 않는 OS에서도 자바 언어를 사용하면 멀티스레드를 구현할 수 있다.
- 객체지향 언어이다.
- 수많은 개발자와 레퍼런스가 있어 문제가 발생하였을 때, 트러블슈팅을 하기 쉽다.
- 디버깅하는 실행 속도를 개선하기 위해 JIT 컴파일러가 사용된다.
- GC(가비지 컬렉션)이 존재하여 객체의 소멸을 스스로 해준다.

단점

- 실행 속도가 다른 언어보다 느리다.
- 다른 언어와 비교했을 때 소스코드의 길이가 길다.
- GC가 언제 어떻게 작동될지 아무도 모르기 때문에 중간에 끊김 현상이 발생할 수 있어 실시간 응용 시스템으로 부적합하다

[Java의 장단점](https://okeybox.tistory.com/131)

</details>


<details>
<summary>자바의 버전별 특징에 대해 설명해주세요</summary>

<br>

자바8: 람다, 인터페이스의 default method, stream api, **Null 처리 Optional** 등이 추가됨

자바9: 인터페이스 내에서 private 메서드 사용이 가능

자바10: 타입 추론 변수 var 추가, 병렬 처리 GC, 개별 스레드로 분리된 Stop the world등이 추가됐다.

- 기존에는 Stop-The-World 가 발생하면 GC 를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춘다. GC 작업을 완료한 이후에야 중단했던 작업을 다시 시작한다. 근데 이게 개별 쓰레드로 분리되어서 Stop-The-World 시간이 개선된것 같다.

자바 11: String 메서드 추가(`strip()`, `isBlank()`, `lines()`, `repeat()`), 람다 파라미터로 var사용

자바 12~14: 스위치 표현식 개선 (표현식에서 값 반환 가능)

[java 버전별 차이 & 특징](https://velog.io/@ljo_0920/java-%EB%B2%84%EC%A0%84%EB%B3%84-%EC%B0%A8%EC%9D%B4-%ED%8A%B9%EC%A7%95)

</details>


<details>
<summary>객체지향 설계 5원칙(SOLID)란?</summary>

<br>

SRP(Single Responsibility Principle, 단일 책임 원칙)

- 작성된 클래스는 하나의 기능만 가지며 클래스가 제공하는 모든 서비스는 그 하나의 책임을 수행하는데 집중되어야 한다.

OCP(Open Close Principle, 개방폐쇄의 원칙)

- 소프트웨어의 구성요소는 확장에 열려있고 변경에는 닫혀있다. 변경을 위한 비용은 가능하면 줄이고 확장을 위한 비용은 극대화해야한다.
- 요구사항의 변경이나 추가 사항이 발생하여도 기존 구성요소는 수정이 일어나지 말아야 하며, 기존 구성요소를 쉽게 확장해서 재사용할 수 있어야 한다.

LSP(The Liskov Substitution Principle, 리스코프 치환의 원칙)

- 서브 타입은 언제나 기반 타입과 호환될 수 있어야 한다.
- 상속은 궁극적으로 다형성을 통한 확장성을 목표로 한다. LSP도 서브클래스가 확장에 대한 인터페이스를 준수해야함을 의미한다.

ISP(Interface Segregation Principle, 인터페이스 분리의 원칙)

- 한 클래스는 자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다. → 다른 크랠스에 종속될 때는 가능한 최소한의 인터페이스만을 사용해야 한다.

DIP(Dependency Inversion Principle, 의존성 역전의 원칙)

- 하위 레벨 모듈의 변경이 상위 레벨 모듈의 변경을 요구하는 위치 관계를 끊는 의미의 역전이다.
- **저수준 모듈이 고수준 모듈에 의존하게 되는 것을 의미한다.**
- 추상화에 의존하고 구체화에 의존하면 안 된다. 즉, 하위 모듈이 상위 모듈에서 정의한 추상 타입(인터페이스)에 의존하여야 한다.

</details>


<details>
<summary>GC(Garbage Collection)</summary>

<br>

`stop-the-world`란, GC을 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것이다.

- stop-the-world가 발생하면 GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춘다.

GC는 두 가지 가설 아래에서 만들어졌다.

- 대부분의 객체는 금방 접근 불가능 상태(unreachable)가 된다.
- 오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다.

이러한 가설에 의해 GC는 Young, Old영역으로 나눠서 동작하게 된다.

- Young 영역(Yong Generation 영역): 새롭게 생성한 객체의 대부분이 여기에 위치한다. 대부분의 객체가 금방 접근 불가능 상태가 되기 때문에 매우 많은 객체가 Young 영역에 생성되었다가 사라진다. 이 영역에서 객체가 사라질때 Minor GC가 발생한다고 말한다.
- Old 영역(Old Generation 영역): 접근 불가능 상태로 되지 않아 Young 영역에서 살아남은 객체가 여기로 복사된다. 대부분 Young 영역보다 크게 할당하며, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생한다. 이 영역에서 객체가 사라질 때 Major GC(혹은 Full GC)가 발생한다고 말한다.

Young영역은 Eden영역과 2개의 Survivor영역으로 나뉜다. 동작은 아래와 같다.

- 새로 생성한 대부분의 객체는 Eden 영역에 위치한다.
- Eden 영역에서 GC가 한 번 발생한 후 살아남은 객체는 Survivor 영역 중 하나로 이동된다.
- Eden 영역에서 GC가 발생하면 이미 살아남은 객체가 존재하는 Survivor 영역으로 객체가 계속 쌓인다.
- 하나의 Survivor 영역이 가득 차게 되면 그 중에서 살아남은 객체를 다른 Survivor 영역으로 이동한다. 그리고 가득 찬 Survivor 영역은 아무 데이터도 없는 상태로 된다.
- 이 과정을 반복하다가 계속해서 살아남아 있는 객체는 Old 영역으로 이동하게 된다.

> Survivor 영역 중 하나는 반드시 비어 있는 상태로 남아 있어야 한다.
>

Old 영역은 기본적으로 데이터가 가득 차면 GC를 실행한다. GC 방식에 따라서 처리 절차가 달라지므로, 어떤 GC 방식이 있는지 살펴보면 이해가 쉬울 것이다. GC 방식은 JDK 7을 기준으로 5가지 방식이 있다.

- Serial GC
  - CPU코어가 하나만 있을 때 사용하기 위해 만든 방식이라 성능이 많이 떨어져서 절대 사용하면 안된다
  - Old 영역의 GC는 `mark-sweep-compact`이라는 알고리즘을 사용
    1. Old 영역에 살아 있는 객체를 식별(Mark)
    2. 힙(heap)의 앞 부분부터 확인하여 살아 있는 것만 남긴다(Sweep)
    3. 각 객체들이 연속되게 쌓이도록 힙의 가장 앞 부분부터 채워서 객체가 존재하는 부분과 객체가 없는 부분으로 나눈다(Compaction)
- Parallel GC
  - Serial과 동작 알고리즘은 같으나 GC를 처리하는 쓰레드가 여러개라 더 빠르다.
- Parallel Old GC(Parallel Compacting GC)
  - `Mark-Summary-Compaction`단계를 거친다.
    - Summary 단계는 앞서 GC를 수행한 영역에 대해서 별도로 살아 있는 객체를 식별한다
- Concurrent Mark & Sweep GC(이하 CMS)
  - 동작은 과정
    1. Initial Mark 단계에서는 클래스 로더에서 가장 가까운 객체 중 살아 있는 객체만 찾는 것으로 끝내서 stop the world가 매우 짧다.
    2. Concurrent Mark 단계에서는 방금 살아있다고 확인한 객체에서 참조하고 있는 객체들을 따라가면서 확인한다. 이 단계의 특징은 다른 스레드가 실행 중인 상태에서 동시에 진행된다는 것이다.
    3. Concurrent Sweep 단계에서는 쓰레기를 정리하는 작업을 실행한다. 이 작업도 다른 스레드가 실행되고 있는 상황에서 진행한다.
  - CMS GC는 stop the world가 짧다는 장점이 있으나 아래의 단점이 존재한다.
    - 다른 GC 방식보다 메모리와 CPU를 더 많이 사용한다.
    - Compaction 단계가 기본적으로 제공되지 않는다.
- G1(Garbage First) GC
  - G1 GC는 Young 영역과 Old 영역에 대해서는 잊는 것이 좋다.
  - G1 GC는 바둑판의 각 영역에 객체를 할당하고 GC를 실행한다. 그러다가, 해당 영역이 꽉 차면 다른 영역에서 객체를 할당하고 GC를 실행한다.
    - 앞서 동작한 Young의 세가지 영역에서 데이터가 Old 영역으로 이동하는 단계가 사라진 GC 방식이다.
  - G1 GC의 가장 큰 장점은 성능이다. 지금까지 설명한 어떤 GC 방식보다도 빠르다.

[NAVER D2](https://d2.naver.com/helloworld/1329)

</details>


<details>
<summary>Package란 무엇이며 왜 사용할까?</summary>

<br>

패키지는 관련된 클래스 코드들을 모어서 관리하기 위해 사용한다.
패키지 분리를 통해 필요한 클래스 파일들을 쉽게 찾을 수 있으며, 각각의 프로젝트나 소프트웨어간의 코드 충돌을 방지할 수 있다. 또한 배포할 때 관련된 코드들을 묶어서 배포하고 재사용할 수 있다.

> 모든 패키지의 이름은 소문자로 관리하는 것이 관례이며 패키지 명은 일반적으로 도메인명을 사용하는 것이 관례이다.

</details>

<details>
<summary>String, Integer와 같은 클래스는 import 없이 어떻게 사용이 가능할까?</summary>

<br>

자바는 빌드를 하며 빌트인 패키지를 자동으로 import한다. String, Integer, System과 같은 클래스가 속해있는 java.lang은 해당 클래스에 해당하여 자동으로 import한다.

</details>


<details>
<summary>클래스와 인스턴스는 무엇이 다를까?</summary>

<br>

- 클래스는 인스턴스를 생성하기위한 template으로 클래스 자체만으로는 상태가 없다.
- 인스턴스는 클래스를 통해 실체화된 객체이다. 클래스와 다르게 실체화가 되었기에 상태를 갖고 있다.

</details>


<details>
<summary>인스턴스 필드/메서드와 클래스 필드/메서드는 무엇이 다를까?</summary>

<br>

- 인스턴스
  - 필드 - **인스턴스의 상태를 갖는 변수**를 인스턴스 필드라 한다.
  - 메서드 -  인스턴스가 생성된 이후에 호출이 가능하며 인스턴스의 상태(필드)를 변경하는 메서드를 의미한다.
- 클래스
  - 필드 - 여러 **인스턴스에서 공유하는 정보를 클래스 필드**라 한다. 즉, static 키워드가 붙은 공유되는 필드를 클래스 필드라 한다.
  - 메서드 - 클래스 메서드는 인스턴스 상태와 관련 없이, **인스턴스가 생성되지 않아도 호출이 가능한 클래스**를 뜻한다. 즉, static이 붙은 메서드를 클래스 필드라 한다.

</details>


<details>
<summary>JVM load와 unload에 대해 설명해주세요</summary>

<br>

JVM Load는 클래스가 필요한 시점에 동적으로 클래스의 바이트코드를 읽어 메모리에 할당하는 과정을 뜻한다.

JVM Unload는 클래스가 더 이상 사용되지 않아 메모리에서 클래스를 해제하는 과정을 의미한다.

</details>


<details>
<summary>new String()을 통한 문자열 선언</summary>

<br>

```java
String string1 = "abc";
String string2 = new String("abc");
```

위의 코드는 String class를 만드는 두가지 방법을 나타낸다. 두가지 방법은 보기에는 같은 결과가 나온다고 생각할 수 있지만 내부적으로는 다른 결과를 낸다. string1과 string2는 스트링 풀(String pool)에 있는 같은 객체를 바라보게 된다. 반면에 `new String()`을 통해 생성한 string3의 경우는 힙 메모리에 새로운 인스턴스를 만들어 관리를 하게 된다. 예시 코드를 작성하여 수행해보면 다음과 같은 결과가 나온다.

```java
public class StringTest {

	public static void main(String[] args) {
		String string1 = new String("abc");
		String string2 = new String("abc");

		System.out.println(string1 == string2); // false

		String string3 = "abc";
		String string4 = "abc";

		System.out.println(string3 == string4); // true
	}
}
```

위의 코드의 경우 `new String` 을 사용하여 새로운 인스턴스를 생성한 string1, string2의 경우는 서로 다른 주소값을 가르켜 false라는 결과를 반환한다. 반면에 스트링 풀의 주소만을 가르키며 생성한 string3, string4의 경우는 값이 같다는 결과가 나오게 된다.

</details>


<details>
<summary>String이 같은지 비교할 때는 동등성(equals) 비교를 왜 해야할까요?</summary>

<br>

```java
public class StringTest {

	public static void main(String[] args) {
		String string1 = "abc";
		String string2 = "abc";

		System.out.println(string3.equals(string4)); // true
	}
}
```

string1과 string2는 같은 객체를 바라본다는데 어째서 둘을 비교할 때 동일성(==)이 아닌 동등성(equals)으로 같은지 체크할까? Java8 이후로는 `String string1 = "abc"`와 같이 선언한 내용도 GC의 지시 대상이 되어서 다른 객체가 될 수 있다. 그래서 String 객체들의 비교는 동일성이 아닌 동등성으로 체크한다.

</details>


<details>
<summary>동일성과 동등성에 대해 설명해주세요</summary>

<br>

동일성(==)은 객체가 참조하고 있는 주소 값을 비교하는 것이며 동등성(equals)는 equals를 통해 정의된 값에 따라 비교를 하는 것이다. 객체들의 최상위 클래스 Object는 기본적으로 equals가 주소 값을 비교하는 동일성 체크와 동일하며여 우리는 객체의 equals재정의를 통해 내부 값이 같으면 두 객체가 동등하다고 판단할 수록 할 수 있다.

</details>


<details>
<summary>Equals & HashCode는 왜 재정의를 해야할까?</summary>

<br>

객체들의 최상위 클래스 Object는 기본적으로 equals가 주소 값을 비교하는 동일성 체크와 동일하며여 우리는 객체의 equals재정의를 통해 내부 값이 같으면 두 객체가 논리적으로 동등하다고 판단할 수록 할 수 있다.

그렇다면 HashCode는 왜 재정의를 해야할까?

Object의 명세서에는 `equals(Object)가 두 객체를 같다고 판단했다면, 두 객체의 hashCode는 똑같은 값을 반환해야 한다.` 라는 조항이 존재합니다. 이를 위해 우리는 equals를 재정의할 때는 hashCode도 반드시 재정의해야 한다.

</details>
