개발자는 어떤 메서드에든 클로저를 추가함으로써 메서드의 동작을 기술할 수 있다. Ruby에서는 이러한 클로저를 블록이라고 부른다.
```ruby
search_engines = 
	%w[Google Yahoo MSN].map do |engine|
		"http://www." + engine.downcase + ".com"
	end
```
*위 문법은 do ... end 문법 구조에서 기술되었다. 
map 메서드는 주어진 단어 목록에 블록을 적용한다. 이처럼 Ruby의 다른 메서드도 그 동작 중 일부를 자신의 블록으로 채워넣을 수 있도록 한다.*

#ruby