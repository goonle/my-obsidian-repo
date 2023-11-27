#### 스트림
---
자바에서 입출력을 수행하려면 두 노드(키보드 , 모니터, 메모리, 파일 등) 사이를 연결하는 것
**데이터를 운반하는데 사용되는 연결통로**

이 때, 스트림은 단방향으로 통신이 가능하며 하나의 스트림으로 입출력을 함께 처리할 수 없다.

스트림이 처리하는 데이터 타입에 따라 
- 바이트 기반 스트림(XXXStream)  - 8비트 기반 스트림
- 캐릭터 기반 스트림(XXXer)로 나누어진다.

### InputStream , OutputStream
---
모든 바이트 기반 스트림의 조상이다.
InputStream은 추상 클래스로 read 메서드가 추상메서드로 지정되어 있다.

##### InputStream
---
```java
public abstract class InputStream extends Object implements Closable {
	public abstract int read() throws IOException;

	public int read(byte[] b) throws IOException{
	
	}

	public int read(byte[] b , int off, int len){
	}

	public void close() throws IOException{
	}
}
```


#java-developer-roadmap
#java 
#jdk
#io
