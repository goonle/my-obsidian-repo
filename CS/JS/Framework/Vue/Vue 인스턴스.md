```javascript
var vm = Vue.createApp({
	name : "name",
	data(){
		return {};
	}
}).mount("#app");
```

Vue.createApp을 통한 객체 인스턴스를 vue 인스턴스라고 칭한다.
여기서 name과 data를 **옵션객체**라고 한다.

#### data 옵션
---
컴포넌트과 관리, 추적해야 하는 데이터를 등록한다 (변경을 탐지하고 화면을 갱신한다.)
반드시 return {} (객체) 로 되어야 한다.

```console
vm.name = vm.$data.name
```

vue 사용시 $, \_로 시작하는 변수는 data 객체의 속성으로 사용하면 안된다. 
```javascript
data(){
	return { $name : ""}; //이런거 하면 안 됨.
}
```

#vue