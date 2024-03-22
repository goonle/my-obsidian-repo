### v-pre
---
해당 디렉티브는 html에 대한 컴파일을 수행하지 않는다.
#### 예제
```html
<!doctype html>
<html>
	<head>
		<meta charset="utf-8">
		<title>03-17</title>
	</head>
	<body>
		<div id = "app">
			<span v-pre>{{message}}</span>
		</div>
		<script src="http://unpkg.com/vue"></script>
		<script>
			var vm = Vue.createApp({
				name : "APP",
				data(){
					return {message : "Hello, world" };
				}
			}).mount("#app");
		</script>
	</body>
</html>
```
```화면
//화면
{{message}}
```

### v-once
---
한번만 렌더링 한다. ( = 렌더링 이후 값을 변경해도 화면에 변경된 값이 표시 되지 않는다.)
```html
<div>
	<span v-once> {{message}} </span>
</div>
```

#vue 
#v-once
#v-pre
