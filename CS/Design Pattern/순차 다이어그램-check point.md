![[Pasted image 20240807081335.png]]
# 첫트
### 나의 코드
```java
class A1 {
	private A2 a2;

	public void doA2(this){
		a2 = new A2(this);
	}
	private void doIt(){
		a2.doIt();
	};
}
class A2 extends A1{
	private A3 a3;
	public A2 (A1 a1){
		a3 = new A3(a1);
		this.doIt(a3);
	}
	@Ovveride
	public void doIt(A3 a3){
		this.a3 = a3;
		a3.doIt();
	}
}
class A3 extends A1 {}
```

### GPT 코드
```java
class A1 {
    private A2 a2;

    public void doA1() {
        a2 = new A2(this);
        a2.doA2();
    }
}

class A2 {
    private A3 a3;
    private A1 a1;

    public A2(A1 a1) {
        this.a1 = a1;
        a3 = new A3();
    }

    public void doA2() {
        a3.doA3();
    }
}

class A3 {
    public void doA3() {
        // Implementation of doA3()
    }
}

```

### 코드 비교 후 느낀 점
객체 생성 시, 파라미터를 전달했다고만 되어있지 상속에 대한 것은 없었음에도 넣은 게 첫번째 문제다.
객체의 메서드를 사용하려면 내부에 객체를 선언해주는 생각을 못한게 두번째 문제다.

다만, 그림과 메서드명이 다르기 때문에 한번더 느낀점을 토대로 코드를 변경해보고 답안과 비교를 해봐야겠다.
# 두번째 트라이
### 코드 수정
```java
public void doA1(){
	A1 a1 = new A1();
}
class A1{
	private A2 a2;
	
	public void doA2(this){
		a2 = new A2();	
	}
	public void doIt();
}
class A2{
	private A3 a3;
	private A1 a1;

	public A2(){
		a3 = new A3();
	}

	public void doIt(A3 a3){
		a1.doIt();
	}
}
class A3{}
```

### 답안
```java
public class A1 {
	public void doA1{
		A2 a2 = new A2();
		a2.doA2(this);
	}
	public void doIt(A3 a3){
		a3.doIt();
	}
}

public class A2 {
	public void doA2(A1 a1){
		A3 a3 = new A3();
		a1.doIt(a3);
	}
	public class A3 {
		public void doIt();
	}
}
```

### 답안을 보고 난 후
화살표와 메서드를 가진 상관관계를 거꾸로 생각해서 그랬던 것 같다. 시작점에 위치한 객체가 메서드를 가지고 있다고 생각했는데 도착점에 위치한 객체가 메서드를 포함하고 있었다. 이런 규칙성이라면 다음에 작성을 할 때는 보다 근접한 해답을 찾을 것 같다.