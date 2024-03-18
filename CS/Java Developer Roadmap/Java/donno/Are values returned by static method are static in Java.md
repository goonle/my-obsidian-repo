[원문 : Are values returned by static method are static in Java?](https://www.tutorialspoint.com/are-values-returned-by-static-method-are-static-in-java)

```
Whenever you return values from a static method they are either static nor instance by default, they are just values.

The user invoking the method can use them as he wants. i.e. you can retrieve the values and declare them static.

But, since you cannot declare variables of a method static if you need to declare the vales returned by a method static you need to invoke it in the class outside the methods.
```

Static 매서드로부터 Value를 리턴할 때는 그것이 스테틱이던 아니던 value일 뿐이다.
유저는 그들이 원하는 방식으로 사용할 수 있다. 당신은 값들을 다시 참조하거나 static으로 정의할 수 있다.
다만, 당신이 해당 클래스 외부의 메소드를 사용하여 값을 리턴하기 위해 선언할 때는 변수를 스태틱으로 선언할 수 없다. 

#java #static