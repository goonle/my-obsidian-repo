[출처 : velog - tkadks123 - Java NIO에 대해 알아보자](https://velog.io/@tkadks123/Java-NIO%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90-12)
[출처: brunch - myner - 자바 NIO의 주요 키워드](https://brunch.co.kr/@myner/47)
### NIO (New Input Output)
---
기존 Java IO를 개선하기 위해 나온 패키지

C/C++처럼 직접 메모리를 관리하고 운영체제 수준의 시스템 콜을 직접 사용할 수 없기 때문에 커널 버퍼에서 JVM 내부의 Buffer로 한번 더 데이터를 옮겨주는 과정이 생기면서 발생하는 문제점인 JVM 내부 버퍼로 복사시 발생하는 CPU  연산, GC 관리, IO 요청에 대한 스레드 블록이 발생하는 현상 떄문에 효율이 좋지 못한 점을 개선하기 위해 나온 패키지이다.

-> 직접 메모리 관리를 할 수 없기에 생기는 연산 때문에 비효율적인 부분을 개선한 패키지

### IO vs NIO
---
- NIO는 양방향 입출력이 되는 Channel이라는 것을 사용한다.
	- 입력과 출력을 구분하기 위한 별도의 채널을 만들 필요가 없다
	- IO는 입력과 출력 ( InputStream , OutputStream)을 만들어 사용한다.
- NIO는 버퍼를 사용한다.
	- 버퍼를 사용하면 복수개의 바이트를 한번에 읽어 빠르다
	- IO는 사용안한다
	- 버퍼를 사용하면 별도 저장 없이 읽은 데이터의 위치를 이동할 수 있다.
- NIO는 채널을 관리하는 Selector라는게 있다.
	- IO를 사용시 클라이언트(일반적으로 브라우저) 하나당 스레드 하나를 생성하지만
	- NIO는 Channel을 사용하기 때문에 하나의 스레드로 여러개의 처리를 할 수 있다.
- NIO의 buffer 사용의 용량은 작다
	- 입출력이 빈번하고 하나의 작업이 빠른 경우 NIO가 효과적이다.


#java-developer-roadmap
#java 
#jdk
#io
