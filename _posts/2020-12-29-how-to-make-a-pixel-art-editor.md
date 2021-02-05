---
layout: post
title: "HTML5 Canvas를 사용하여 픽셀 아트 편집기를 만드는 방법"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/flagged/photo-1562599838-8cc871c241a5?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDF8fHBpeGVsfGVufDB8fHw&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


웹은 물건을 만들기에 좋은 장소이며, 당신의 창작물을 보여줄 수 있는 좋은 장소이기도 합니다. 픽셀 아트 편집기는 웹 개발 기술을 테스트하는 재미있는 프로젝트입니다. 그것은 여러분의 창의성을 보여줄 수 있고 많은 잠재 고객을 확보할 수 있습니다.

픽셀 아트가 뭐냐고 물으실지 모르겠습니다.

> 픽셀 아트(Pixel art)는 디지털 아트의 한 형태로, 픽셀 레벨에서 이미지가 편집되는 소프트웨어 사용을 통해 만들어진다.

우리는 당신의 향후 노력에 도움이 될 이 프로젝트를 구축하기 위해 많은 현대 웹 기술을 사용할 것입니다. 자, 이제 시작하겠습니다.

## 사용된 기술

프로젝트에서는 다음 웹 기술을 사용할 것입니다.

- HTML5 캔버스
- 응답성 설계를 위한 CSS 미디어 쿼리
- GIF 생성을 위한 gif.js 라이브러리
- 애플리케이션 같은 환경을 위한 PWA(Progressive Web Apps)
- 객체 지향 설계

## 편집자의 특징

만들 웹 앱에는 다음과 같은 기능이 있습니다.

- 반응성 설계(모바일 친화적)
- 픽셀 아트의 치수 설정
- 선, 원, 타원, 페인트 등의 기본 그리기 도구
- 프레임별 애니메이션 GIF 작성 기능.

## HTML5 Canvas란?

캔버스(Canvas)는 웹 페이지에서 그래픽을 그리는 데 사용할 수 있는 HTML 요소입니다. 그것은 우리가 단순하고 복잡한 그래픽 객체를 형성할 수 있습니다.

캔버스 이전에 개발자들은 그러한 애니메이션을 만들기 위해 플래시를 사용해야 했고, 이 애니메이션은 웹 페이지에 포함되어 있었다. 캔버스는 플래시에 비해 많은 장점이 있으며 웹 페이지에 그래픽을 표시하는 데 널리 사용됩니다.

예를 들어 `<canvas> 태그를 사용하여 캔버스를 만들 수 있습니다.

```html
<canvas id="drawing" width="500" height="500"></canvas>
```

이렇게 하면 빈 500 X 500 캔버스가 만들어집니다. 캔버스는 HTML 요소이기 때문에, 모든 CSS 속성은 캔버스에도 적용될 수 있다.

예를 들어 SVG와 같이 HTML 페이지에 그래픽을 표시하는 다른 옵션이 있습니다. 그러나 우리는 캔버스를 비트맵 이미지에 더 적합하기 때문에 사용할 것이며, 픽셀 아트는 본질적으로 비트맵 이미지의 집합이다.

## 편집기를 설계하는 방법

우리는 우리의 앱을 PixelCraft라고 부를 것이다. 저희 앱의 전체 소스 코드와 데모를 여기서 확인하실 수 있습니다.

앱을 만드는 첫 번째 단계는 사용자 인터페이스를 설계하는 것입니다. 좋은 UI는 모든 화면 크기에 맞게 조정되어야 하며 쉽게 액세스할 수 있어야 합니다.

앱의 UI는 다음과 같습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-173.png)

응답성이 뛰어나 모바일 기기처럼 작은 화면 크기에 자동으로 적응할 수 있다.

### 대화 상자 만드는 방법

앱을 열면 차원을 묻는 대화 상자가 표시됩니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-176.png)

팝업의 HTML 코드는 다음과 같습니다.

```html
<div id="popup">
<h3>Select the Dimensions Of the grid</h3>
<input type="text" id="width" value="16">X<input type="text" id="height" value="16">
<button id="close">OK</button>
</div>
```

CSS는 다음과 같습니다.

```css
#popup {
  background-color: #332f35;
  color: white;
  font-size: 20px;
  padding: 30px;
  box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.5);
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%) scale(0.1, 0.1);
  text-align: center;
  max-width: 420px;
  width: 70%;
  transition: 0.2s all;
  z-index: 2;
  border-radius: 5px;
  display: none;
}
```

여기서 중요한 속성은 화면 어디에나 대화 상자를 배치할 수 있는 `위치: 고정`입니다. 왼쪽:50%와 위쪽:50%는 대화 상자의 왼쪽 상단 모서리를 페이지 중앙에 배치합니다.

대화 상자의 중심을 페이지 센터에 맞추려면 페이지 중앙에 배치하는 `변환: 번역(-50%-50%)`을 사용합니다.

처음에는 페이지 로드 시 `display` 속성이 none으로 설정됩니다. 그래서 우리는 대화 상자를 표시하기 위해 `display:block`으로 바꿀 것이다.

### 캔버스 그리는 방법

사용자가 치수를 선택하면 해당 치수를 기준으로 캔버스 요소가 만들어집니다. 캔버스 구성요소는 페이지 중앙에 위치합니다.

```html
<canvas id="canvas"></canvas>
```

캔버스에 필요한 HTML 코드는 그것뿐입니다. 다른 모든 속성은 JavaScript를 사용하여 설정됩니다. 모든 도면 작업은 또한 그래픽을 표시하는 데 매우 유용한 캔버스를 만드는 JavaScript를 사용하여 수행됩니다.

캔버스 요소에 필요한 CSS는 다음과 같습니다.

```css
#canvas {
  box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.5);
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 75%;
  max-width: 550px;
  display: none;
  cursor: crosshair;
  touch-action: none;
}
```

페이지의 캔버스를 중앙에 배치하는 데 필요한 CSS 속성은 대화상자의 특성과 동일합니다. 터치 동작: 없음 속성은 캔버스에 그림을 그리는 동안 다른 스와이프 동작을 비활성화하기 때문에 모바일 장치에 유용합니다.

### 도구 모음 및 색상표를 작성하는 방법

생성하려는 다른 UI 요소는 도구 모음과 색상 팔레트입니다. 이들은 각각 왼쪽 가장자리와 오른쪽 가장자리에 정렬됩니다.

그러나 작은 화면에서는 데스크톱에 비해 수평 공간이 작습니다. 이것은 우리가 아래와 같이, 상부의 모바일 장치에 화면의 바닥에 이사를 할 것 같다는 것을 의미한다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-177.png)

이를 위해 CSS 미디어 쿼리를 사용할 것입니다. 특정 화면 크기에서만 특정 CSS 규칙 집합을 사용할 수 있게 해주므로 모바일에서만 실행되는 CSS를 추가할 수 있습니다.

이것은 우리 앱이 휴대폰에 있는 사람들에게 모바일 친화적이 될 뿐만 아니라, 데스크탑 버전에서도 사용 가능한 모든 공간을 사용할 수 있게 할 것이다.

도구 모음의 HTML은 다음과 같습니다.

```html
<div id="toolbar">
<span class="item"><i class="fas fa-pencil-alt"></i></span>
<span class="item"><i class="fas fa-eraser"></i></span>
<!-- for every toolbar item -->
</div>
```

`i` 태그는 글꼴 멋진 아이콘에 대한 것으로, 많은 범용 아이콘이 포함되어 있습니다. 이 도구 모음의 CSS는 다음과 같습니다.

```css
#toolbar {
  position: fixed;
  top: 50%;
  left: 0%; /* align to left */
  transform: translateY(-50%);
  padding: 0px;
  color: white;
  max-width: 150px;
}

#toolbar .item {
  display: inline-block;
  float: left; /* toolbar items stack to left */
  padding: 15px;
  border: 1px solid #FFF;
  cursor: pointer;
  height: 32px;
  width: 32px;
  font-family: Arial, FontAwesome;
  font-size: 24px;
}
```

CSS 미디어 쿼리를 사용하려면 CSS에 다음을 추가해야 합니다.

```css
@media only screen and (max-width: 600px) {
  /* CSS added here will only be used on screen-width smaller than 600px */   
}
```

이 미디어 쿼리에서, 우리는 화면 하단에 도구 모음을 정렬하기 위해 CSS를 추가하고 있습니다.

마찬가지로 색상 팔레트는 데스크톱의 화면 오른쪽과 모바일 장치의 화면 맨 위에 정렬됩니다. 이 세 가지 구성 요소를 사용하면 UI의 설계 부분이 완성됩니다. UI를 만들 때 자신만의 창의력을 발휘해 볼 것을 적극 추천합니다.

## 앱의 기능을 만드는 방법

저희 앱의 디자인이 준비되었으니, 이제 기능을 추가하겠습니다. 우리는 앞으로 새로운 기능을 더 쉽게 추가할 수 있도록 자바스크립트의 객체 지향적인 특성을 사용할 것이다.

개체 지향 설계는 개체와 관련된 모든 속성 및 메서드를 함께 그룹화해야 함을 의미합니다.

우리 디자인에서 캔버스는 하나의 객체가 될 것이기 때문에 캔버스 요소의 모든 특성과 그 방법이 하나의 캔버스 클래스에서 함께 있어야 한다.

```undefined
class Canvas {
  constructor(width, height) {}  // initialize all canvas properties
    
  draw(x, y) {}  // method to draw a pixel on canvas
    
  erase(x, y){}  // method to erase a pixel on canvas
    
  setcolor(color) {}  // method to set the current color
    
  setmode(i) {}  // method to set the active tool
    
  save() {}  // method to save pixel art as image

  clear() {}  // method to clear canvas

  addFrame() {}  // method to add current frame to frame list

  deleteFrame(f) {}  // method to delete a specific frame

  loadFrame(f) {}  // method to load a specific frame onto canvas

  renderGIF() {}  // method to render a GIF using frames

  undo() {}  // method to undo a given step

  redo() {}  // method to redo a given step

  addImage() {}  // method to load an image as pixel art
}
```

생성자는 클래스의 인스턴스가 생성될 때마다 실행됩니다. 개체의 속성을 초기화하는 데 사용됩니다. 우리의 경우, 캔버스의 폭과 높이가 생성자에서 설정됩니다.

마우스 이동 또는 스와이프 동작을 사용하여 캔버스에 그림을 그리려면 이벤트 수신기를 캔버스에 추가해야 합니다. 데스크톱에서 마우스 움직임을 감지하는 이벤트 수신기는 마우스 이동입니다. 모바일 기기에서는 터치 무브(touch move)다.

이벤트 수신기는 다음과 같이 설정할 수 있습니다.

```undefined
var canvas = document.querySelector("#canvas");

canvas.addEventListener("mousemove", e => {
      if (this.active) {
        var rect = canvas.getBoundingClientRect();
        var x = e.clientX - rect.left;
        var y = e.clientY - rect.top;
        x = Math.floor(this.width * x / canvas.clientWidth);
        y = Math.floor(this.height * y / canvas.clientHeight);
        if(tools[Tool.pen]) {
          this.draw(x, y)
        }
        else if(tools[Tool.eraser]) {
          this.erase(x, y);
        }
      }
});
```

이벤트 수신기를 설정하고 이벤트가 발생하면 이벤트와 관련된 데이터를 포함하는 이벤트 핸들러에 매개 변수 `e`가 전달됩니다.

이 경우 마우스 좌표는 이 매개 변수에서 찾을 수 있습니다. 이 좌표는 페이지와 관련하여 참조되지만, 우리는 캔버스에 관한 좌표가 필요합니다. 이를 위해 getBoundingClientRect() 방법을 사용한다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-178.png)

이렇게 하면 캔버스 요소의 경계 사각형이 제공되어 캔버스와 관련하여 마우스 좌표를 찾는 데 사용할 수 있습니다. 이 좌표는 여전히 픽셀 단위입니다.

캔버스를 초기화할 때 일정한 폭과 높이를 차원으로 지정했습니다. 가로, 세로 방향으로 원하는 픽셀 수입니다. 따라서 마우스 좌표는 이러한 단위로 변환해야 합니다.

JavaScript를 사용하여 찾은 좌표는 페이지와 관련하여 픽셀 단위입니다. 예를 들어, 캔버스의 CSS 치수가 320 X 320이고 16 X 16 픽셀 이미지를 만든 경우 각 픽셀은 약 320/16 = 20 픽셀이 됩니다.

따라서 JavaScript를 사용하여 발견된 좌표가 (40, 60)이면 픽셀 좌표는 (40*16/320, 60*16/320)이 됩니다. 모든 좌표는 이렇게 변환해야 합니다.

### 그리기 방법 사용 방법

우리는 캔버스의 주어진 좌표에서 픽셀을 그리기 위해 `draw` 방법을 사용할 것이다. 주어진 크기의 픽셀을 그리기 위해 캔버스 컨텍스트의 fillRect() 방법을 사용할 것이다. 예를 들면,

```undefined
var canvas = document.querySelector("#canvas");
var ctx = canvas.getContext('2d');

ctx.fillRect(10,10,50,50);  

// creates a 50 X 50 rectangle with upper-left corner at (10,10)
```

### 'set color' 방법 사용 방법

설정된 색상은 모든 그리기 작업에 사용되는 캔버스에 활성 색상을 사용합니다. 우리는 캔버스 컨텍스트의 fillStyle 속성을 사용할 것이다.

```undefined
var canvas = document.querySelector("#canvas");
var ctx = canvas.getContext('2d');

ctx.fillStyle = "rgba(255,0,0,255)";

// Sets the canvas color to red
```

### 프레임 추가 방법 사용 방법

현재 캔버스 상태에서 프레임을 만들기 위해 `AddFrame` 방법을 사용합니다. 이 프레임은 나중에 GIF 렌더링에 사용됩니다. 모든 프레임은 배열에 저장됩니다. 캔버스는 `toData URL()` 방법을 사용하여 영상으로 저장할 수 있습니다.

### 설정 모드 사용 방법

set mode(설정 모드) 메서드는 현재 활성 상태인 도구를 저장합니다. 이것은 마우스 이벤트에서 어떤 작업이 수행될 것인지를 결정하기 때문에 중요합니다. 마우스 이벤트는 활성 도구를 기준으로 연필, 지우개, 원, 타원 등이 될 수 있습니다.

### undo 및 redo 방법 사용 방법

`ㄹ`과 `ㄹ` 방법은 되돌아가거나 다시 실행된다. 이 작업은 모든 단계를 배열에 저장하여 수행할 수 있습니다. 실행 취소가 호출될 때마다 단계 배열에서 한 단계가 제거되고 redo 배열에 추가됩니다. redo를 호출하면 하나의 요소가 redo 배열에서 제거되고 단계 배열에 추가됩니다.

## 애니메이션 GIF 만드는 방법

저희 앱의 가장 중요한 기능 중 하나는 GIF 애니메이션 제작 능력입니다. 하지만 캔버스는 우리에게 애니메이션 GIF를 만드는 어떠한 방법도 제공하지 않습니다. 대신, 우리는 이 목적을 위해 외부 라이브러리를 사용해야 할 것입니다.

우리는 앱에 gif.js를 사용할 것입니다. 프레임에서 GIF를 렌더링하는 빠르고 인기있는 라이브러리입니다.

gif.js를 사용하려면 라이브러리를 다운로드하여 페이지로 가져와야 합니다. 가져오면 다음과 같이 GIF 작업자를 초기화해야 합니다.

```undefined
var gif = new GIF({
  workers: 2,
  quality: 10,
  width: width,  // width of GIF
  height: height  // Height of GIF
});

gif.on('finished', function (blob) {
  var url = URL.createObjectURL(blob);
  var link = document.createElement('a');
  link.download = 'canvas.gif';
  link.href = url;  // download GIF after rendering
  link.click();
});
```

위의 코드는 GIF 작업자를 초기화하고 렌더링이 완료되면 GIF를 다운로드합니다.

GIF를 생성하려면 이 작업자에 프레임을 추가해야 합니다. 다음과 같이 할 수 있습니다.

```undefined
gif.addFrame(img, {
  copy: true,
  delay: 100  // Delay of frame in milliseconds
});
```

우리는 계속해서 우리의 GIF에 프레임을 추가할 것입니다. 프레임 추가를 마치면 gif.render() 함수를 사용하여 프레임에서 GIF를 렌더링할 수 있습니다. 호출하면 배경 작업자가 프레임에서 GIF를 렌더링합니다. GIF가 준비되면 다운로드됩니다.

이것으로, 우리는 픽셀 아트 에디터를 만드는 것을 마쳤습니다. 애니메이션 GIF뿐만 아니라 이미지 생성에도 사용할 수 있습니다.

## 결론

이 튜토리얼에서는 HTML5 캔버스를 사용하여 픽셀 아트 편집기를 만들었다. 편집기를 만드는 동안, 우리는 많은 웹 기술을 사용했습니다. 응답성 UI를 생성하는 방법과 개체 지향 설계를 사용하여 유지관리 가능한 코드를 작성하는 방법을 배웠습니다.

다시 한 번 말씀드리지만, 이 프로젝트는 여기서 찾을 수 있습니다. 또한 모든 기능이 포함된 앱의 작동 데모도 포함되어 있습니다.

우리가 이 기사에서 논의한 것은 가능한 것에 비해 여전히 매우 간단하다. 앱을 훨씬 더 재미있게 만들기 위해 많은 기능을 추가할 수 있습니다. 재미있게 놀다 오세요.

야, 네가 이 기사를 좋아하고 뭔가 배웠길 바라. 넌 내 인터넷 집에서 날 찾을 수 있어, 애비야.github.io이나 내 Github에. 내 다른 기사들도 확인해 봐. 감사합니다.