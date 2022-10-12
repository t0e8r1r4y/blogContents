# JAVA Junit

## JUnit에 대하여

### 1. JUnit이란

- 자바 프로그래밍 언어용 유닛 테스트 프레임워크
- given, when, then 구조에 맞춰서 코드를 작성하고 테스트를 보통한다.

### 2. JUnit4와 JUnit5

- JUnit5 = ***JUnit Platform* + *JUnit Jupiter* + *JUnit Vintage***
    
    ![%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-10-12_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_8 46 46](https://user-images.githubusercontent.com/91730236/195222270-ac81d331-6838-445d-ba6b-c2031c3c5a92.png)
    
- Jupiter는 프로그래밍 모델과 실행 모델의 조합이라는데, 요약하면 테스트가 엔진위에서 `어떻게 동작할지 정의(프로그래밍 모델)` `어떻게 실행할지(실행 모델)`를 테스트 코드를 보고 결정한다.
- Vintage는 Jupiter에서 정의한 테스트를 실행하는 엔진이다.
- JUnit5 이점은 아래 3가지다.
    - 필요한 것만 import하여 사용이 가능하다.
    - 실행하는 runner를 복수로 띄워 테스트가 빠르다.
    - 자바 8의 특징에 더 잘 맞게 만들었다.
- JUnit4와 JUnit5는 실행구조의 차이로인해 코드작성도 차이가 생긴다. 따라서 JUnit4 코드 중 일부는 마이그레이션이 필요할 수 있다. 또한 maven, gradle 버전에 따른 에러가 발생할 수 있으니 공식문서를 반드시 확인해야 한다.
    - [공식 Doc](https://junit.org/junit5/docs/current/user-guide/#migrating-from-junit4)
    - [예시](https://www.baeldung.com/junit-5-migration)
    - [마이그레이션 샘플 코드](https://github.com/junit-team/junit5-samples)

## Mockito에 대하여

### 1. Mockito란

- Mockito란 단위 테스트를 위한 Java Mocking Framework이다. JUnit에서 수행할 모듈과 연결되는 외부의 다른 모듈을 흉내내는 `가짜 모듈을 생성`하여 테스트를 효율적으로 하기위해서 사용하는 객체이다.

### 2. Mock과 Spy

- Mock Annotation을 사용하게 되면 흉내내는 모듈의 `껍데기`만 만든다. 해당 내용의 구체적인 로직은 생성되지 않는다.
- Spy Annotation을 사용하게 되면 실제 로직의 모든 기능을 가지고 있는 `완전한 객체`이다. spy는 일부 필요한 로직에 대해서 stub(재정의)하여 사용이 가능하다. 재정의 하지않으면 실제 로직의 결과를 return 한다.
- 대체로 Mock을 사용하는 것을 많이 권장하며, 외부라이브러리를 이용한 테스트에는 Spy를 사용한다.

<aside>
🔥 Service에서 사용하는 외부 라이브러리는 두 종류가 있다. dependency를 추가하여 사용하는 진짜 외부 라이브러리, 그리고 사용자가 정의한 외부 Service 등 두가지다.

사용자가 정의한 외부 Service의 경우는 Mock을 사용하는 것이 좋아보인다. 사용자가 정의한 외부 Service는 return이 명확하다. 그러기에 Mock한 객체가 return하는 것이 명확하므로 테스트하고자 하는 Service 흐름만을 명확하게 테스트가 가능하다.

그러나 dependency로 추가한 외부 라이브러리는 정확한 결과를 알 수 없으며, API 요청 같은 경우 네트워크 에러 등이 발생할 수 있기때문에 spy가 유리 할 수 있다.

</aside>

### 3. 코드 사용 방법

- Mockito 클래스의 mock 메서드를 사용하여 mock 객체를 생성하는 방법
- Mock 어노테이션을 사용하는 방법
- Mock 객체를 생성하고 InjectMocks 어노테이션을 사용하여 mock 대상에 해당 객체를 주입하는 방법
- Spy로 객체를 생성하고 수정이 필요한 부분만 stub하여 사용

<aside>
🔥 사용하는 과정에서 객체를 주입하는게 처음에 굉장히 헷갈린다. 그 의존성 주입의 Target이 무엇인지 확인 필요하다.

</aside>

### 4. 의존성 주입이 헷갈리는 부분

- 아래 내용으로 코드를 쓰면 에러가 발생한다. MockBean은 mock 객체를 스프링 컨텍스트에 등록한다. 그러나 InjectMocks는 스프링 컨텍스트에서 의존성을 찾지 않는다.
- 이럴 경우에는 Autowired 어노테이션을 사용하여 스프링 컨텍스트에서 Mock 된 객체를 찾아와야 한다.

```java
@SpringBootTest
public class Test {

	@MockBean
	private TestRepository testRepository;

	@InjectMocks
	private TestService testService;

	@Test
	public void testFunction1() {
		...
	}
}
```

- SpyBean도 동일하다. 이렇게 사용해야 한다.

```java
@SpringBootTest
public class Test {

	@SpyBean
	private TestRepository testRepository;

	@Autowired
	private TestService testService;

	@Test
	public void testFunction1() {
		...
	}
}
```

- 테스트에 문제가 되는 부분 중 하나가 autowired 어노테이션이다. 의존성을 주입할 때 스프링 컨텍스트에서 가져오는데, 테스트 과정에서는 다른 컨텍스트 영역에서 의존성을 주입하려고 할 수 있기 때문에 테스트 에러에서 한번쯤 의심해야 한다.

---

### 참고자료

- [JUnit5 (JUnit4)와 비교](https://jade314.tistory.com/entry/Junit-5)
- [Mockito 사용 예시](https://cobbybb.tistory.com/16)
