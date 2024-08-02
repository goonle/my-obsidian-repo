### MVC 패턴은 디자인 패턴인가?

>[!quote] chatGPT
>MVC 패턴은 디자인 패턴으로 간주됩니다. 디자인 패턴은 소프트웨어 공학에서 자주 발생하는 문제를 해결하기 위한 재사용 가능한 해결책을 제공하는 일반적인 템플릿을 의미합니다. MVC (Model-View-Controller) 패턴은 애플리케이션의 구조를 모듈화하여 유지보수성과 확장성을 높이기 위한 대표적인 디자인 패턴 중 하나입니다.

###### 1. MVC는 애플리케이션의 구조적 설계 패턴, 
###### 2. 템플릿 메서드 패턴은 알고리즘의 골격을 정의하고, 일부 단계를 서브클래스에서 구현하도록 하는 행동 패턴입니다.

### 템플릿 메서드 패턴
**코드**
```java
abstract class Game {
	public final void play(){
		initialize();
		startPlay();
		endPlay();
	}

	abstract void initialize();
	abstract void startPlay();
	abstract void endPlay();
}

class Cricket extends Game {
	@Override
	void initialize(){
		System.out.println("Cricket Game is Initialized");
	}
	@Override
	void startPlay(){
		System.out.println("Cricket Game's just started");
	}
	@Override
	void endPlay(){
		System.out.println("Cricket Game is going to end soon");
	}
}

class Football extends Game {
	@Override
	void initialize(){
		System.out.println("Football Game is Initialized");
	}
	@Override
	void startPlay(){
		System.out.println("Football Game's just started");
	}
	@Override
	void endPlay(){
		System.out.println("Football Game is going to end soon");
	}
}

public class TemplateMethodPatternDemo {
	public static void main(String[] args){
		Game game = new Cricket();
		game.play();
		
		game = new Football();
		game.play();
	}
}
```



