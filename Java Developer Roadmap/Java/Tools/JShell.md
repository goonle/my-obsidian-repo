
---
- Java 프로그래밍 합습과 Java 코드 프로토타이핑을 위한 대화식 도구
- hell에 선언문, 식(Expression), 문(Statement) 및 JShell 명령을 입력하면, 즉시 입력이 평가되고 그 결과(Feedback)가 출력
- Java9에 추가됨

#### JShell은 왜 필요한가?
---
- 코드 실행과 옵션 탐색이 매우 편리
-  메서드의 다양한 옵션을 시험해볼 수 있으며, 익숙하지 않은 API를 실험할 수 있음
```java
% jshell
|  Welcome to JShell -- Version 9
|  For an introduction type: /help intro
jshell>
```

```java
jshell> int x = 45
x ==> 45
|  created variable x : int
```
