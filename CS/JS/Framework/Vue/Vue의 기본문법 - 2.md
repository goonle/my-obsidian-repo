
### v-for 디렉티브와 key 속성
---
Vue는 가상 DOM을 이용해서 변화된 부분만 변경을 한다.
그렇기에 배열의 키 값에 인덱스를 넣으면 특정 값이 중간, 혹은 앞에 들어갈 경우 전체 인덱스가 변경되어 비효율 적이다.

```javascript
let a = [1,2,3,4,5];
// 각각의 인덱스는 0,1,2,3,4
let b = 3.5;
console.log(a.unshift(b));
// [3.5,1,2,3,4,5]
// 각각의 인덱스는 0,1,2,3,4,5 --> 기존의 0이 1이 되고 줄줄이 바뀌면서 바뀐상태가 총 5개가 됨
```

위의 이유로 v-for의 속성 key에는 고유값을 넣어야 한다.

### 데이터 변경 시 주의사항
---
#### 예제코드
```html
<html>
	<body>
		<div id = "app">
			<table id="list">
				<thead>
					<tr>
						<th>번호</th><th>이름</th><th>전화번호</th>
					</tr>
				</thead>
				<tbody id="contacts">
					<tr v-for="contac in contacts" :key="contact.no">
						<td>{{contact.no}}</td>
						<td>{{contact.name}}</td>
						<td>{{contact.tel}}</td>
				</tbody>
			</table>
		</div>
	</body>
</html>
<script src="http://unpkg.com/vue"></script>
<script>
	var model = {
		"contacts" : [
			{"no" : 1011, "name": "RM", "tel" : "010-010-0101"},
			{"no" : 1012, "name": "정국", "tel" : "010-010-0102"},
			{"no" : 1013, "name": "제이홉", "tel" : "010-010-0103"},
			{"no" : 1014, "name": "슈가", "tel" : "010-010-0104"}
		]
	};
	
	var vm = Vue.createApp({
		name : "APP",
		data(){
			return model;
		}
	}).mount("#app");
	
</script>

```
```console
vm.contacts
=> Proxy {}

model.contacts
=> (4)[{},{},{},{}]

```

뷰 객체에 담긴 값들은 proxy로 래핑되어 있어  vue 객체 밖에서 선언된 객체와 배열은 직접 변경하면 안된다.

#vue 
#v-for
