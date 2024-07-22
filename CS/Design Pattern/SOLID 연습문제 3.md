>[!info] 체크포인트 3
>만약 Kid 클래스가 다음 클래스 다이어그램과 같이 Robot 클래스와 연관 관계를 맺었다고 가정하면 어떤 일이 발생하는가?
>Kid -----> Robot
>```java
>public class Kid {
>	private Robot toy;
>	public void setToy(Robot toy){
>		this.toy = toy;
>	}
>	public void play(){
>		System.out.println(toy.toString());
>	}
>}
>public class Main {
>	public static void main(string[] args){
>		Robot t= new Robot();
>		Kid k = new Kid();
>		k.setToy(t);
>		k.play();
>	}
>}
>```

토이의 종류가 변경 될 때마다 Kid 클래스 안에있는 toy라는 변수의 타입을 계속해서 변경해야 한다.


   
   