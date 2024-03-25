### watched property
---
```html
<body>
	<div id="app">
		x : <input type="text" v-model.number="values.x"/><br/>
		y : <input type="text" v-model.number="values.y"/><br/>
		덧셈 결과 : {{sum}}
	</div>
	<script type="text/javascript" src="https://unpkg.com/vue"></script>
	<script type="text/javascript">
		var vm = Vue.createApp({
			name : "APP",
			data(){
				return { x:0 , y:0, sum: 0};
			},
			watch: {
				x(current, old){
					console.log(`## x: ${old} --> ${current}`);
					var result = Number(current) + Number(this.y);
					if(isNaN(result)) this.sum = 0;
					else this.sum = result;
 				},
 				y(current, old){
					console.log(`## y: ${old} --> ${current}`);
					var result = Number(this.x) + Number(current);
					if(isNaN(result)) this.sum = 0;
					else this.sum = result;
 				}
			}
		}).mount("#app");
	</script>
</body>
```

#### 특징
리턴할 필요가 없다

### 주의사항
인스턴스에서 사용하는 데이터, 속성이 복잡한 구조의 객체인 경우에 감시기능이 작동하지 않을 **수도**있다.

```html
<body>
	<div id="app">
		x : <input type="text" v-model.number="x"/><br/>
		y : <input type="text" v-model.number="y"/><br/>
		덧셈 결과 : {{sum}}
	</div>
	<script type="text/javascript" src="https://unpkg.com/vue"></script>
	<script type="text/javascript">
		var vm = Vue.createApp({
			name : "APP",
			data(){
				return { values : {x:0 , y:0}, sum: 0};
			},
			watch: {
				values(current){
					var result = Number(current.x) + Number(current.y);
					is(isNaN(result)) this.sum = 0;
					else this.sum = result;
				}
			}
		}).mount("#app");
	</script>
</body>
```

위 코드는 객체 내부의 값이 변경했을 뿐 객체의 메모리 주소가 바뀐것이 아니기 때문에 화면에 변화가 없다.
아래 코드처럼 짜면 원하는데로 기능하지만 쓸데없이 코드가 복잡해진다. methods를 쓰면 되기 때문이다.

```javascript
watch : {
	values : {
		handler : function(current){
			var result = Number(current.x) + Number(current.y);
			is(isNaN(result)) this.sum = 0;
			else this.sum = result;
		},
		deep: true
	}
}
```


#vue 
#watch