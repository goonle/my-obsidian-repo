[원문출처 : testbook.com](https://testbook.com/key-differences/difference-between-throw-and-throws-in-java)

자바에서, throw 와 throws 라는 용어는 예외처리를 위해 자주 사용된다. 하지만 각자 다른 상황에서 다른 목적으로 사용된다. 'throws'라는 키워드는 하나의 매소드가 잠재적으로 예외를 만들어 낼 수 있음을 선언할 떄 사용하는 반면에 'throw'라는 키워드는 블록 단위의 코드 안에서 혹은 매소드 안에서 예외를 표시하기 위한 단어이다. 이 차이는 자바에서 예외처리를 위해 굉장히 중요하다.

#### 자바에서 Throw 와 Throws의 차이 살펴보기
| 요소             | Throw                                                               | Throws                                                                                                   |
| -------------- | ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| 목적             | throw라는 키워드는 블럭 혹은 매소드 단위의 코드에서 예외를 표시하기 위해 사용된다.                   | throws라는 키워드는 매소드를 선언할 때 해당 매소드가 잠재적으로 예외처리가 사용될 수 있음을 선언할 떄 사용한다.                                       |
| 사용             | throw라는 키워드는 오직 한번에 하나의 예외처리를 할 때 사용된다. 여러 개의 예외처리를 순차적으로 할 수 없다.   | throws는 여러개의 예외처리를 한번에 선언할 수 있다.                                                                         |
| Exception type | throw는 체크되지 않은 예외처리만을 전파할 수 있다. 다시말해서 체크된 예외처리는 throw를 통해 전파할 수 없다. | throws는 체크되거나 체크되지 않은 둘 모두의 예외처리에 사용될 수 잇습니다. 체크된 예외처리에서 throws는 특정 이름의 exception 클래스의 이름과 함께 사용되어야 합니다. |
| 문법             | throw는 인스턴스 변수로 사용됩니다.                                              | throws는 exception 클래스의 이름으로 사용됩니다.                                                                       |
| 사용처            | 매소드의 안에 있어야 합니다.                                                    | 매소드의 선언에 사용되어야 합니다.                                                                                      |

### Checked exception과 Unchecked exception
---
[출처 : rollbar](https://rollbar.com/blog/how-to-handle-checked-unchecked-exceptions-in-java/)

![[Pasted image 20240313193112.png]]

#java 
#throws
#throws 
#exception 