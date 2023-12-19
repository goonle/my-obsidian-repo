
## 정의
---
**Polling** 이란 하나의 장치(또는 프로그램)이 충돌 회피 또는 동기화 처리 등을 목적으로 다른 장치(또는 프로그램)의 상태를 주기적으로 검사하여 일정한 조건을 만족할 때 송수신 등의 자료처리를 하는 방식을 말한다.

여기서 주요 포인트는 *상태를 주기적으로 검사하여 일정한 조건을 만족할 때 , 자료처리를 하는 방식*이다.

웹 개발에서는 일정한 주기로 Ajax 호출을 사용한다.

###  AJAX Polling
---

```javascript
//jQuery 기준
var global_flag = true;
var intervalfunc;

intervalfunc = setTimeout(function(){
	if(global_flag){
		chkStatus();
	}
}, 5000);

function chkStatus(){
	$.ajax({
		data : { key : 123},
		url : "url",
		dataType : 'json',
		success: function(data){
			if (data.resultCode == 500){
				global_flag = false;
				clearTimeout(intervalfunc)
			}
		}
	})
}


```

#js 
#polling