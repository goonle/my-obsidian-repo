### 외형
---
![[Pasted image 20240117094151.png]]
[출처: highchart.com](https://www.highcharts.com/demo/highcharts/3d-scatter-draggable)

### 생성 방법
---
위 링크를 클릭해서 나오는 Demo 사이트에서 화면에 보이는 컴포넌트 아래에 이런 버튼을 클릭해서 나오는 코드를 복사 + 붙여넣기를 하면 생성 가능하다.
![[Pasted image 20240117094616.png]]

```javascript
	// Set up the chart
	const bubbleChart = new Highcharts.Chart({
	    chart: {
	        renderTo: 'bubbleChart1',//element_id
	        margin: 40,
	        type: 'scatter3d',
	        animation: false,
	        options3d: {
	            enabled: true,
	            alpha: 10,
	            beta: 30,
	            depth: 250,
	            viewDistance: 5,
	            fitToPlot: false,
	            frame: {
	                bottom: { size: 1, color: 'rgba(0,0,0,0.02)' },
	                back: { size: 1, color: 'rgba(0,0,0,0.04)' },
	                side: { size: 1, color: 'rgba(0,0,0,0.06)' }
	            }
	        }
	    },
	    title: false,
	    subtitle: false,
        tooltip: {
            pointFormat: '위험지수 : {point.x} <br/> 위험등급 : {point.y}'
        },
	    yAxis: {
	        min: 0,
	        max: 10,
	    },
	    xAxis: {
	        min: 0,
	        max: 10,
	        gridLineWidth: 1,
	    },
	    zAxis: {
	        min: 0,
	        max: 10,
	        showFirstLabel: false
	    },
	    legend: {
	        enabled: false
	    },
	    series: [{
	        name: 'Data',
	        colorByPoint: true,
	        accessibility: {
	            exposeAsGroupOnly: true
	        },
	        data: sampleData
	    }]
	});

```

### 사전 import
---
기본 highchart 라이브러리는 아래의 코드로 import가 가능하다.
```javascript
	importNonThemeFile("/js/highcharts_11.2.0/highcharts.js");
	importNonThemeFile("/js/highcharts_11.2.0/highcharts-more.js");
 	importNonThemeFile("/js/highcharts_11.2.0/highcharts-3d.js");
```

관련 글 : [[error 17]]

### 속성
---
Devexpress 컴포넌트가 익숙하다 보니 highchart를 사용할 때, 속성에 대한 것을 하나씩 찾아봐야 한다.

#### 1. renderTo
```javascript
chart: {
	        renderTo: 'bubbleChart1'
}
```
> renderTo에는 그릴 html 태그의 ID를 넣는다. $("#" + id).dxChart(); 와 같다.
#### 2. margin
```javascript
chart: {
	        margin: 10
}
```
> chart를 그리는 배경과 chart Object 사이의 간격으로 margin이 클수록 그래프가 작아진다.

#### 3. type
```javascript
chart: {
	        type: "scatter3d",
	        options3d : {},
	        plotOptions : {}
}
```
> 화면에 그릴 차트의 타입으로 3d의 경우 options3d가 선언되지 않으면 그려지지 않는다.
#### 4. options3d
```javascript
chart: {
	        options3d : {
		        enabled: true,
		        viewDistance : 5,
		        fitToFlot : false,
				frame: {
	                bottom: { size: 1, color: 'rgba(0,0,100,0.2)' },
	                back: { size: 1, color: 'rgba(0,100,0,0.4)' },
	                side: { size: 1, color: 'rgba(100,0,0,0.6)' }
	            },
				alpha: 10,
	            beta: 30,
	            depth: 250,
	        }
}
```
##### 0) enable
false일 경우 2d로 표현됨. 해당 옵션을 사용하지 않는다는 뜻
##### 1) viewDistance
![[Pasted image 20240117105925.png]]
##### 2) fitToFlot
화면 사이즈에 맞추기. 화면을 제어할 경우 그래프의 사이즈가 작아지기도 한다.
![[Pasted image 20240117110252.png]]
##### 3) frame
그래프의 배경을 담당하는 속성으로 bottom, back, side로 정의되어 있으며 각각 x 면, y 면, z면을 뜻한다.
각각 size와 rgba 속성이 있다.

size : 는 면의 두께
rgba는 red, green, blue, alpha 값을 의미한다.

##### 4) alpha, beta, depth
```bash
//공식문서
For all 3D charts the following options are the most important (part of _chart.options3d_):
모든 3D 차트는 아래의 옵션이 가장 중요하다. 

- enabled                   This indicates whether the chart has to have 3D or not, set this to true.
							이 속성은 3d를 사용할지 안할지 정하는 것이며 사용하려면 true를 주면된다.
- depth                     The total depth of the chart, defaults to 100.
							차트의 깊이를 뜻하며 기본값은 100이다.
- viewDistance              This defines how far a viewer is from the chart.
							사용자의 시점이 그래프에서 얼마나 먼지를(멀다) 정한다.
- alpha & beta              The angles to rotate the view of the chart.
							차트를 보는 시점의 각도를 이동한다.
```
depth :  차트의 z 축 사이즈 작으면 x 축에 해당하는 bottom의 화면 사이즈가 작아진다. ( frame의 bottom.size와 다름)
alpha :  숫자가 클 수록 시점이 점점 위에서 보는 시점이 된다. ( 0 일경우 카메라가 바닥에 있고 100 일경우 천장에 달림)
beta : 숫자가 클 수록 시점이 점점 오른쪽에서 보는 시점으로 변한다 ( 0: 왼쪽에서 바라 봄, 100: 오른쪽에서 바라 봄)

#### 5. 일반 속성
[[일반 속성]]

#### 6. series
시리즈에 type 속성을 따로 정의하지 않으면 chart의 type을 따른다.
시리즈는 3단계의 세팅값으로 적용이 되는데
1. 모든 시리즈에 적용이 되는 plotOptions.series
2. scatter3d 시리즈에만 적용이 되는 plotOptions.scatter3d
3. 각각의 series에 적용이 되는 array형식
```javascript
Highcharts.chart('container', {
    plotOptions: {
        series: {
            // general options for all series
        },
        scatter3d: {
            // shared options for all scatter3d series
        }
    },
    series: [{
        // specific options for this series instance
        type: 'scatter3d'
    }]
});
```


#highchart 