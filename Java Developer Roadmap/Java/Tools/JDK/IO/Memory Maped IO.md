[출처 : 코드연구소- (운영체제) Memory Mapped I/O 와 I/O Mapped I/O 란?](https://code-lab1.tistory.com/204)

>[!info]
>Memory Mapped I/O 는 마이크로프로세서(CPU)가 입출력 장치를 접근할 떄, 입출력 메모리의 주소 공간을 분리하지 않고 하나의 메모리 공간에 취급하여 배치하는 방식이다. -Wikipedia
>

### Memory Mapped I/O vs I/O Mapped I/O
---
Memory Mapped I/O는 메모리의 일부 공간에 I/O 포트를 할당하고 제한적인 사용이 가능하지만 빈번한 작은 입출력에 효과적이다.

### Memory Mapped I/O in Java
---
[출처 : geeksforgeeks - What is memory mapped file in Java]
위의 글은 OS의 Memory Mapped I/O 였다. 그렇다면 Java에서는 어떤 것일까?

Memory-mappped file들은 자바에선 메모리에서 바로 내용에 접근 가능한 파일들이다. 자바 프로그래밍은 java.nio 패키지를 통해 Memory-mapped file을 지원한다. [[Java NIO]]  
Memory-mapped I/O는 사용자의 파일 시스템 페이지로 부터 직접적으로 매핑하는 가상 메모리를 만들어 파일 시스템을 사용한다. 단순히 커다란 배열로 생각할 수 있다. 메모리는 Memory-mapped file을 읽는 메모리는 Java Heap 영역 밖에 있다.

우리는 MappedByteBuffer를 사용해 메모리에서 읽고 쓰는 것응ㄹ 사용한다. 이 유틸리티는 효과적인 Memory-mapped file들을 만들고 저장할 수  있도록 사용된다. MemoryByteBuffer에 대한 몇몇 주요 특징을 적어본다.
1. MappedByteBuffer와 파일 매핑은 garbage가 collect 될 때 까지 유효하다. sun.misc.Cleaner는 아마도 Memory-mapped  file들을 지울 수 있는 유일한 옵션일 것이다.
2. Memory-mapped file에서 읽기와 쓰기는 보통 디스크에 내용을 작성하는 운영 시스템이 주로 한다.
3. 더 나은 성능을 위해 Direct buffer를 Indirect Buffer보다 선호합니다.
4. 파일을 읽는 메모리는 자바 힙 영역 밖에 있고 파일에 접근하는 두가지 방법을 제공하는 공유 메모리에 위치합니다. 하지만 이것은 사용자의 사용 버퍼에 달려있습니다