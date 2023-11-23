
[출처 : 망나니개발자 - Java Stream API에 대한 이해](https://mangkyu.tistory.com/112)
### Stream API?
---
Java는 객체지향 언어이기 떄문에 기본적으로 함수형 프로그래밍이 불가능하다.
하지만 JDK8 부터 Stream API, Lambda식, 함수형 인터페이스를 지원하면서 Java를 이용해 함수형으로 프로그래밍 할 수 있는 API를 제공하고 있다.

Stream은 객체.함수.함수.함수 이런식으로 사용가능하게 만든 객체

예제를 보자
#### Stream API 사용 전
---
```java
String[] nameArr = {"IronMan", "Captain", "Hulk", "Thor"};
List<String> nameList = Arrays.asList(naneArr);

//원본데이터가 집접 정렬됨.
Arrays.sort(nameArr);
Collections.sort(nameList);

for(String str: nameArr){
	System.out.println(str);
}

for(String str: nameList){
	System.out.println(str);
}

```

#### Stream API 사용
---
```java
String[] nameArr = {"IronMan", "Captain", "Hulk", "Thor"};
List<String> nameList = Arrays.asList(naneArr);

//원본 데이터가 아닌 별도의 Stream을 생성함
Stream<String> nameStream = nameList.stream();
Stream<String> arrayStream = Arrays.stream(nameArr);

//복사된 데이터를 정렬하여 출력함
nameStream.sorted().forEach(System.out::println);
arrayStream.sorted().forEach(System.out::println);

```


#java-developer-roadmap
#java 
#jdk
#streamAPI
#not-done-yet
