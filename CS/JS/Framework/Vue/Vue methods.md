### 매서드
---
Vue 인스턴스에서 사용할 메서드를 등록하는 옵션이다.

```html
<body>
	<div id="app">
		1보다 큰수 : <input id="a" type="text" v-model.number="num">
		<br/>
		1부터 입력한 값까지의 합 : <span>{{sum()}}</span><br/>
		1부터 입력한 값까지의 합 : <span>{{sum()}}</span><br/>
		1부터 입력한 값까지의 합 : <span>{{sum()}}</span><br/>
	</div>
	<script type="text/html" src="https://unpkg.com/vue"></script>
	<script>
		var vm = Vue.createApp({
			name : "APP",
			data(){
				return {num : 0};
			},
			methods: {
				sum(){
					console.log("sum :: ", this.num);
					var n = parseInt(this.num);
					if(Number.isNaN(n)) return 0;
					return (n*(n+1))/2;
				}
			}
	
		}).mount('#app');
	</script>
</body>
```
기존 computed  와 다른 점은 함수를 실행하는 횟수가 다르다.

#vue 
#methods
