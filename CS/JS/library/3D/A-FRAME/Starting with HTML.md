
### Placing our Box in Front of the Camear
---
```html
<html>
  <head>
    <script src="https://aframe.io/releases/1.5.0/aframe.min.js"></script>
  </head>
  <body>
	<a-scene>
	  <a-box color="red" position="0 2 -5" rotation="0 45 45" scale="2 2 2"></a-box>
	</a-scene>
  </body>
</html>
```


### 부모와 자식
---
```html
<a-scene>
  <a-box position="0 2 -5" rotation="0 45 45" scale="1 1 1" color="purple">
    <a-sphere position="1 1 1" color="green"></a-sphere>
  </a-box>
</a-scene>
```
A-Frame HTML은 3D Scene 그래프를 표현한다. 씬 그래프에서 엔티티들은 하나의 부모와 여러 자식을 가질 수 있다. 자식 엔티티들은 부모 엔티티의 속성을 상속한다.

### 환경(배경)추가
---
A-Frame은 개발자들이 재사용 가능한 컴포넌트를 다른 이들과 공유하고 만들 수 있도록 허용한다. [@feiss](https://github.com/feiss/)의 환경 컴포넌트는 단 한줄의 html 코드로 전체 환경에 대한 다양성을 단꼐적으로 만들고 있다. 이 환경 컴포넌트는 VR 애플리케이션을 시각적으로 빠르게 시작할 수 있는 훌륭하고 간편한 방법으로, 다수의 매개변수와 함께 수십 개의 환경을 제공합니다:

먼저, A-Frame 뒤에 스크립트 테그를  사용하여 환경변수를 include해줍니다.
```html
<head>
  <script src="https://aframe.io/releases/1.5.0/aframe.min.js"></script>
  <script src="https://unpkg.com/aframe-environment-component/dist/aframe-environment-component.min.js"></script>
</head>
```

그리고 이 씬안에 환경변수를 붙인 엔티티를 추가합니다. 우리는 프리셋 하나를 수많은 다른 파라미터와 함께 구체적으로 선언할 수 있습니다.
```html
<a-scene>  
  <a-box color="red" position="0 2 -5" rotation="0 45 45" scale="2 2 2"></a-box>  
  
  <!-- Out of the box environment! -->  
  <a-entity environment="preset: forest; dressingAmount: 500"></a-entity>  
</a-scene>
```

### 이미지 텍스쳐(겉면) 적용하기
---
>[!important]
>텍스처를 올바르게 적용하기 위해서는 당신의 html이 로컬서버에서 동작하는지 확실하게 해야한다.

마치 우리가 보통의 \<img/\>를 사용하는 것처럼 박스에 이미지, 비디오, \<canvas\>를 src 속성을 사용하여 이미지 텍스쳐를 사용할 수 잇다.  또한 우리는 반드시 color="red" 속성을 지워야 한다. 지우지 않으면 색과 텍스쳐가 섞일 수 있다. 기본 재질 색은 화이트이다. 그렇기 때문에 컬러 속성을 지우는 것 만으로 충분하다. 
``` html
<a-scene>
  <a-box src="https://i.imgur.com/mYmmbrp.jpg" position="0 2 -5" rotation="0 45 45"
    scale="2 2 2"></a-box>

  <a-sky color="#222"></a-sky>
</a-scene>
```

### 바닥 적용하기
---
```html
<a-plane rotation="-90 0 0"></a-plane>
```

### 애니메이션 적용하기
---
```html
<a-scene>
  <a-assets>
    <img id="boxTexture" src="https://i.imgur.com/mYmmbrp.jpg">
  </a-assets>

  <a-box src="#boxTexture" position="0 2 -5" rotation="0 45 45" scale="2 2 2"
         animation="property: object3D.position.y; to: 2.2; dir: alternate; dur: 2000; loop: true"></a-box>
</a-scene>
```

[출처: a-frame 공식사이트 - Building a Basic Scene ](https://aframe.io/docs/1.5.0/guides/building-a-basic-scene.html)
  