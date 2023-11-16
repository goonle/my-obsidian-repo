#### 자바스크립트 마우스 이벤트 4가지 좌표 차이
---
자바스크립트 마우스 이벤트와 마우스 이벤트 객체에서 얻어낼 수 있는 3가지 좌표
1. clientX/Y 
2. pageX/Y
3. offsetX/Y, screenX/Y
---
#### 마우스 이벤트 객체
---
![[Pasted image 20231107172616.png]]

##### MouseEvent.clientX/Y
응용 프로그램(웹 브라우저)의 뷰포트(위 그림의 오렌지 박스) 내에서 수평 좌표를 제공합니다(페이지 내 좌표가 아닌 브라우저)
##### MouseEvent.pageX/Y
현재 볼 수 없는 문서 부분이 포함

##### MouseEvent.offsetX
클릭 이벤트 target 노드가 좌표 원점의 기준이 되고 클릭 이벤트가 발생한 좌표값은 그 원점을 기준으로 X, Y 좌표값이 계산

#js 
#donno