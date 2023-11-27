
[From JENKCV.com witten by Jakob Jenkov : Java IO : Networking](https://jenkov.com/tutorials/java-io/networking.html)

### Java IO : Networking
---
자바에서 네트워킹의 자세한 사항은 약간 자바 IO 튜토리얼을 벗어났다. 자바 네트워킹은 나의 자바 네트워킹 튜토리얼에 더 자세히 나와있다. 하지만 네트워크 커넥션들이 흔한 자원이거나 데이터의 목적지이기 시작한 후부터 우리는 네트워키 연결을 넘는 통신을 위히 자바 IO API를 사용한다. 이 글은 자바 네트워킹을 약간 서술한다.

두 프로세스들이 통신을 위해서는 마치 파일을 다룰 때처럼 네트워크 커넥션이 생긴다. 데이터를 읽기 위해 InputStream을 사용하고 데이터를 쓰기 위해 OutputStream을 사용하넌것. 다른 말로 하자면, Java Networking API는 프로세스 간의 네트워크 커넥션을 만들기 위해 사용되는 반면, Java IO는 프로세스 간 네트워크 커넥션이 생기면 프로세스 간의 데이터 교환을 위해 사용된다.

기본적으로 만약 우리가 파일에 무엇인가를 기록할 수 있는 코드를 작성하면 같은 것을 네트워크 커넥션에 쓰는 것은 쉽게 되는 것을 의미한다. 필요한 모든 것은 우리의 컴포넌트가 FileOutputStream 대신 OutputStream에 의존하는 것이다. FileOutputStream이 OutputStream의 서브클래스이기 떄문에 문제가 없다.

파일에서부터 데이터를 읽는 것 또한 같다. 파일에서 어떤 데이터를 읽을 수 있다면, 쉽게 같은 데이터를 네트워크 커넥션으로부터 읽을 수 있다. 단지 컴포넌트를 읽을 때 FileInputStream이 아니라 InputStream을 통해 읽어야 한다. 

다음은 그 예제 코드이다.
```java
public class MyClass {
	public static void main( String[] args){
		InputStream inputStream = new FileInputStream("c:\\myfile.txt");
		process(inputStream);
	}
	public static void process(InputStream input) throws IOException {
		//do something with the InputStream
	}

}
```

이 예제에서 process() 는 이 InputStream이 파라미터가 파일시스템에서 오는지 네트워크에서 오는지 알지 못한다. 단지 process() 메소드는 InputStream 위에서 작동할 뿐이다.




#java-developer-roadmap
#java 
#jdk
#io
