### 자바 17의 기능
---
자바 17이 출시되면서 오라클은  자바 어플리케이션의 보안성과 유연함을 강화시키기 위해  만들어진 새로운 기능인 Sealed Classes를 소개했다.

### 정의
---
Sealed Classes는 개발자들이 인터페이스 혹은 클래스의 계층적 상속을 제한할 수 있게 하는 기능이다. 다시 말하자면 클래스가 확장되고 선언되는 것을 좀 더 제어할 수 있게 해준다.

이해를 돕기 위해 아래의 Shape 클래스의 예제를 보자. Shape 클래스는 Circle, Square, Triangle 클래스로 확장될 수 있다. Sealed Classes에서는 Shape 클래스에서 오직 위에 언급한 세 클래스만을 확장(extended)할 수 있도록 할 수 있다. (= 다른 명칭의 클래스로 확장하여 사용할 수 없다.)

```java
public sealed class Shape permits Circlem Squarem Triangle {
	// 기능 정의
}
```

이 예제에서, 우리는 오직 Circle, Square,m, Triangle만 확장이 가능하도록 Shape 클래스를 정의했다.

### 좋은 점
---
Sealed Class(봉인된 클래스 , 동봉된 클래스)는 아래와 같은 장점이 있다.
1. 강화된 보안성 : 개발자가 클래스나 인터페이스를 제한하여 허용된 클래스만 접근할 수 있게 하여 보안성에 민감한 코드에서 접근을 막는다.
2. 향상된 유지보수 : 상속 계층을 제한함으로써 Sealed Class들은 코드를 쉽게 이해할 수 있고 수정도 쉽게 한다.
3. 향상된 성능 : Sealed Class는 JVM이 런타임에서 더욱 최적화 될수 있도록 하여 성능을 향상시킨다.

[출처 :  medium - Sealed Classes in Java 17 ](https://medium.com/@fullstacktips/sealed-classes-in-java-17-a22e4b0569e4)

#java 
#jdk17 