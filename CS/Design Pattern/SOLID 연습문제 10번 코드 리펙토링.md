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
>	private JTextField tfWorkingHours = new JTextField();
>	private JTextField tfOvertimeHours = new JTestField();
>	private JTextField tfResult = new JTextField();
>	
>	private JButton calcButton = new JButton("Calculate");
>	private JButton resetButton = new JButton("Reset");
>	private JButton end = new JButton("Stop)";
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
>			payAmount = 10\*x + 15\* 7;
>			tfResult.setText(String.valueOf(payAmount));
>			resetButton.setEnabled(true); 
>		}
>	}
>}
>```
