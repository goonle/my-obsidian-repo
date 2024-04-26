### p.66 코드 2-4를 ArrayList 클래스를 이용하도록 변경하라.

```java
public class ArrayStack {
	private int top;
	private int[] itemArray;
	private int stackSize;

	public ArrayStack(int stackSize){
		itemArray = new int[stackSize];
		top = -1;
		this.stackSize = stackSize;
	}
	public boolean isEmpty(){
		return (top == -1);
	}
	public boolean isFull(){
		return (top  == this.stackSize -1);
	}

	public void push(int item){
		if(isFull){
			System.out.println("inserting fail! Array Stack is full!!");
		}else{
			itemArray[++top];
			System.out.println("Inserted Item : " +item);
		}
	}
	public int pop(){
		if(isEmtpy()){
			System.out.println("Deleting fail! Array Stack is empty!");
			return -1;
		}else{
			return itemArray[top-];
		}
	}
	

}
```