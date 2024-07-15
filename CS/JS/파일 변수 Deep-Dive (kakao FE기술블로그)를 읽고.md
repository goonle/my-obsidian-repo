우리의 회사는 현재 react, redux, next, express 등을 사용하지 않고 있습니다.
제겐 상태 처리라는 것이 잘 와닿지 않는 개념으로, 모르는 용어 혹은 개념이 있어 어려움이 있었지만 새롭게 알게 된 사실이 있어 이를 약간 정리해봤습니다.

그 전에 원글 [파일 변수 - Deep-Dive by 이혁원(bill) from kakao entertainment FE 기술블로그](https://fe-developers.kakaoent.com/2024/240715-handling-file-variables/)에 대한 링크를 남깁니다.

본래 글의 취지는 웹서비스가 점점 커져감에 따라서 편의성을 위해 전역 **상태**관리 툴인 Redux를 너무 많이 사용하여 코드 가독성이 떨어지고 관리가 힘들어져서 상태를 유형별로 나누고 Redux로 사용하던 상태값을 파일의 전역변수로 사용하는 이유와 방식에 대해 설명하고 있습니다.

하지만 우리는 상태관리를 하기 때문에 제가 모르던 것, 알게된 것에 대해 적어보았습니다.

## 1. Class 내의 private 변수
---
올해 들어서 클래스를 활용한 화면 컴포넌트를 위한 class를 만든 적이 있습니다. 최근에는 길 책임님도 복잡한 화면과 코드를 단순화하고자 작성을 했습니다. 그 때 제게 물었던 질문 중에 "*클래스 내부의 함수에 접근이 가능하느냐"* 라는 것이 있었는데 그 때는 JS의 특성상 접근이 가능하기 때문에 내부함수에는 \_(언더바)를 붙이는 관습이 있으며, 이는 개발자끼리의 약속으로 알고 있다고 말씀드렸었지만 \#을 붙임으로써 실제로 접근할 수 없는 내부 private 변수를 만들 수 있음을 이 글을 통해 확인했습니다.

[Private properties by MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_properties)

```javascript
class Device {
  // Private 변수 선언
  #isMobileServer;
  #isMobileClient;

  constructor(isMobile) {
    this.#isMobileServer = isMobile;
    this.#isMobileClient = isMobile;
  }

  // setter 함수
  setIsMobile(value) {
    this.#isMobileServer = value;
    this.#isMobileClient = value;
  }

  // Public method to get the value of the fields
  getIsMobile() {
    return {
      isMobileServer: this.#isMobileServer,
      isMobileClient: this.#isMobileClient,
    };
  }
}

const device = new Device(true);

console.log(device.getIsMobile()); 
// { isMobileServer: true, isMobileClient: true }

device.setIsMobile(false);
console.log(device.getIsMobile()); 
// { isMobileServer: false, isMobileClient: false }

// 내부 private 변수에 접근하거나 수정하려할 경우
console.log(device.#isMobileServer); 
// SyntaxError: Private field '#isMobileServer' must be declared in an enclosing class
device.#isMobileServer = true; 
// SyntaxError: Private field '#isMobileServer' must be declared in an enclosing class

```
## 2. 변수 스코프
---
##### 1. 전역 범위 
##### 2. 함수 범위
##### 3.  블록 범위
- let, const는 중괄호 안에서만 접근이 가능합니다.
##### 4. 모듈 범위
- ES6 문법을 사용할 경우 특정 파일 내에서 export문을 사용한다면 해당 파일 자체가 모듈이 됩니다.

## 3. 서버 사이드에서 모듈 안의 전역변수는 모든 유저가 공유된다.


# 마무리
---
 FE 기술 블로그로써 많은 문서를 참조했다는 것에 FE의 영역이 단지 화면 만을 고려하는 것이 아님을 알게 되었습니다. 