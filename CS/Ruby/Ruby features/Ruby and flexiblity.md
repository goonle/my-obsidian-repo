개발자가 Ruby의 어떤 부분이든 자유롭게 바꿀 수 있다. 원한다면 Ruby의 코어 부분도 제거하고 재정의할 수도 있다. 혹은 오버라이드도 가능하다. 
```ruby
class Numeric
	def plus(x)
		self.+)x
	end
end

//기존코드
y = 5+6
//위 코어에 추가한 코드
y = 5.plus 6

```
#ruby
