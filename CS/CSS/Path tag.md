
# 기본 명령어 
---
>[!info] 명령어
>M : moveTo (한점에서 한점으로 이동)
>L :  lineTo (선을 만든다)
>H : horizontal lineTo(수평선을 만든다)
>V : vertical lineTo (수직선을 만든다.)
>C : curveTo (곡선을 만든다)
>S : smooth curve to ( 부드러운 곡선을 만든다.)
>Q :  quadratic Bezier curveTo (베지에 곡선을 만든다 ( 여러점으로 만드는 곡선))
>T : smooth quadratic Bezier curveTo (부드러운 베지에 곡선을 만든다.)
>A : elliptical Arc ( elliptical Arc를 만든다 (삼각함수 ? 좌표로 만드는 곡선))
>Z : closepath ( 선을 닫음)

# 기본 주의 사항
---
1. x 와 y의 좌표값은 좌측 상단을 0으로 치고 아래와 오른쪽으로 값을 더하며 생긴다. 기본적으로 알고 있는 좌표에서 y좌표가 반대로 된 느낌

# 예제
---
## example 1
```html
<svg height="210" width="400" xmlns="http://www.w3.org/2000/svg">  
  <path d="M150 5 L75 200 L225 200 Z"  
  style="fill:none;stroke:green;stroke-width:3" />  
</svg>
```

### 해석
1. M150 5 L75 200
	- 점 (150, 0) 에서 점(75 200)으로 이동하며 선을 그려라.  그리고 점 (225,200) 으로 선을 만들어라. 
2. L225 200 
	- 점 (75, 200) 에서 점(225, 200)으로 점을 이동하며 선을 만들어라
3. Z
	- 작성된 선을 닫아라

## example2
```html
<svg height="400" width="450" xmlns="http://www.w3.org/2000/svg">  
  
<!-- Draw the paths -->  
<path id="lineAB" d="M 100 350 L 150 -300" stroke="red" stroke-width="4"/>  
<path id="lineBC" d="M 250 50 L 150 300" stroke="red" stroke-width="4"/>  
<path id="lineMID" d="M 175 200 L 150 0" stroke="green" stroke-width="4"/>  
<path id="lineAC" d="M 100 350 Q 150 -300 300 0" stroke="blue" stroke-width="4" fill="none"/>  
  
<!-- Mark relevant points -->  
<g stroke="black" stroke-width="3" fill="black">  
<circle id="pointA" cx="100" cy="350" r="4" />  
<circle id="pointB" cx="250" cy="50" r="4" />  
<circle id="pointC" cx="400" cy="350" r="4" />  
</g>  
  
<!-- Label the points -->  
<g font-size="30" font-family="sans-serif" fill="green" text-anchor="middle">  
<text x="100" y="350" dx="-30">A</text>  
<text x="250" y="50" dy="-10">B</text>  
<text x="400" y="350" dx="30">C</text>  
</g>  
  
</svg>
```
