Java 객체지향 디자인 패턴 - 116P ~ 120P

# 리스코프 치환 원칙(Liskov substitution principle)
>[!cite] 원문
>"A type of hierachy is composed of subtypes and supertype. The intuitive idea of a subtype is one whose objects provide all the behavior of another type(the supertype) plus something extra. What is wanted here is something like the foloowing substitution property : if for each object o1 of type S there is an object o2 of type T such that for all programs P defined in terms of T, the behavior of P is unchanged when o1 is substituted for o2, then S is a supertype of T. 

LSP는 **일반화 관계**에 대한 이야기이며, 자식 클래스는 부모 클래스를 대체했을 때, 프로그램 상의 변화가 없어야 한다는 뜻이다.

예를 들면, 포유류
- 포유류는 알을 낳지 않고 새끼를 낳는다
- 포유류는 젖을 먹여 새끼를 키우고 폐를 통해 호흡한다.
- 포유류는 체온이 일정한 저어온 동물이며 털이나 두꺼운 피부로 덮여있다.

오리너구리
- 오리너구리는 알을 낳지 않고 새끼를 낳는다.
- 오리너구리는 젖을 먹여 새끼를 키우고 폐를 통해 호흡한다.
- 오리너구리는 체온이 일정한 저어온 동물이며 털이나 두꺼운 피부로 덮여있다.

로 바꿨을 때,

오리너구리는 알을 낳아 번식하기 때문에  대체가 불가능 하여 LSP를 만족하지 않는데 이는 만족하지 않는다.
부모클래스인 포유류를 자식클래스인 오리너구리가 대체할 수 없기 때문이다. 

(리스코프 치환 원칙에 오리너구리가 대입되려면 포유류의 첫번째 특징이 없어지면 된다)

아래는 자바 코드로 작성한 예다.
```java
public class Bag {
	private int price;
	public void setPrice(int price){
		this.price = price;
	}
	public int getPrice(){
		return price;
	}
}

public class WrongBag extends Bag{
	private double discountRate = 0;
	public void setDiscountRate(double discountRate){
		this.discountRate = discountRate;
	}
	public void setPrice(int price){
		super.setPrice(price - (int)(discountRate * price));
	}
}

public class rightBag extends Bag{
	private double discountRate = 0;
	public void setDiscountRate(double discountRate){
		this.discountRate = discountRate;
	}
	public void applyDiscount(int price){
		super.setPrice(price - (int)(discountRate * price));
	}
}
```

위 코드를 보면 WrongBag은 discountRate가 0일 때를 제외하면 WrongBag.setPrice를 했을 때, Bag.setPrice와 다른 price가 설정이 된다. 완전한 대체가 불가능하게, 행동이 변함, 되었기 때문에 LSP를 만족하지 않는다.

하지만 RightBag의 경우는 다르다. RightBag.setPrice()와 Bag.setPrice는 같은 결과 값을 냄으로써 LSP를 만족하지만 RightBag.applyDiscount(int)를 통해서 원하는 기능을 해낼 수 있다.

#solid 
#LiscovSubstitutionPrinciple
