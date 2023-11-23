[출처: Oracle docs : Class Optional <T](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Optional.html)
---
이 객체의 컨테이너는 null 값이 아닌 값을 가지거나 가지고 있지 않다. 만약 값이 존재하면 isPresent()는 true를 반환한다. 이 객체의 값이 없다면 , 빈 객체라면 isPresent()는 false를 반환한다.

들어있는 값의 존재와 부재에 달려있는 추가적인 매소드들도 제공된다. 예를 들면 orElse() (값이 없을 경우 기본 값을 반환하는 기능) 과 ifPresent() (값이 존재한다면 행위를 실행하는 기능) 등이 있다.

이것은 value-based 클래스이다; 프로그래머들은 동등한 인스턴스를 상호교환 할 수 있도록 다뤄야 하며, 동기화를 위해 인스턴스를 사용해선 안되며 그렇지 않으면 예측할 수 없는 동작이 발생할 수 있습니다. 예를 들면, 추후 릴리즈에서 동기화는 실패할 수도 있습니다.


---

### [출처 : 메이쁘 (블로그) -### JAVA8 Optional Class에 대한 정의 및 사용방법 ](https://maivve.tistory.com/332)
---
#### 사용이유
NPE(NullPointerException)을 방지하기 위해 사용하는 클래스. null이 들어올 수 있는 값을 한번 감싸는 Wrapper Class
Generic Type이 있어 필요한 값의 클래스를 지정할 수 있다.
Optional Class를 통해 null 이 들어와도 NPE가 발생하지 않게 해준다.

#jdk #Optional
#class
