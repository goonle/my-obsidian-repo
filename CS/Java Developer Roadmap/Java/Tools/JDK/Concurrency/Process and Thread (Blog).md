
### 프로세스란?
---
- 실행중인 프로그램
- 프로세스 = 프로그램 + 프로세스 제어블록
- 프로세스는 각각 독립된 메모리 영역(Code, Data, Stack, Heap의 구조)을 할당 받는다.

### 쓰레드란?
---
- 프로세스 내에서 각가 Stack만 따로 할당받고 code, Data, Heap영역은 공유한다.
- 주소공간이나 자원들을 같은 프로세스 내의 스레드끼리 공유하면서 실행된다.
- 같은 프로세스 안에 있는 여러 스레드들은  같은 힙 공간을 공유한다.

### Java 쓰레드란?
---
- 일반 스레드와 거의 차이가 없으며, JVM이 운영체제의 역할을 한다
- 자바에는 프로세스가 존재하지 않고 스레드만 존재하며, 자바 스레드는 JVM에 의해 스케쥴 되는 실행 단위 코드 블록이다.

### Java에서의 스레드 구현과 실행
---
- 쓰레드를 구현하는 방법은 Thread 클래스를 상속받는 방법과 Runnable 인터페이스를 구현하는 방법, 모두 두 가지가 있다.
- Thread 클래스를 상속받으면 다른 클래스를 상속받을 수 없기 때문에, Runnable 인터페이스 구현이 일반적이다.

##### 1. Thread 클래스를 상속
```java
class MyThreead extends Thread {
	public void run(){
		//작업내용
	}
}
```

##### 2. Runnable 인터페이스를 구현
```java
public class Test2 implements Runnable {
	@Override
	public void run(){
		//작업내용
	}
}
```

### Thread 예제
---
```java
class ThreadEx1_1 extends Thread {
	@Override
	public void run(){
		for(int i =0 ; i <5 ; ++i){
			System.out.println(getBane());
		}
	}
}

class ThreadEx2_2 implements Runnable {
	@Override
	public void run(){
		//Thread.currentThread() - 현재 실행죽인 Thread를 반환한다.
		System.out.println(Thread.currentThread().getName());
	}
}

public class Test2 {
	public static void main(String[] args) {
		ThreadEx1_1 t1 = new ThreadEx1_1();
		
		Runnable r = nbbew ThreadEx2_2();//Thread의 자손 클래스의 인스턴스 를 생성
		Thread t2 = new Thread(r);//생성자 Thread(Runnable target)

		Thread t3 = new Thread(new ThreadEx2_2());// 위 두줄을간단히
	}
}
```

### 결론
---
넘어가자


#java-developer-roadmap
#java 
#jdk
#concurrency
