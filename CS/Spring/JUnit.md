
### JUnit이란?
---
자바용 테스트 툴이다.
>[!info]
>1. 테스트 방식을 구분할 수 있는 어노테이션을 제공
>2. @Test 어노테이션으로 메서드를 호출할 때마다 새 인스턴스를 생성
>3. 독립 테스트 가능
>4. 예상 결과를 검증하는 어썰션 매서드 제공
>5. 사용방법이 단순하여 코드 작성 시간이 적음
>6. 자동 실행, 자체 결과를 확인하고 즉각적인 피드백을 제공

#### TL ; DR (Too Long ; Didn't Read) : 너무 길어서 안 읽었다.
- 간단하여 작성시간이 짧다.
- 직관적이다.

### 예제 코드1
---
```java
public class JUnitCycleTest {
	@Test
	public void test1() {
		System.out.println("test1");
	}
}
```

Eclispse  기준으로 우클릭 후 JUnit으로 실행하면 결과가 확인된다.

### 예제 코드2
---
```java
public class JUnitCycleTest {
	@BeforeAll // 전체 테스트를 시작하기 전에 1회 시작함으로 매서드는 static으로 선언
	static void beforeAll() {
		System.out.println("@BeforeAll");
	}
	@BeforeEach // 테스트 케이스를 시작하기 전마다 실행
	public void beforeEach() {
		System.out.println("@BeforeEach");
	}
	@Test
	public void test1() {
		System.out.println("test1");
	}
	@Test
	public void test2() {
		System.out.println("test2");
	}
	@AfterAll
	static void afterAll() {
		System.out.println("afterAll");
	}
	@AfterEach
	public void afterEach() {
		System.out.println("afterEach");
	}
}
```

#### 의문점
---
>[!faq]
>왜 @Test 어노테이션은 public일까?

코드를 복사 붙여넣기를 해서 테스트를 작성해보니 테스트 실패가 되었다. 
왜 였을까? 이유는 public을 써야하는 곳에 static을 쓰고 static을 써야하는 곳에 public을 써서였다.

단순히 궁금해서 찾다보니 다음의 구글 대화를 찾을 수 있었다.
[구글 대화 : JUnit의 테스트 메소드는 왜 public이어야 할까요?](https://groups.google.com/g/ksug/c/xpJpy8SCrEE?pli=1)

#### TL ; DR
여기엔 개발자들이 생각하는 관념적인 이유와
실제 이유가 있다.

###### 실제 이유
처음 개발할 당시 public만 받아서 관례적으로 이어져오고 있다.
###### 개발자들의 생각
테스트는 모두가 확인해야 하기 때문에, 실제 코드 변환에 쉬워서


#java 
#junit 
#test