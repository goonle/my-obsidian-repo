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
---
![[Pasted image 20231116185513.png]]
다음 생성자를 사용해서 ServerSocket 클래스의 객체를 만든다.
```java
- ServerSocket(int port) :지정된 포트 번호에 바인딩 된 서버 소켓을 만듦 (최대 50)
- ServerSocket(int port, int backlog) :지정된 포트 번호에 바인드 된 서버 소켓을 만들고 대기중인 최대 얀걀수를 backlog 매개뱐수로 고정 
- ServerSocket(int port, int backlog, InetAddress bibddAddr) : 서버 소켓을 만들고 지정된 포트 번호와 로컬 IP주소에 바인딩 
```

```java
1. 초기화
ServerSocket serverSocket = new ServerSocket(8000);

2. Listen for a connection
Socket socket =  serverSocket.accept();

3. Read data from the Client
InputStream input = new socket.getInputStream(input); 
(#byte배열로 읽기 때문에 상위 데이터를 읽으려면 InputStreamReader로 읽는다)

InputStreamReader reader = new InputSteramReader(input);
int character = reader.read(); //read a single character

(BufferedReader 에 InputStream을 래핑하여 데이터를 String으로 읽음)
BufferedReader reader = new BufferedReader(new ImpotStreamReader(input));
String line = reader.readLine() ; // reads  a line of text

4. Send Dat to the client
OutputSTream output = socket.getOutputStream(); //stream 형식?

(PrintWriter를 사용하면 텍스트 형식으로 데이터를 보낼 수 있다.)
PrintWiter writer = new PrintWriter(output, true);
writer.println("This is a message sent to the server");

5. Close the client Connection
socket.close();
(close는 InputStream 과 OutputStream을 닫아준다.)

6. Terminate the Server
서버를 중지하는 것은
serverSocket.Close();
```


#java-developer-roadmap
#java 
#jdk
#io

