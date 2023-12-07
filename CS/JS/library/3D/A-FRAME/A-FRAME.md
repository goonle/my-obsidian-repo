
### 예제
---
```html
<html>  
  <head>  
    <script src="https://aframe.io/releases/1.5.0/aframe.min.js"></script>  
  </head>  
  <body>  
    <a-scene>  
      <a-box position="-1 0.5 -3" rotation="0 45 0" color="#4CC3D9"></a-box>  
      <a-sphere position="0 1.25 -5" radius="1.25" color="#EF2D5E"></a-sphere>  
      <a-cylinder position="1 0.75 -3" radius="0.5" height="1.5" color="#FFC65D"></a-cylinder>  
      <a-plane position="0 0 -4" rotation="-90 0 0" width="4" height="4" color="#7BC8A4"></a-plane>  
      <a-sky color="#ECECEC"></a-sky>  
    </a-scene>  
  </body>  
</html>
```

### 예측
---
##### 태그
위 코드르 보니 a-scene 테그 안에서 객체를 선언할 수 있는 것 같고 a-box, a-sphere, a-cylinder, a-plane, a-sky등 약속어를 사용하면 기본적인 3D 객체를 만들어 주는 듯 하다.

##### 속성
1. position :
	    x,y,z축의 좌표값으로 보이며
2.  rotation : 
	   회전 각도로 보이는데 띄어쓰기로 분리된 3가지는 각 축에대한 각도로 보이지만 소수점 단위는 삼각함수 값일 수도 있다는 생각이 든다.
3. color, height, width 는 기본적인 css로 보인다.

### 공식 사이트의 설명
---
A-frame은 VR 경험을 만들어내기 위한 웹 프레임워크 입니다. A-frame은 시작하기 쉽게 HTML 위에 그려집니다. 그렇다고 A-frame은 단순한 3D 씬 그래프거나 마크업 언어가 아닙니다. 코어는three.js를 통해 쉽게 선언할수 있고 확장가능하며 조합가능한 구조를 제공하는 강력한 엔티티 컴포넌트 프레임워크입니다.

원래 모질라에 의해 만들졌었지만 현재는 Supermedium안의 공동 창조자들에 의해 유지보수되고 있습니다 A-Frame은 VR 컨텐츠 개발을 위한 쉬우며 강력한 방식으로 개발되었습니다. 독립적인 오픈소스 프로젝트로써 A-Frame은 가장 커다란 VR 커뮤니티 중 하나로 성장했습니다.

A-Frame은 Vive, Rift, Windoes Mixed Reality, Cardbiard, Oculus Go와 같은 대부분의 VR 헤드셋울 지원하며 증강현실을 위해서도 사용가능합니다. 비록 A-Frame이 모든 스펙트럼을 지원하지만 A-Frame의 목표는 360도 컨텐츠를 넘어 모든 위치적 트레킹과 컨트롤러를  위한 완전히 상호작용가능한 VR 경험을 목표로 하고 있습니다.

### 특징 (by 공식 사이트)
---
##### VR을 간단하게
##### HTML에 선언
##### Entity-Component 구조
##### 크로스 플렛폼 VR
##### 성능
##### 시각적인 인스펙터
##### 컴포넌츠
##### 증명되고 확장 가능한 기능성

#a-frame
#js 
#3d 