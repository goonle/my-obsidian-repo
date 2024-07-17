Java 객체지향 디자인 패턴 - 104p ~ 111p
# 단일 책임 원칙 - Single Responsibility Principle(SRP)

객체지향 **설계**관점에서 책임의 기본 단위는 객체를 지칭한다. 예측하지 못한 변경사항이 발생하더라도 유연하고 확정성이 있도록 시스템의 구조를 설계하기 위해 객체는 가장 잘할 수 있는 기능만을 가지는 것이 좋다.

객체가 기능을 많이 가지고 있을 때, 코드에 변경사항이 온다면 직접적이 관계가 없더라도 모든 코드를 다시 테스트 해야한다. 이를 *회귀 테스트*라고 한다. 이런 회귀 테스트를 최소화하기 위해서는 하나의 객체가 하나의 기능만을 가지고 있을 때 가능하다.

### 1. 결합도 낮추기
아래와 같은 객체가 있다고 하자.

```java
public class Student{
	public 수강과목_조회(){}
	public 신입생_정보_DB_기록(){}
	public 성적표_출석부(){}
}
```

이 객체가 하나의 책임을 가지기 위해서는 책임의 분리가 필요하다.
```java
// Student 클래스는 학생의 기본 정보만을 담는 역할을 합니다.
public class Student {
}

// 수강 과목 조회를 담당하는 클래스
public class CourseEnrollment {
    public void 수강과목_조회(Student student) {
        // 수강 과목 조회 로직
    }
}

// 신입생 정보를 DB에 기록하는 클래스
public class StudentDatabase {
    public void 신입생_정보_DB_기록(Student student) {
        // DB 기록 로직
    }
}

// 성적표와 출석부 관리를 담당하는 클래스
public class StudentReport {
    public void 성적표_출석부(Student student) {
        // 성적표 및 출석부 로직
    }
}

```

이런 책임의 분리는 *결합도*를 낮춘다.

### 2. 응집도 높이기
하나의 책임(기능)이 여러 개의 클래스로 나누어져 있을 경우에도 단일 책임 원칙을 통해 설계해야 한다. 하나의 로직(Logic A)이 여러 개 의 로직(Logic B,C,D,E)으로 이루어져 있을 경우, 로직 B가 수정이 된다면 B를 참조하는 모든 코드를 찾아내 수정을 해야 오류가 없을 수 있다. 이는 산발적으로 흩어진 모든 코드를 수정해야 하기 때문에 많은 집중도가 요구된다.

이 경우, 부분적인 로직을 별개의 클래스로 분리하여 사용한다면 로직이 변경되었을 때, 클래스 안의 코드만 변경이 되면 return하는 데이터의 형식이 맞다면 일일이 찾아서 수정할 필요가 없어진다. 이는 공통된 책임을 모은다고하여 응집도라고 표현한다.

### 3. 관심지향 프로그래밍과 횡단 관심 문제
*횡단 관심 문제*는 앞서 말했던 응집도를 높이기 위한 예제에 나온 흩어진 로직을 뜻한다. 대표적인 예로는 로깅(logging), 보안(security), 트랜젝션 관리(transaction management) 등이 있다.

> [!info] 
> 관심지향 프로그래밍(Aspect-Oriented Programming : AOP)는 횡단 관심을 수행하는 코드를 애스팩트(Aspect)라는 특별한 객체로 모듈화 하고 위빙(weaving)이라는 작업을 통해 모듈화한  코드를 핵심기능에 끼워넣을 수 있다. 

##### 3-1. 용어
1. 횡단 간심사
	- 로깅, 보안, 트렌젝션 관리 등과 깉이 여러 모듈이나 클래스에 걸쳐 공통적으로 필요로 하는 기능
2. 에스펙트
	- 횡단 관심사를 모듈화한 특수한 객체
	- 로깅, 보안, 트렌젝션 등
3. 조인 포인트
	- 애스펙트가 적용될 수 있는 프로그램 실행 시점
		- 메서드 호출, 실행, 클래스 초기화, 객체 생성 시점등이 있다. (설정이 가능하다)
4. 포인트 컷
	- 특정 조인 포인트를 선택하는 표현식
5. 어드바이스
	- 애스펙트가 조인 포인트에서 수행할 동작을 정의한 코드
	- 예를 들면 매서드를 실행하기 전에 권한 검사를 수행하는 것
6. 위빙
	- 애스펙트를 핵심 기능에 적용하는 과정
	- 컴파일 시, 로드 시, 런타임 시 위빙이 이루어질 수 있다.

##### 3-2. 예제
1. 핵심 로직 클래스
``` java
public class StudentService {
    public void enrollCourse(String studentId, String courseId) {
        // 수강 신청 로직
        System.out.println("Student " + studentId + " enrolled in course " + courseId);
    }
}
```

2. 애스팩트 클래스
```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;

@Aspect
public class LoggingAspect {

    @Before("execution(* StudentService.enrollCourse(..))")
    public void logBefore() {
        System.out.println("A method is about to be called");
    }
}
```

3. Spring 설정 파일
```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/aop
           http://www.springframework.org/schema/aop/spring-aop.xsd">

    <bean id="studentService" class="com.example.StudentService"/>
    <bean id="loggingAspect" class="com.example.LoggingAspect"/>
    
    <aop:config>
        <aop:aspect id="logAspect" ref="loggingAspect">
            <aop:pointcut id="logPointcut" expression="execution(* com.example.StudentService.enrollCourse(..))"/>
            <aop:before method="logBefore" pointcut-ref="logPointcut"/>
        </aop:aspect>
    </aop:config>
</beans>
```

AOP 설정 부분을 보면 aspect를 정의할 때 어떤 클래스를 언제 사용할 지를 작성합니다.
### 설명

- **핵심 비즈니스 로직 클래스**: `StudentService` 클래스는 수강 신청 로직을 포함한 핵심 기능을 담당합니다.
- **애스펙트 클래스**: `LoggingAspect` 클래스는 메서드가 호출되기 전에 로깅을 수행하는 횡단 관심사를 정의합니다.
- **포인트컷**: `execution(* StudentService.enrollCourse(..))` 표현식은 `StudentService` 클래스의 `enrollCourse` 메서드가 호출될 때를 지정합니다.
- **어드바이스**: `logBefore` 메서드는 지정된 포인트컷에서 실행될 동작을 정의합니다.
- **위빙**: Spring 설정 파일을 통해 로깅 애스펙트가 핵심 비즈니스 로직에 적용됩니다.

### 실행 순서

1. **Spring 컨텍스트 초기화**: Spring 컨텍스트가 초기화되면 `applicationContext.xml`에 정의된 빈(bean)들이 로드되고 초기화됩니다. 여기에는 `studentService`와 `loggingAspect` 빈이 포함됩니다.
    
2. **위빙(Weaving)**: Spring AOP 설정에 따라 `StudentService` 클래스의 `enrollCourse` 메서드에 대해 정의된 `LoggingAspect`가 적용됩니다. 이 과정은 런타임 시에 일어나며, `@Before` 어드바이스가 `enrollCourse` 메서드 호출 전에 실행되도록 설정됩니다.
    
3. **메서드 호출**: 클라이언트 코드에서 `StudentService` 클래스의 `enrollCourse` 메서드를 호출합니다.
```java
StudentService studentService = context.getBean(StudentService.class);
studentService.enrollCourse("12345", "CS101");
```
    
4. **조인 포인트 실행**: `enrollCourse` 메서드가 호출될 때, AOP 설정에 따라 이 메서드 호출 지점이 조인 포인트로 간주됩니다.
    
5. **포인트컷 매칭**: AOP 프레임워크는 `execution(* StudentService.enrollCourse(..))` 포인트컷 표현식이 `enrollCourse` 메서드 호출과 매칭되는지 확인합니다.
    
6. **어드바이스 실행**: 매칭되는 경우, `LoggingAspect` 클래스의 `logBefore` 메서드가 먼저 실행됩니다.
```java
// LoggingAspect의 logBefore 메서드 실행
System.out.println("A method is about to be called");
```
    
7. **핵심 비즈니스 로직 실행**: 어드바이스가 실행된 후, 원래의 `enrollCourse` 메서드가 실행됩니다.
```java
// StudentService의 enrollCourse 메서드 실행 
System.out.println("Student " + studentId + " enrolled in course " + courseId);`
```
```cmd
Student 12345 enrolled in course CS101
```

#solid
#SRP
