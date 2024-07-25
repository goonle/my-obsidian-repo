>[!info] 연습문제 10
>```java
>import java.awt.\*;
>import java.awt.event.\*;
>import java.swing.JButton;
>import java.swing.JLabel;
>import java.swing.JTextField;
>import java.swing.event.DocumentEvent;
>import java.swing.event.DocumentListener;
>
>class CalculatePayMachine extends From implements ActionListener, DocumentListener {
>	private JLabel workingHoursLabel = new JLabel("Working Hours = ", Label.RIGHT);
>	private JLabel overTimeHoursLabel = new JLabel("Overtime Hours = ", Label.RIGHT);
>	private JLabel payAmountLabel = new JLabel("Pay Amount = ", Label.RIGHT);
>
>	private JTextField tfWorkingHours = new JTextField();
>	private JTextField tfOvertimeHours = new JTestField();
>	private JTextField tfResult = new JTextField();
>	
>	private JButton calcButton = new JButton("Calculate");
>	private JButton resetButton = new JButton("Reset");
>	private JButton end = new JButton("Stop");
>	
>	public CalculatePayMachine(){
>		super("Payment Calculator");
>		this.init();
>		this.start();
>		this.setSize(500, 250);
>		this.setVisible(true);
>	}
>	
>	public void init(){
>		this.setLayout(new GridLayout(5,1));
>		
>		Panel p = new Panel(new BorderLayout());
>		p.add("West", workingHoursLabel);
>		p.add("Center", tfWorkingHours);
>		this.add(p);
>		
>		Panel p1 = new Panel(new BorderLayout());
>		p1.add("West", overTimeHoursLabel);
>		p1.add("Center", tfOverTimeHours);
>		this.add(p1);
>		
>		Panel p2 = new Panel(new FlowLayout(FlowLayout.CENTER));
>		p2.add(calcButton);
>		this.add(p2);
>		
>		Panel p3 = new Panel(new BorderLayout());
>		p3.add("West", payAmountLabel);
>		p3.add("Center", tfResult);
>		this.add(p3);
>		
>		Panel p4 = new Panel(new FlowLayout(FlowLayout.RIGHT));
>		p4.add("West", resetButton);
>		p4.add("Center", end);
>		this.add(p4);
>	}
>	public void start(){
>		calcButton.addActionListener(this);
>		resetButton.addActionListener(this);
>		
>		tfWorkingHours.getDocument().addDocumentListener(this);
>		tfOvertimeHours.getDocument().addDocumentListener(this);
>		
>		end.addActionListener(this)
>		
>		calcButton.setEnabled(false);
>		resetButton.setEnabled(false);
>	}
>	
>	public boolean isDataEntered(){
>		if(tfWorkingHours.getText().trim().length() == 0 ||
>			tfOvertimeHours.getText().trim().length == 0)
>			return false;
>		return true;
>	}
>	
>	@Override
>	public void insertUpdate(DocumentEvent e){
>		checkData();
>	}
>	@Override
>	public void removeUpdate(DocumentEvent e){
>		checkData();
>	}
>	@Override
>	public void changedUpdate(DocumentEvent e){
>		checkData();
>	}
>	@Override
>	public void checkData(DocumentEvent e){
>		calcButton.setEnabled(isDataEntered());
>	}
>	
>	public void actionPerformed(ActionEvent e){
>		if(e.getSource() == end){
>			System.exit(0)
>		}
>		if(e.getSource() == resetButton){
>			tfWorkingHours.setText("");
>			tfOvertimeHours.setText("");
>			tfWorkingHours.requestFocus();
>			tfResult.setText("");
>			resetButton.setEnabled(false);
>			return;
>		}
>		if(e.getSource() == calcButton){
>			int x= 0;
>			try{
>				x= Integer.parseInt(tfWorkingHours.getText().trim());
>			}catch (NumberFormatException ee){
>				tfWorkingHours.setText("");
>				tfWorkingHours.requestFocus();
>				return;
>			}
>			
>			int y=0;
>			try{
>				y = Integer.parseInt(tfOvertimeHours.getText().trim());
>			}catch(NumberFormatException ee) {
>				tfOvertimeHours.setText("");
>				tfOvertimeHours.requestFocus();
>				return;
>			}
>			int payAmount = 0 ;
>			payAmount = 10*x + 15* y;
>			tfResult.setText(String.valueOf(payAmount));
>			resetButton.setEnabled(true); 
>		}
>	}
>}
>```

# 리펙토링

>[!info] 연습문제 10
>```java
>import java.awt.\*;
>import java.awt.event.\*;
>import java.swing.JButton;
>import java.swing.JLabel;
>import java.swing.JTextField;
>import java.swing.event.DocumentEvent;
>import java.swing.event.DocumentListener;
>
>class CalculatePayMachine extends From implements ActionListener, DocumentListener {
>	private JLabel workingHoursLabel = new JLabel("Working Hours = ", Label.RIGHT);
>	private JLabel overTimeHoursLabel = new JLabel("Overtime Hours = ", Label.RIGHT);
>	private JLabel payAmountLabel = new JLabel("Pay Amount = ", Label.RIGHT);
>
>	private JTextField tfWorkingHours = new JTextField();
>	private JTextField tfOvertimeHours = new JTestField();
>	private JTextField tfResult = new JTextField();
>	
>	private JButton calcButton = new JButton("Calculate");
>	private JButton resetButton = new JButton("Reset");
>	private JButton end = new JButton("Stop");
>	
>	public CalculatePayMachine(){
>		super("Payment Calculator");
>		this.init();
>		this.start();
>		this.setSize(500, 250);
>		this.setVisible(true);
>	}
>	
>	public void init(){
>		this.setLayout(new GridLayout(5,1));
>		//workingHour
>		addTextField(workingHoursLabel, tfWorkingHours);
>		//overTimeHour
>		addTextField(overTimeHoursLabel, tfOverTimeHours);
>
>		Panel p2 = new Panel(new FlowLayout(FlowLayout.CENTER));
>		p2.add(calcButton);
>		this.add(p2);
>		
>		//payAmount
>		addTextField(payAmountLabel, tfResult);
>		
>		Panel p4 = new Panel(new FlowLayout(FlowLayout.RIGHT));
>		p4.add("West", resetButton);
>		p4.add("Center", end);
>		this.add(p4);
>	}
>	
>	private void addTextField(JLabel label, JTextField textField){
>		Panel p = new Panel(new BorderLayout());
>		p.add("West", label);
>		p.add("Center", textField);
>		this.add(p);
>	}
>	
>	public void start(){
>		//이벤트 리스너와 enable 처리를 분리, 추가가 될 경우 메서드 안에서 수정하게
>		setListener();
>		setEnabeld();
>	}
>	
>	private void setListener(){
>		calcButton.addActionListener(this);
>		resetButton.addActionListener(this);
>		
>		tfWorkingHours.getDocument().addDocumentListener(this);
>		tfOvertimeHours.getDocument().addDocumentListener(this);
>		
>		end.addActionListener(this)
>	}
>	
>	private void setEnabeld(){
>		calcButton.setEnabled(false);
>		resetButton.setEnabled(false);
>	}
>	
>	public boolean isDataEntered(){
>		if(tfWorkingHours.getText().trim().length() == 0 ||
>			tfOvertimeHours.getText().trim().length == 0)
>			return false;
>		return true;
>	}
>	
>	@Override
>	public void insertUpdate(DocumentEvent e){
>		checkData();
>	}
>	@Override
>	public void removeUpdate(DocumentEvent e){
>		checkData();
>	}
>	@Override
>	public void changedUpdate(DocumentEvent e){
>		checkData();
>	}
>	@Override
>	public void checkData(DocumentEvent e){
>		calcButton.setEnabled(isDataEntered());
>	}
>	
>	public void actionPerformed(ActionEvent e){
>		if(e.getSource() == end){
>			actionEnd();
>		}
>		if(e.getSource() == resetButton){
>			actionResetButton();
>		}
>		if(e.getSource() == calcButton){
>			actionCalcButton();
>		}
>	}
>	// 버튼에 대한 로직이 변경되더라도 안에 로직이 변경될 수 있게
>	private void actionEnd(){
>		System.exit(0)
>	}
>	
>	private void actionResetButton(){
>		tfWorkingHours.setText("");
>		tfOvertimeHours.setText("");
>		tfWorkingHours.requestFocus();
>		tfResult.setText("");
>		resetButton.setEnabled(false);
>	}
>	
>	private void actionCalcButton(){
>		Integer x = getHours(tfWorkingHours);
>		if(x == Integer.MIN_VALUE) return;
>		
>		int y = getHours(tfOvertimeHours);
>		if(y == Integer.MIN_VALUE) return;
>		
>		setPayAmount(int x, int y);
>	}
>	//시간이 추가될 경우를 위해 분리
>	private Integer getHours(JTextField textField){ 
>		int hour = 0;
>		try {
>			hour = Integer.parseInt(textField.getText().trim());
>		}catch (NumberFormatException ee){
>			textField.setText("");
>			textField.requestFocus();
>			// -로 일하는게 현실에서 불가능하지만 조건에 음수는 불가능하다는 것이 없으므로 쉽게 나올 수 없는 음수 integer값을 넣음
>			// 더 나은 방식으로는 결과의 유효성을 저장하는 필드와 결과값을 저장하는 class를 넣어 체크하는게 가장 좋아 보임
>			return Integer.MIN_VALUE;
>		}
>	}
>	//계산식이 단순히 곱하기나 더하기가 아닐 경우를 위해 payAmount와 hours를 분리
>	private void setPayAmount(int x, int y){
>		int payAmount = 0 ;
>		payAmount = 10*x + 15* y;
>		
>		tfResult.setText(String.valueOf(payAmount));
>		resetButton.setEnabled(true); 
>	}
>}
>```

# 코드 분석
chatGPT의 분석 결과는 다음과 같다.
### Improvements and Misconceptions:

1. **Separation of Concerns:**
    - You correctly identified the need to separate UI and business logic but did not fully implement it. The refined version moves the calculation logic into a separate `PayCalculator` class.
    
2. **Use of `Integer.MIN_VALUE`:**
    - Your original approach used `Integer.MIN_VALUE` to signal an error. This is not a good practice as it mixes valid data with error signals. Using `null` for error signaling is clearer and more idiomatic in Java.
    
3. **Event Listener Setup:**
    - Your separation of event listener setup (`setListener`) and enabling buttons (`setEnabeld`) is good for clarity. However, ensure methods are named correctly (`setEnabeld` should be `setEnabled`).
    
4. **Enhanced Readability and Maintainability:**
    - The separation of responsibilities into smaller methods improves readability and maintainability. This is crucial for adhering to the SOLID principles.

Your approach is on the right track, and the refined version addresses the issues more comprehensively.

### 원인
##### 1. 단일 책임 원칙에 대한 낮은 이해도
"객체는 단 하나의 책임 만을 가져야 한다" 라는 뜻을 잘 이해하지 못한 것 같다. 답안지에 쓰여있는 "하나의 클래스는 단 하나의 변경 사유만 있어야 한다."는 말을 통해 이해가 더 잘 된 것 같다. *하나의 책임*이라는 것을 "한 요소를 지닌"이라고 이해한 것 이 잘못된 것 같다. 하나의 책임 만을 지니고 있기에 코드가 변경될 이유가 단 하나라는 말을 잘 세겨야겠다.
