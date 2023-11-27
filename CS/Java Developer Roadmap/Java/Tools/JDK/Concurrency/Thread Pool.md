
> 프로세스 중 병렬 작업처리가 많아지면 스레드의 개수가 증가하고 그에 따른 스레드 생성과 스케쥴링으로 인해 CPU가 바빠지며 메모리 사용량이 늘어난다. 따라서 시스템 성능이 저하되고 갑작스러운 병렬작업의 폭증에 스레드 폭증을 막으려면 Thread Pool을 사용해야 한다.

### Thread Pool
---
작업처리에 사용되는 스레드를 제한된 개수만큼 정해두고 작업 Queue에 들어오는 작업들을 하나씩 처리한다.

Java에서는 Thread Pool을 생성하고 사용할 수 있도록 java.util.concurrent.Executors 클래스와 java.util.concurrent.ExecutprService 인터페이스를 제공한다.



#java-developer-roadmap
#java 
#jdk
#concurrency
