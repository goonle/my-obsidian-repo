### watched property
---
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

#vue 
#watch