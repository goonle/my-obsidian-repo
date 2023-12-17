[출처 : Yasunobu Ikeda - Many Icons in 3D using Three.js](https://codepen.io/clockmaker/pen/gpozrX)

위 코드펜의 소스를 분석하여 필요한 기능을 사용하기

### 목표
---
fontawesome의 아이콘을 3d로 구현하기

### 코드
---
```javascript
THREE.ImageUtils.crossOrigin = "*";

   /주석은 눈에 띄게 일부러 틀린방법 사용//
   /Basic 뷰는 window에 사용하기 쉽게 선언하는 함수//
   /생성함수가 존재하지만 코드의 가독성을 위해 본래 코드는 위 codepen에서 확인//
   
   /여기서부터 주의깊게 봐야할것 같다.//
   /보면 초기값 세팅을 하는 constructor를 만들어주고//
   /Class.prototype으로 overwrite를 해주는 모습이 보인다.//

    DemoIconsWorld.prototype.setup = function() {
      // ------------------------------
      // カメラの配置
      // ------------------------------
      this.camera.far = 100000;
      this.camera.near = 1;
      this.camera.position.z = 5000;
      this.camera.lookAt(this.HELPER_ZERO);

      // ------------------------------
      // 背景の作成
      // ------------------------------
      /번역기를 돌리니 배경을 작성하는 부분이라고 한다.//
      var plane = new THREE.PlaneBufferGeometry(50000, 50000, 1, 1);
      var mat = new THREE.MeshBasicMaterial({
        map: THREE.ImageUtils.loadTexture('http://ics-web.jp/lab-data/150601_threejs_mosaic/imgs/bg.png')
      });
      var bg = new THREE.Mesh(plane, mat);
      bg.position.z = -10000;
      this.scene.add(bg);
      this._bg = bg;

      // ------------------------------
      // 3D空間のパーツを配置
      // ------------------------------
      /이부분은 라이트를 설정하고 더해주는 부분//
      var light = new THREE.DirectionalLight(0xffffff);
      light.position.set(0, 1, +1).normalize();
      this.scene.add(light);
      // particle motion
      this._wrap = new THREE.Object3D();
      this.scene.add(this._wrap);
      // ------------------------------
      // パーティクルのテクスチャアトラスを生成
      // ------------------------------
      var container = new createjs.Container();
      var SIZE = 256;
      for (var i = 0, len = this._matrixLength * this._matrixLength; i < len; i++) {
        var char = String.fromCharCode(61730 + i);
        / **사실 이부분에서 텍스트를 container에 넣어주고//
        var text2 = new createjs.Text(char, "200px FontAwesome", "#FFF");
        text2.textBaseline = "middle";
        text2.textAlign = "center";
        text2.x = SIZE * (i % this._matrixLength) + SIZE / 2;
        text2.y = SIZE * Math.floor(i / this._matrixLength) + SIZE / 2;
        container.addChild(text2);
      }
      container.cache(0, 0, SIZE * this._matrixLength, SIZE * this._matrixLength);
      var cacheUrl = container.getCacheDataURL();
      var image = new Image();
      image.src = cacheUrl;
      / **이부분에서 이미지로 만들고 Textrue에 넣어서 //
      var texture = new THREE.Texture(image);
      texture.needsUpdate = true;
      // ------------------------------
      // パーティクルの作成
      // ------------------------------
      var ux = 1 / this._matrixLength;
      var uy = 1 / this._matrixLength;
      this._particleList = [];
      for (var i = 0; i < this.CANVAS_W; i++) {
        for (var j = 0; j < this.CANVAS_H; j++) {
          var ox = (this._matrixLength * Math.random()) >> 0;
          var oy = (this._matrixLength * Math.random()) >> 0;
          var geometry = new THREE.PlaneGeometry(40, 40, 1, 1);
          this.change_uvs(geometry, ux, uy, ox, oy);
          / **여기에 material로 만들고 //
          var material = new THREE.MeshLambertMaterial({
            color: 0xffffff,
            map: texture,
            transparent: true,
            side: THREE.DoubleSide
          });
          material.blending = THREE.AdditiveBlending;
          / **여기서 Mesh로 만든다음에//
          var word = new THREE.Mesh(geometry, material);
          / **_wrap 이라는 3dObjcet에 넣어준다.//
          / ** _wrap은 이미 scene에 들어있기 때문에 렌더링 된다. //
          this._wrap.add(word);
          this._particleList.push(word);
        }
      }
      this.createParticleCloud();
    };
    
    /이 아래의 코드는 애니메이션과 원하는 군집의 모양을 만드는 함수//
  
```

### 사용해야 할 코드
---
```javascript
var container = new createjs.Container();
//여기서 char은 문자
//String.fromCharCode(61730 + i) 여기의 의미를 모르겠음
// *** 찾아봐야함
var char = String.fromCharCode(61730 + i);
/ **사실 이부분에서 텍스트를 container에 넣어주고//
var text2 = new createjs.Text(char, "200px FontAwesome", "#FFF");
text2.textBaseline = "middle";
text2.textAlign = "center";
text2.x = SIZE * (i % this._matrixLength) + SIZE / 2;
text2.y = SIZE * Math.floor(i / this._matrixLength) + SIZE / 2;
container.addChild(text2);
		
container.cache(0, 0, SIZE * this._matrixLength, SIZE * this._matrixLength);


//cacheUrl도 의미를 모름
var cacheUrl = container.getCacheDataURL();
var image = new Image();
image.src = cacheUrl;
/ **이부분에서 이미지로 만들고 Textrue에 넣어서 //
var texture = new THREE.Texture(image);
//needsUpdate도 의미를 찾아야함
texture.needsUpdate = true;

/ **여기에 material로 만들고 //
var material = new THREE.MeshLambertMaterial({
	color: 0xffffff,
	map: texture,
	transparent: true,
	side: THREE.DoubleSide
});

 material.blending = THREE.AdditiveBlending;
/ **여기서 Mesh로 만든다음에//
var word = new THREE.Mesh(geometry, material);
/ **_wrap 이라는 3dObjcet에 넣어준다.//
/ ** _wrap은 이미 scene에 들어있기 때문에 렌더링 된다. //
//this._wrap.add(word);
/위 코드를 변경하여 //
var wrapper = new THREE.Object3D();
wrapper.add(word);
var scene = new THREE.scene();
scene.add(wrapper);
var renderer = new THREE.webGLRenderer();
renderer.add(scene);
```

위 코드를 사용하기 위해서 알아야 할 것들이 있다.
1.  [[createjs]]
2. [[String.fromCharCode()]]
3. [[fontawesome icon hex code]]