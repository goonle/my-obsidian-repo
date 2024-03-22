### v-cloak
---
가끔 v-for 문을 사용할 때 일시적으로  {{data}} 표현식이 표시되는 경우를 막기위 위한 디렉티브다.
```html
<!doctype html>
<html>
	<head>
		...
		<style>
			#list {..}
			#list td, #list th {...}
			#list > thead > tr {...}
			[v-clock] {display : none;}
		</style>
	</head>
	<body>
		<div id = "app" v-cloak>
			...
		</div>
	</body>
</html>
```

#vue 
#v-cloak
