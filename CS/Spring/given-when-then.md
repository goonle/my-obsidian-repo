
### given-when-then
---
>[!info]
>테스트 코드를 세 단계로 구분해서 작성하는 방식.
>1. given : 테스트 코드를 준비하는 단계
>2. when : 테스트를 진행하는 단계
>3. then : 테스트 결과를 검증하는 단계

### 예제
```java
@DisplayName("새로운 메뉴를 저장한다.")
@Test
public void saveMenuTest(){
	//given : 메뉴를 저장하기 위한 준비 과정
	final String name = "아메리카노";
	final int price = 2000;

	final Menu americano = new Menu(name, price)

	// when : 실제 메뉴를 저장
	final long savedId = menuService.save(americano);

	// then : 메뉴가 추가 되었는지 검증하는 단계
	final Menu savedMenu = menuService.findById(savedId).get();
	assertThat(savedMenu.getNmae()).isEqualTo(name);
	assertThat(savedMenu.getPrice()).isEqualTo(price);
}
```

#testcode
#java 
#spring 