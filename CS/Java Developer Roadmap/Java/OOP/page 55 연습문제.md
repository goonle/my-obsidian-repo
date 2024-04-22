### 7. 다음 클래스 다이어그램에 해당하는 코드를 작성하라

| Account                                                                        |     |
| ------------------------------------------------------------------------------ | --- |
| -id Integer<br>-owner: String<br>-balance: Double                              |     |
| +deposit(amount: Double)<br>+withdraw(amout: Double)<br>\#getBalance(): Double |     |

```java
public class Account {
	private Integer id;
	private String owner;
	private Double balance;
	
	public Account(String owner){
		this.owner = owner;
		this.id = 1;
		this.balance = 0;
	}
	
	public void deposit(Double amount) {
		balance += amount;
	}

	public void widthdraw(Double amount) {
		balance -= amount;
	}

	public Double getBalance(){
		return balance;
	}
}
```

### 8. 다음 설명에 맞는 클래스 다이어그램을 작성하라
- 고객은 여러 개의 신용카드를 소유할 수 없다.
- 신용카드가 없는 고객도 있다.
- 신용카드에는 어떤 고객 정보도 없다.

![[Pasted image 20240423085805.png]]

