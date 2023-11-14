[출처 : woolbro.tistory.com](https://woolbro.tistory.com/29)
### Server Socket API
---
ServerSocket의 클래스는 서버 프로그램을 구현하는데 사용됩니다. 일반적인 서버 프로그램의 과정은 Step 1 ~ Step 6으로 나눌 수 있습니다.

1. 서버 소켓 생성, 포트 바인딩
2. 클라이언트로부터의 연결을 기다리고 (Connect Listen) 요청이 오면 수락
3. 클라이언트 소켓에서 가져온 InputStream(클라이언트 쪽에서는 OutputStream)을 읽음
4. 응답이 있다면, OutputStream을 통해 클라이언트에 데이터를 보냄
5. 클라이언트와의 연결을 닫음.
6. 서버 종료

사용 목적이나 용도에 따라 3~4단계는 반복될 수 있다.

#### 예제의 순서
---
> Create a Server Socket -> Listen for a connection ->  Read data from the client -> Send Data to the Client -> Close the client Connection -> Terminate the Server 

#### Step 1. Create a Server Socket
작성중