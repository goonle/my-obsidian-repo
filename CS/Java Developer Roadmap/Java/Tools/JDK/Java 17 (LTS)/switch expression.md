
[출처 : velog.io - dongvelop](https://velog.io/@dongvelop/Java-switch-expression)

Java의 버전이 업그레이드 됨에 따라 switch문이 변경된 것으로 보인다.

### 기존의 switch문
```java
private static void test(int n){
	switch(n){
		case 1 :
		case 2 :
		case 3 : {
			System.out.println("1-3");
			break;
		}
		case 4 : {
			System.out.println("4");
			break;
		}
	}
}
```

### 변경된 switch 문
```java
private static void test(int n){
	switch(n){
		case 1, 2, 3 -> System.out.println("1-3");
		case 4 -> System.out.println("4");
	}
}
```

### 개선된 점
- 화살표 함수로 인해 코드가 간결해짐
- 불필요한 중복을 줄임
- break 문을 사용하지 않아도 됨

### 개선된 점 2
```java
private static void test(int n){
	System.out.println(
		switch(n){
			case 1,2,3 -> "1-3"
			case 4 -> "4"
		};
	)
}
```
위의 코드와 같이 리턴값이 있는 형태이기 떄문에 매개변수로 사용할 수 있다.

### 개선된 점 3
```java
private static int plus(int n){
	int result = switch(n){
		case 1 -> { yield n ++;}
		default  -> { yield n;}
	}
}
```
- [[yield]]  를 사용 할 수 있다.
- return과 비슷하다
- switch문에서만 유효하다


#java 
#jdk17
#switch