### CompletableFuture에 대한 이해
---
#### Future의 단점 및 한계
java 5 에 future가 추가되면서 비동기 작업에 대한 결과 값을 반환 받을 수 있게 되었다. 하지만 Futrure은 다음과 같은 한계를 지닌다
- 외부에서 완료시킬 수 없고, get 의 타임아웃 설정으로만 완료가 가능
- 블로킹 코드(get)를 통해서만 이후의 결과를 처리할 수 있음
- 여러 Future을 조합할 수 없음
- 여러 작업을 조합하거나 예외처리할 수 없음

#### Completable Future 클래스
CompletableFuture는 기존의 Future기반으로 외부에서 완료시킬 수 있어 CompletableFuture라는 이름을 같게 되었다. Future 외에도 CompletableStage 인터페이스도 구현하고 있는데, CompletionStage는 작업들을 중첩시키거나 완료 후 콜백읠 위해 추가되었다. 예를 들어  Future에서는 불가능했던 "몇 초 이내에 응답이 안오면 기본값을 반환한다." 와 같은 작업이 가능해 진것이다. 즉, Future으ㅟ 진화된 형태로써 외부에서 작업을 온려시킬 수 있을 뿐만 아니라 콜백 등록 및 Future 조합등이 가능해졌다