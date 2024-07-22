Java 객체지향 디자인 패턴 128p

>[!info] 체크포인트 1
>다음 FuelMonitoring 클래스는 로켓의 연료 탱크를 검사해 특정 조건에 맞지 않으면 관리자에게 경고 신호를 보내는 기능이 있다. 연료 탱크를 검사하는 방식과 경고를 보내는 방식이 변경될 가능성이 큰 경우에 대비해 다음 코드를 수정하라.
>```java
>public class FuelTankMonitoring{
>	public void checkAndWarn(){
>		if(checkFuelTank(...)){
>			giveWarningSignal(...);
>		}
>	}
>	public boolean checkFuelTank(...){...}
>	public void getWarningSignal(...){...}
>}
>```

### 내 풀이
먼저 검사하는 방식과 경고를 보내는 방식이 변경될 가능성이 큰 경우를 대비하는 것이 목적이라면 '개방 폐쇄 원칙'을 따라야 한다고 생각된다. 변경될 가능성이 큰 것과 작은 것을 분리하여 변하지 않을 것에 의존성을 두는 것이 개방 폐쇄 원칙이라고 생각한다.

하지만 코드를 보니 이미 내용의 추상화는 잘되어 있는 듯하다. 그렇다면 단일 책임 원칙일 수 있겠다. 현재 검사하는 방식과 경고하는 방식이 하나의 클래스 안에 작성되어 있어 하나의 기능이 수정되면 다른 기능에 영향을 줄 수 있다고 생각하기 때문이다.

그렇다면 FuelTankMonitoring에서 검사 기능과 경고 기능을 나눠 사용하면 될 것 같다.

```java
public class FuelTankCheck{
	FuelTank fuelTank;
	public FuelTankCheck(FuelTank ft){
		this.fuelTank = ft;
	}
	public boolean checkFuelTank(){...};
}
public class FuelTankWarn{
	FuelTankCheck ftc;
	public FuelTankWarn(ftc){
		this.ftc = ftc;
	}
	public void getWarningSignal(boolean check){...}
}

public void main(String[]){
	FuelTank ft = new FuelTank();
	FuelTankCheck ftc = new FuelTankCheck(ft);
	FuelTankWarn ftw = new FuelTankCheck(ftc);
	FuelTankWarn.getWarningSignal();
}
```

예제에서 FuelTank에 대한 언급이 없었어서 걸린다. 기능을 나눌 때, getter와 setter를 따로 만들지 않은 이유는 모델로 사용될 객체가 FuelTank로 남아있어야 하지 않을까 해서 그렇다. 

아래는 정답 예제이다.

### 정답 예제를 읽고

책에서 파트는 개방폐쇄 원칙 파트였고 상속받은 자식 클래스에서 기존의 메서드는  protected로 선언 후 기능을 추가하는 방식으로 사용했다. 잘 못 짚었다.


