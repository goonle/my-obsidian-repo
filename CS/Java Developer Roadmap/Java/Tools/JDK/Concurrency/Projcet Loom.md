### What is Project Loom?
---
기존의 Java 쓰레드 처리방식의 비효율성을 탈피하고자 나온 JDK
사용 방식이 크게 다르지 않으나 내부적으로는 경량 스레드의 이점을 취할 수 있음

#### 기존 스레드의 문제점
- 기존의 스레드는 OS가 제공하는 쓰레드이기 때문에 무겁다
	- 무겁다
		- A.리소스 부하가 많다
		- B.동시성 작업 단위가 크다
		- C.선점형 스케쥴러다
##### A.리소스 부하가 많다.
- 서버당 수천개만 만들수 있으나 소켓은 수백만개를 만들 수 있다.  
##### B.동시성 작업 단위가 크다.
- 스레드가 무겁기에 재활용하려하는데 어플의 특성에 따라 동시성의 작업단위가 다르다.
##### C. 선점형 스케쥴러다
- 스케쥴 담당을 OS가 한다.


[참고주소 : Project-Loom 은 새로운 패러다임일까? ](https://velog.io/@recordsbeat/Project-Loom-%EC%83%88%EB%A1%9C%EC%9A%B4-%ED%8C%A8%EB%9F%AC%EB%8B%A4%EC%9E%84%EC%9D%BC%EA%B9%8C)



#java-developer-roadmap
#java 
#jdk
#concurrency
