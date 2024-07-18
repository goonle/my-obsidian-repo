Java 객체지향 디자인 패턴 - 121p ~ 124p
# 의존 역전 원칙(Dependency inversion principle)
객체들 간 의존 관계를 맞을 경우 원칙을 가지고 관계를 맺어야 효과적인 코드 관리를 할 수 있다.
의존 역전 원칙은 변하기 쉬운 구체적인 부분보다 변하지 않는 추상적인 부분을 통해 의존 관계를 맺으라는 원칙이다. 

예를 들면 아이가 가지고 노는 장난감을 예로 들 수 있다.

아이가 가지고 노는 장난감의 종류는 매일매일 변할 수 있다. 하지만 아이가 장난감을 가지고 논다는 사실과 장난감이라는 개념은 변하기 어렵다. 아이패드가 되었든 공룡 로봇이 되었는 아이가 가지고 노는 것과 아이의 손에 들어가면 장난감이 되기 때문이다.

그렇기 때문에 *아이*라는 클래스에 장난감 종류인 *공룡 로봇*클래스로 의존관계를 맺는 코드를 작성하면 *아이패드*라는 장난감이 생겼을 때, 코드를 다시 생성해야 한다. 

```java
public class 아이 {
	private 공룡로봇 공룡로봇;
	public void set공룡로봇(공룡로봇 공룡로봇){
		this.공룡로봇 = 공룡로봇;
	}
	public void play(){
		System.out.println(공룡로봇.print());
	}
}
public class 공룡로봇 {
	public string print(){
		return "공룡로봇";
	}
}
public class Main{
	public static void main(String[] args){
		공룡로봇 공룡로봇 = new 공룡로봇();
		아이 아이 = new 아이();
		아이.set공룡로봇(공룡로봇);
		아이.play();
	}
}
```

위 코드에 아이패드가 새로 생기면 아래와 같이 코드를 추가해줘야한다.

```java
public class 아이 {
	private 공룡로봇 공룡로봇;
	private 아이패드 아이패드; /////////////////////
	public void set공룡로봇(공룡로봇 공룡로봇){
		this.공룡로봇 = 공룡로봇;
	}
	public void set아이패드(아이패드 아이패드){
		this.아이패드 = 아이패드;
	}
	public void play(){
		System.out.println(공룡로봇.print());
	}
	public void play아이패드(){
		System.out.println(아이패드.print());
	}
}
public class 공룡로봇 {
	public string print(){
		return "공룡로봇";
	}
}
public class 아이패드 {
	public string print(){
		return "아이패드";
	}
}
public class Main{
	public static void main(String[] args){
		//공룡로봇 공룡로봇 = new 공룡로봇();
		아이패드 아이패드 = new 아이패드();
		아이 아이 = new 아이();
		//아이.set공룡로봇(공룡로봇);
		//아이.play();
		아이.set아이패드(아이패드);
		아이.play아이패드();
	}
}
```

하지만 의존 역전 주입 원칙 (DIP)를 지킨다면 아래와 같은 코드로 작성할 수 있다.

```java
public class 아이 {
	private 장난감 장난감;
	public void set장난감(장난감 장난감){
		this.장난감 = 장난감;
	}
	public void play(){
		System.out.println(장난감.print());
	}
}

public class 공룡로봇 extends 장난감{
	public string print(){
		return "공룡로봇";
	}
}

public class Main{
	public static void main(String[] args){
		공룡로봇 공룡로봇 = new 공룡로봇();
		아이 아이 = new 아이();
		아이.set장난감(공룡로봇);
		아이.play();
	}
}
```

위 코드에 아이패드가 추가 되면

```java
public class 아이 {
	private 장난감 장난감;
	public void set장난감(장난감 장난감){
		this.장난감 = 장난감;
	}
	public void play(){
		System.out.println(장난감.print());
	}
}

public class 공룡로봇 extends 장난감{
	public string print(){
		return "공룡로봇";
	}
}
public class 아이패드 extends 장난감{
	public string print(){
		return "아이패드";
	}
}

public class Main{
	public static void main(String[] args){
		//공룡로봇 공룡로봇 = new 공룡로봇();
		아이패드 아이패드 = new 아이패드();
		아이 아이 = new 아이();
		아이.set장난감(아이패드);
		아이.play();
	}
}
```

위와 같이 아이패드 클래스를 추가하고, 사용하는 부분도 간단하게 사용 가능하다. play 에도 의존성이 떨어져 새로 만들지 않아도 된다.

#solid 
#dependencyInversionPrinciple

