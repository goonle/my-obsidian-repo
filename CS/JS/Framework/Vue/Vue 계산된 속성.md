### Computed Property
---
계산된 속성은 data나 다른 속성이 변경될 때 함수가 실행되어 저장된 캐싱된 값이다.
```html
<body>
	<div id="app">
		1보다 큰수 : <input id="a" type="text" v-model.number="num">
		<br/>
		1부터 입력한 값까지의 합 : <span>{{sum}}</span><br/>
		1부터 입력한 값까지의 합 : <span>{{sum}}</span><br/>
		1부터 입력한 값까지의 합 : <span>{{sum}}</span><br/>
	</div>
	<script type="text/html" src="https://unpkg.com/vue"></script>
	<script>
		 var vm = Vue.createApp({
			 name: "App",
			 data(){
				 return { num : 0 };
			 },
			 computed : {
				 sum() {
					 console.log("## num : " + this.num);
					 var n = parseInt(this.num);
					 if (Number.isNaN(n)) return 0;
					 return (n * (n + 1))/2
				 }
			 }
		 
		 }).mount("#app");
	</script>
</body>
```

위 코드에서 sum을 3번을 작성했지만 사실 상 값은 1번 계산되어 출력한다.

set매서드를 사용하면 쓰기도 가능하다
```html
<body>
	<div id="app">
		<input type="text" v-model.number="amt" /><br/>
		금액: <span> {{amount}}원</span>
	</div>
	<script type="text/javascript" src="https://unpkg.com/vue"></script>
	<script>
		var vm = Vue.createApp({
			name : "APP",
			data(){
				return {amt :99};
			},
			computed : {
				amont : {
					get(){
						var regexp = /\B(?=(\d{3})+(?!\d))/g;
						return this.amt.toString().replace(regexp, ',');
					},
					set(amout){
						var amt = parseInt(amount.replace(/,/g, ""));
						this.amt = Number.isNaN(amt) ? 0 : amt
					}
				}
			}
		}).amount("#app");
	</script>
</body>
```

#vue 
#computed