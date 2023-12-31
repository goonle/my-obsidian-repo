[출처 : baeldung - Functional Programming in Java - witten by Kumar Chandrakant](https://www.baeldung.com/java-functional-programming)

### What is Functional Programming?
---
기본적으로 functional programming은 컴퓨터 프로그래밍 작성 스타일 중 하나로 연산작업들으 수학적 기능으로 평가하는 것을 말합니다.

수학에서 기능은 입력과 출력의 상관관계를 표현합니다.

중요한 것은, 기능(function)의 결과는 오직 입력에 달렸다는 것입니다. 흥미로운 것은 우리가 두개 혹은 더 많은 기능들을 함께 사용하여 새로운 기능을 만들 수 있다는 것입니다.

### 함수형 프로그래밍
---
#### 프로그래밍 패러다임
프로그래밍 패러다음인 프로그래머에게 프로그래밍 관점을 갖게 하고 코드를 어떻게 작성할지 결정하는 역할을 한다. 새로운 프로그래밍 패러다임을 통해서는 새로운 방식으로 생각하는 법을 배우게 되고, 이를 바탕으로 코드를 작성하게 된다.

#### 최근까지의 패러다임
1. 명령형 프로그래밍 : 무엇을 할지 나타내기보다 어떻게 할지를 설명하는 방식
	- 절차지향 프로그래밍 : 수행되어야 할 순차적인 처리 과정을 포함하는 방식 (C, C++)
	- 객체지향 프로그래밍 :객체들의 집합으로 프로그램의 상호작용을 표현 (C++, Java , C#)
2. 선언형 프로그래밍 : 어떻게 할 지를 나타내기보다 무엇을 할 것인지를 설명하는 방식
	- 함수형 프로그래밍 : 순수 함수를 조합하고 소프트웨어를 만드는 방식 (클로저, 하스켈, 리스프)

#### 함수형  프로그래밍의 등장
명령형 프로그래밍을 기반으로 개발했던 개발자들은 개발하는 소프트웨어의 크기가 커짐에 따라, 복잡하게 얽혀있는 스파게티 코드를 유지보수하는 것이 매우 힘들다는 것을 깨닫게 되었다. 그리고 이를 해결하기 위해 함수형 프로그래밍이라는 프로그래밍 패러다임에 관심을 갖게 되었고 함수형 프로그래밍은 거의 모든 것을 순수 함수로 나누어 문제를 해결하는 기법으로, 작은 문제를 해결하기 위한 함수를 작성하여 가독성을 높이고 유지보수를 용이하게 해준다.

> [!quote] 
> "Functional Programming is programming without assignment statement"
> - Rober C.Martub (Clean Code의 저자)

#### 함수형 프로그래밍에 대한 이해
대입문을 사용하지 않는 프로그래밍이며, 작은 문제를 해결하기 위한 함수를 작성한다.






#java-developer-roadmap
#java 
#jdk
#io
