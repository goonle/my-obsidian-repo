>[!info] 정의
> 자바의 컬렉션 프레임 워크에서 컬렉션에 저장된 요소를 읽어들이는 방법을 표준화한 것 중 하나

## 자료형
```java
public interface Iterator{
	boolean hasNext();
	Object next();
	void remove();
}
```

## 매서드
```java
boolean hasNext(){
 다음 요소가 있으면 true 아니면 false
}
Object next(){
	다음 일겅올 요소
}
void remove(){
	next로 읽어온 요소 삭제
}


```
#java 
#iterator
