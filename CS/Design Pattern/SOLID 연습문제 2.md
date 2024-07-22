JAVA 객체지향 디자인 패턴 129p
>[!info] 체크포인트 2
>다음 코드는 오후 10시가 되면 MP3를 작동시켜 음악을 연주한다. 그러나 이 코드가 제대로 작동하는지 테스트하려면 저녁 10시까지 기다려야 한다. OCP를 적용해 이 문제를 해결하는 코드를 작성하라.
>```java
>import java.util.Calendar;
>
>public class TimeReminder {
>	private MP3 m;
>	
>	public void reminder(){
>		Calendar cal = Calendar.getInstance();
>		int hour = cal.get(Calendar.HOUR_OF_DAY);
>		
>		if(hour >= 22){
>			m.playSong();
>		}
>	}
>}
>```

# 나의 풀이
OCP는 일단 Open Closed Pricipal 개방 폐쇄 원칙이니 기존의 코드는 수정하지 않은 체로 기능의 확장을 이루라는 뜻이며, 테스트를 위해 이 문제를 해결한다면 변화된 시간을 대입했을 때, m.playSong 혹은 reminder가 작동해야 한다.

reminder를 수정하지 않고는 시간의 변화를 줄 수 없으니 TimeReminder 클래스에 새로운 method를 작성해야 한다고 판단했다.

```java
public class TimeReminder {
	// same code
	
	public void testReminder(int hour){
		if(hour >= 22){
			System.out.println("현재시간은 %d시며 알림입니다", hour);
			m.playSong();
		}
	}
}
public void main(String[] str){
	TimeReminder t = new TimeReminder();
	t.testReminder(1);
	t.testReminder(9);
	t.testReminder(10);
}
```

# 해답을 읽고 난 후
100% 틀렸다. 부분 점수도 없다. 기존에 존재하는 method 뿐만 아니라 class 자체도 수정하면 안되는 거였다. 
```java
import java.util.Calendar;

public interface TimeProvider {
	public void setHours(int hours);
	public int getTime();
}

public class FakeTimeProvider implements TimeProvider {
	private Calandar c;
	public FakeTimeProvider(){
		c = Calendar.getInstance();
	}
	public FakeTimeProvider(int hours){
		c = Calendar.getInstance();
		setHours(hours);
	}
	public void setHours(int hours){
		c.set(Calendar.HOUR_OF_DAY, hours);
	}
	public int getTime(){
		return c.get(Calendar.HOUR_OF_DAY);
	}
}

public class TimeReminder{
	TimeProvider tP;
	MP3 m;
	public void setTimeProvider(TimeProvider tP){
		this.tP = tP;
	}
	public void reminder(){
		int hours = tProv.getTime();
		if ( hours >= 22) {
			m.playSong();
		}
	}
}
```

# 해답도 클래스 수정이 이루어졌잖아?
더 나은 코드인 것은 알지만 클래스 수정이 해답도 이루어져서 chatGPT 선생께 물어보니 확장에 열리고 수정에 닫힌 OCP를 위한 코드를 작성하려면 추상화를 통한 의존성 주입이 이루어져야 한다고 한다.  *(DIP 의존 역전 원칙에 부합한다.)*

주요점은 나중에 코드의 변화가 Class TimeReminder에 생기지 않고 인터페이스인 TimeProvider의 다양한 자식 클래스 등을 통해 이루어진다고 한다.

정 코드의 수정을 원하지 않는다면 자식 클래스를 통한 확장을 통해 테스트를 위한 코드를 넣을 수는 있다고 한다.

#오답
#OCP 