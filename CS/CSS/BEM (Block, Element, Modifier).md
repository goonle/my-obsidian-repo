>[!info] BEM이란
>네이밍 방법론 중에 하나다. 처음 이 방식을 본 건 회사에서 다른 회사에 외주작업을 맡겼을 때, 외주 개발자가 scss를 사용하며 알게되었다. 

# Block
페이지의 화면 요소의 단위를 의미한다.

# Element
블록의 하위요소이다. 네이밍이 Block과 연결된다.
```html
<div class="block">
	<div class="block__element"></div>
</div>
```

# Modifier
css 요소와 수정자 이름으로 표시한다.
```html
<div class="block">
	<div class="block__element block__element__border-red"></div>
</div>
```

# 주의점
1. 여러 수준의 하위 요소가 있는 경우 클래스 이름에서 각 수준을 나타내려고 하면 안 된다
   - 하위요소가 여러 개라면, 요소를 새로 정립하는게 낫다.
   - ex) `photo__caption__quote`는 BEM을 잘못 사용한 것으로 `photo__quote`가 더 적합하다

#bem #css