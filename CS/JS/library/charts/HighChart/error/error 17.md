![[Pasted image 20240117094949.png]]
```bash
'에러메세지 구글 번역'
요청한 시리즈 유형이 존재하지 않습니다.

이 오류는 Highcharts에 정의되지 않은 시리즈 유형을 "chart.type"설정할 때 발생합니다. "series.type"일반적인 이유는 시리즈 유형이 정의된 모듈 또는 확장이 "포함되지 않기 때문"일 수 있습니다.

`arearange`예를 들어 시리즈를 생성하려면 "highcharts-more.js"파일을 로드해야 합니다.
```

### 이유
---
#### 이유 1 : 일반적인 상황
> 기본적인 차트는 highcharts.js 만으로 이용이 가능하지만 확장된 차트를 사용하려면 highcharts-more.js를 import를 해줘야한다.

```javascript
importNonThemeFile("/js/highcharts_11.2.0/highcharts.js");
importNonThemeFile("/js/highcharts_11.2.0/highcharts-more.js");
```

현재 몇 가지 써보지 않아서 정확한 것은
- 파이차트
를 사용할 경우 import 해야한다.

#### 이유 2 : 3D차트를 사용할 경우
> 3D 차트를 사용할 경우, 에러는 동일하게 표시되지만 위 두 js파일을 import해도 에러가 표시된다. 왜냐하면 3D 차트의 경우 한가지 js 파일을 더 import해야하기 때문이다.

```javascript
importNonThemeFile("/js/highcharts_11.2.0/highcharts.js");
importNonThemeFile("/js/highcharts_11.2.0/highcharts-more.js");
importNonThemeFile("/js/highcharts_11.2.0/highcharts-3d.js");
```

#javacript
#library 
#highchart
#error