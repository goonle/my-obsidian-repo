```html
<body>
	<div id="app">
		이름 : <input type="text" v-model.trim="name" placeholder="영문 두자 이상을 입력하라."/>
		<br/>
		<ul>
			<li v-for="c in contacts">{{c.name}} : {{c.tel}}</li>
		</ul>
		<div v-show="isLoading">검색중</div>
	</div>
	<script type="text/javascript" src="https://unpkg.com/vue"></script>
	<script type="text/javascript" src="https://unpkg.com/axios"></script>
	<script type="text/javascript" src="https://unpkg.com/lodash"></script>
	<script type="text/javascript">
		const BASEURL = "https://contctsvc.bmater.kro.kr";
		var vm = Vue.createApp({
			name : "APP",
			data(){
				return {name: "" , contacts : [], isLoading: false };
			},
			watch : {
				name(current) {
					if(current.length > 2){
						this.fetchContacts();
					}else{
						this.contact = [];
					}
				}
			},
			methods : {
				fetchContacts: _.debounce(function(){
					this.isLoadinng = true;
					axios.get(BASEURL + `/contacts_long/search/${this.name}`)
						.then((responce)=>{
							this.isLoading = false;
							this.contact = response.data;
						});
				}, 300)
			}
		}).mount("#app");
	</script>
</body>
```

### \_.debounce
---
짧은 시간에 너무 많은 요청을 방지한다.
```javascript
_.debounce( function(){}, 300) ;
```
위 코드는 300ms 동안 연속적인 호출이 일어나지 않을 경우 실행하는 것을 뜻한다.