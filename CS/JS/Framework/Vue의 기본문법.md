### v-html
innerHtml

### v-text
innerText

### v-bind
1. 단방향 데이터 바인딩
2. jsp로 따지면 <%= %>
### v-model
1. 양방향 데이터 바인딩
```html
<html>
	<body>
		<div id="app">
			<input ud="a" type="text" v-model="name">
			<br/>
		</div>
		입력하신 이름 : <span>{{name}}</span>
	</body>
</html>
<script>
	var vm = Vue.createApp({
		name : "App",
		data() {
			return { name : ""};
		}
	})
</script>
```

2. 데이터 형식
- 다중 선택의 경우 배열을 사용해야 하고 단일 선택은 문자열로 받아야 한다.
- checkbox, radio 와 같이 input 요소를 사용하는 경우에는 각각의 요소마다 사용법에 유의해야 한다.

3. 수식어
- lazy
- number
- trim

4. 한글처리
- 이벤트 처리를 해야 한다. (글자가 완성되기 전엔 데이터가 안 들어간다.)

5. template 테그와 v-for 를 통해 반복해서 html 처리가 가능하다.


#vue #기본