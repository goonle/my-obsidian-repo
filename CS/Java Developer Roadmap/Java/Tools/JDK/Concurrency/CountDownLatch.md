
CountDownLatch는 어떤 쓰레드가 다른 쓰레드에서 작업이 완료될 때까지 기다릴 수 있도록 해주는 클래스입니다.

1. 예를 들어, Main thread에서 5개의 쓰레드를 생성하고 어떤 작업을 병렬로 처리되도록 할 수 있습니다. 이 때, Main Thread는 다른 쓰레드가 종료되는 것을 기다리지 않고 다음 코드(statements)를 수행합니다. 여기서 CountDownLatch를 사용하면 다음 코드(statements)를 실행허지 않고 기다리도록 만들 수 있습니다.

2. 어떤 작업을 처리하는데 CPU 리소스가 많이 필요하지 않기 때문에 Main thread에서만 처리하도록 할 수 있습니다. 하지만 어떤 프로세스가 실행도기를 기다리거나 Network 등의 외부에서 어떤 이벤트가 발생하길 기다린다면, 그런 이벤트가 발생하지 않았을 떄 무한히 기다리게 될 수도 있습니다. 이럴 때, 다른 Thread에서 이 작업을 수행하도록 ㅎ하고 Main Thread는 일정 시간을초과하면 작업을 기다리지 않도록, Timeout을 설정할 수 있습니다.

#java-developer-roadmap
#java 
#jdk
#concurrency
