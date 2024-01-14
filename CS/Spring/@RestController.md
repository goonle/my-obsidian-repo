해당 애너테이션은 라우터 열할을 하는 애너테이션이다.

#### 라우터(Router)
라우터란 HTTP 요청과 메서드를 연결하는 장지츠를 말한다. 이 애너테이션이 있어야 클라이언트의 요청에 맞는 매서드를 실행할 수 있다.

@RestController는 @Component와 용어가 다른데 어떻게 @ComponentScan에서 자동으로 등록할 수 있는 것일까? 

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Controller
@ResponseBody
public @interface RestController{
	@AliasFor(annotaion = Controller.class)
	Stirng value() default = "";
}
```
RestController 애너테이션의 정의를 보면 Controller와 ResponseBody 애너테이션이 합쳐진 결과물이라는 것을 알 수 있다. 하지만 아직도 Component는 보이지 않는다.

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Controller{

	@AliasEor(annotation = Coomponent.class)
	String value() default = "";
}
```
@Controller 어노테이션이 바로 @Component로 구성되어 있음을 확인 할 수 있다. 이 때문에 @ComponentScan을 통해 빈으로 등록되는 것이다.

#annotation 
#java 
