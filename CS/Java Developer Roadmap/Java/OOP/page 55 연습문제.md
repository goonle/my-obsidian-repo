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

### 12. 그림 1-14를 구현한 코드 (48쪽 체크포인트 해설 참조)에서 과목의 수강생을 구하는 getStudents 메서드를 구현하라.

``` java
import java.util.Vector
public class Course {
	private String name;
	private Vector<Student> students;
	
	public Vector<Student> getStudents(){
		return students;
	}
}


// 정답
public Vector<Student> getStudents(){
	Vector<Student> students = new Vector<Student>();
	Iterator<Transcript> itor = transcripts.iterator();

	while(itor.hasNext()){
		Transcript tr = iter.next();
		students.add(tr.getStudent());
	}
	return students;
}
```


### 14. 다음 설명에 맞는 클래스 다이어그램을 작성하라.
![[Pasted image 20240423191326.png]]
