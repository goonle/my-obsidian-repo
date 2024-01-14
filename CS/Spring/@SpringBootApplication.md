스프링 부트 사용에 필요한 기본 설정을 해준다.

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration //(1)
@ComponentScane(exclideFilter = { //(2)
@Filter(type = FilterType.Custom,
	classes = TypeExcludeFilter.class)
	@Filter(type = FilterType.Custom,
	classes = AutoConfigurationEcludeFilter.class)
})
@EnlableAutoConfiguration //(3)
public @interface SpringBootApplication{
	...생략
}
```

### @SpringBootConfiguration
---
스프링 부트 관련 설정을 나타네는 에너테이션

### @ComponentScan
---
사용자가 등록한 빈을 읽고 등록하는 에너테이션, 이 에너테이션은 @Component라는 에너테이션을 가진 클래스를 찾아 빈으로 등록하는 역할을 한다. 그렇다고 모든 빈에 Component만 사용하지난 않는다. @Component를 감싸는 애너테이션이 있는데 주로 사용하는 애너테이션은 아래와 같다.

| 에너테이션 | 설명 |
| -------------- | ------- |
| @Configuration                        | 설정 파일 등록|
| @Repository                             | ORM 매핑        |
| @Controller, @RestController  | 라우터             |
| @Service                                   | 비즈니스 로직 |
### EnableAutoConfiguration
---
스프링 부트에서 자동 구성을 활성화 하는 에너테이션이다. 이 에너테이션은 스프링 부트 서버가 실행될 때, 스프링 부트의 메타 파일을 읽고 정의된 설정들을 자동으로 구성하는 역할을 수행한다.

#애너테이션
#annotation
#spring 
#java 