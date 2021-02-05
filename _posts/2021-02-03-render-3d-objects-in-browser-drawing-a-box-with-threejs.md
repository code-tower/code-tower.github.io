---
layout: post
title: "브라우저에서 3D 개체를 렌더링하는 방법: 3.js로 상자 그리기"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/02/Stack.002-1.jpeg
tags: undefined
---


만약 당신이 자바스크립트로 게임을 만들고 싶다면, 당신은 Three.js를 만났을 것이다.

Three.js는 브라우저에서 3D 그래픽을 렌더링하는 데 사용할 수 있는 라이브러리입니다. 모든 것이 자바스크립트에 포함되어 있기 때문에, 어떤 논리로 애니메이션을 추가하거나, 상호 작용을 하거나, 게임을 게임으로 만들 수도 있습니다.

이 튜토리얼에서는 매우 간단한 예를 살펴보겠습니다. 우리는 3D 상자를 만들고, 그렇게 하는 동안 Three.js의 기본 원리를 배울 것입니다.

Three.js는 후드 아래에서 WebGL을 사용하여 3D 그래픽을 렌더링합니다. 우리는 평범한 WebGL을 사용할 수 있지만, 매우 복잡하고 다소 낮은 수준입니다. 반면에 Three.js는 레고를 가지고 노는 것과 같다.

이 기사에서는 3D 물체를 장면에 배치하고 조명과 카메라를 설정하고 캔버스에 장면을 렌더링하는 방법에 대해 살펴보겠습니다. 자, 우리가 어떻게 이 모든 것을 할 수 있는지 봅시다.

## 장면 개체 정의

먼저, 장면을 정의해야 합니다. 이것은 3D 객체와 조명을 설치하는 컨테이너가 될 것입니다. 장면 개체에는 배경색과 같은 일부 속성도 있습니다. 그러나 이 설정은 선택 사항입니다. 설정하지 않으면 기본값은 검은색입니다.

```undefined
import * as THREE from "three";

const scene = new THREE.Scene();
scene.background = new THREE.Color(0x000000); // Optional, black is default

...
```

## 형상 + 재료 = 망사

그리고 3D 박스를 그물망으로 현장에 추가합니다. 망사(mesh)는 기하학과 재료의 조합이다.

```undefined
...

// Add a cube to the scene
const geometry = new THREE.BoxGeometry(3, 1, 3); // width, height, depth
const material = new THREE.MeshLambertMaterial({ color: 0xfb8e00 });
const mesh = new THREE.Mesh(geometry, material);
mesh.position.set(0, 0, 0); // Optional, 0,0,0 is the default
scene.add(mesh);

...
```

### 지오메트리란?

기하학은 우리가 만들고 있는 상자처럼 렌더링된 모양입니다. 지오메트리는 꼭짓점에서 빌드하거나 미리 정의된 지오메트리를 사용할 수 있습니다.

BoxGeometry는 가장 기본적인 사전 정의된 옵션입니다. 우리는 상자의 폭, 높이, 깊이만 설정하면 됩니다.

상자를 정의하면 멀리 갈 수 없다고 생각할 수도 있지만, 미니멀한 디자인의 많은 게임들은 상자 조합만 사용합니다.

미리 정의된 다른 지오메트리도 있습니다. 평면, 원통, 구 또는 심지어 이코사면체를 쉽게 정의할 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/freecodecamp-4.001.jpeg)

### 재료 작업 방법

그런 다음 재료를 정의합니다. 재료는 물체의 모양을 나타냅니다. 여기서 텍스처, 색상 또는 불투명도와 같은 항목을 정의할 수 있습니다.

이 예에서는 색상만 설정하려고 합니다. 재료에 대한 다양한 옵션이 있습니다. 그들 대부분은 빛에 어떻게 반응하느냐가 주된 차이점이에요.

가장 간단한 것은 메쉬 기본 재료입니다. 이 재료는 빛에 전혀 신경 쓰지 않고, 각 면마다 같은 색이 될 거예요. 그러나 상자의 가장자리가 보이지 않기 때문에 최상의 옵션은 아닐 수 있습니다.

빛에 관심을 갖는 가장 단순한 물질은 메쉬 램버트 재료입니다. 그러면 실질적으로 각 변인 각 정점의 색상이 계산됩니다. 하지만 그 이상은 아닙니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/freecodecamp-4.002.jpeg)

좀 더 정밀도가 필요하다면 고급 소재가 더 많다. MeshPhong 재료는 꼭짓점뿐만 아니라 각 픽셀별로 색상을 계산합니다. 색상은 측면 내에서 변경될 수 있습니다. 이는 사실성에 도움이 될 수 있지만 성능에도 비용이 듭니다.

또한 실제 효과가 있는 경우 조명 설정과 지오메트리에 따라 달라집니다. 우리가 박스를 렌더링하고 방향등을 사용한다면 결과는 그렇게 많이 변하지 않을 거예요. 하지만 우리가 구를 만든다면, 그 차이는 더 명백합니다.

### 망사 배치 방법

망사가 있으면 장면 내에서 망사를 배치하고 각 축별로 회전을 설정할 수도 있습니다. 나중에 3D 공간에서 개체를 애니메이션화하려면 이 값을 대부분 조정합니다.

포지셔닝에는 크기를 설정하는 데 사용한 것과 동일한 단위를 사용합니다. 작은 숫자를 사용하든 큰 수를 사용하든 상관 없으며, 자신만의 세계에서 일관성을 유지하면 됩니다.

회전의 경우 값을 라디안으로 설정합니다. 그래서 만약 여러분이 각도로 값을 가지고 있다면, 여러분은 그것들을 180°로 나눈 다음 PI로 곱해야 합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/freecodecamp-3.004.jpeg)

## 빛을 추가하는 방법

그럼 조명을 추가해볼까요? 기본 소재를 사용한 망사는 조명 설정에 상관없이 그물망 색상이 설정되기 때문에 빛이 필요 없습니다.

그러나 Lambert 소재와 Phong 소재는 빛을 필요로 한다. 빛이 없다면 그물망은 어둠 속에 남게 될 것이다.

```undefined
...

// Set up lights
const ambientLight = new THREE.AmbientLight(0xffffff, 0.6);
scene.add(ambientLight);

...
```

주변 조명과 방향 조명 등 두 개의 조명을 추가할 예정입니다.

먼저 주변 조명을 추가합니다. 주변 조명은 모든 방향에서 빛나며, 우리의 기하학적인 색상에 기본 색을 부여합니다.

주변 조명을 설정하기 위해 색상과 명암을 설정합니다. 색상은 보통 흰색이지만 아무 색이나 설정할 수 있습니다. 강도는 0과 1 사이의 숫자입니다. 우리가 정의하는 두 개의 조명은 누적된 방식으로 작동하기 때문에 이 경우 각각에 대해 강도가 약 0.5가 되어야 합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/freecodecamp-3.003.jpeg)

방향등의 설정은 비슷하지만 위치도 있습니다. 여기 있는 단어 위치는 약간 오해의 소지가 있습니다. 왜냐하면 빛이 정확한 위치에서 오는 것을 의미하지 않기 때문입니다.

방향광은 아주 먼 곳에서 빛나고 있으며, 많은 평행 광선들이 고정된 각도를 가지고 있다. 하지만 각도를 정의하는 대신, 우리는 하나의 광선의 방향을 정의합니다.

이 경우, 10,20,0 위치의 방향에서 0,0,0 좌표를 향하여 빛납니다. 하지만 물론, 방향광은 하나의 광선일 뿐만 아니라 무한한 양의 병렬광선입니다.

태양이라고 생각하세요. 더 작은 규모로 보면, 태양의 광선 또한 평행하게 내려오고, 태양의 위치는 중요한 것이 아니라 방향이다.

그리고 그것이 방향광이 하는 일입니다. 그것은 아주 먼 곳에서 평행한 광선으로 모든 것을 비춰요.

```undefined
...

const dirLight = new THREE.DirectionalLight(0xffffff, 0.6);
dirLight.position.set(10, 20, 0); // x, y, z
scene.add(dirLight);

...
```

여기서는 조명의 위치를 위에서(Y 값으로) 설정하고 X축을 따라 약간 이동합니다. Y축의 값이 가장 높습니다. 이것은 상자의 윗부분이 가장 많은 빛을 받고 그 상자의 가장 빛나는 면이 될 것이라는 것을 의미합니다.

또한 빛이 X축을 따라 약간 이동하기 때문에 상자의 오른쪽에도 약간의 빛이 들어오지만 적은 빛이 들어옵니다.

그리고 우리는 Z축을 따라 조명 위치를 이동하지 않기 때문에 박스의 앞면은 이 광원에서 어떤 빛도 받지 못합니다. 만약 주변 조명이 없다면, 앞면은 어둠 속에 남아있을 것이다.

다른 종류의 조명도 있다. 예를 들어 PointLight를 사용하여 전구를 시뮬레이션할 수 있습니다. 그것은 고정된 위치를 가지고 있고 모든 방향으로 빛을 방출합니다. 스폿라이트는 자동차의 스포트라이트를 시뮬레이션하는 데 사용될 수 있습니다. 그것은 하나의 지점에서 원뿔을 따라 방향으로 빛을 방출한다.

## 카메라 설정 방법

지금까지, 우리는 기하학과 재료로 망사를 만들었습니다. 그리고 우리는 또한 조명을 설치하고 현장에 추가했습니다. 우리는 여전히 이 장면을 어떻게 보는지 정의하기 위해 카메라가 필요합니다.

여기에는 두 가지 옵션이 있습니다. 투시 카메라와 맞춤식 카메라입니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/Stack.010.jpeg)

비디오 게임은 주로 투시 카메라를 사용합니다. 왜냐하면 그것들이 작동하는 방식이 실제의 상황을 보는 방식과 비슷하기 때문입니다. 멀리 떨어져 있는 것은 더 작아 보이고 바로 앞에 있는 것은 더 커 보입니다.

맞춤식 투영법을 사용하면 카메라에서 얼마나 멀리 떨어져 있든지 간에 사물의 크기가 같습니다. 직교 카메라는 좀 더 미니멀하고 기하학적인 느낌을 준다. 기하학적 구조를 왜곡하지 않습니다. 평행선이 평행하게 나타납니다.

두 카메라 모두 시야를 정의해야 합니다. 이 부분은 3D 공간에서 스크린에 투영될 영역입니다. 이 지역 밖의 모든 항목은 화면에 표시되지 않습니다. 너무 가깝거나 너무 멀거나 카메라가 방향을 가리키지 않기 때문이다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/freecodecamp-2.001.jpeg)

원근 투영을 통해 시야 안의 모든 것이 일직선으로 관점을 향해 투영된다. 카메라에서 멀리 떨어져 있는 사물이 화면에서는 더 작게 나타납니다. 왜냐하면 시야에서 보면 더 작은 각도 아래에서 볼 수 있기 때문입니다.

```undefined
...

// Perspective camera
const aspect = window.innerWidth / window.innerHeight;
const camera = new THREE.PerspectiveCamera(
  45, // field of view in degrees
  aspect, // aspect ratio
  1, // near plane
  100 // far plane
);

...
```

투시 카메라를 정의하려면 뷰의 수직 각도인 시야를 설정해야 합니다. 그런 다음 프레임의 폭과 높이의 가로 세로 비율을 정의합니다. 전체 브라우저 창을 채우고 가로 세로 비율을 유지하려면 이렇게 해야 합니다.

그런 다음 마지막 두 파라미터는 근방 평면과 원거리 평면이 시야에서 얼마나 떨어져 있는지를 정의합니다. 카메라와 너무 가까운 것은 무시되고, 너무 멀리 있는 것도 무시됩니다.

```undefined
...

// Orthographic camera
const width = 10;
const height = width * (window.innerHeight / window.innerWidth);
const camera = new THREE.OrthographicCamera(
  width / -2, // left
  width / 2, // right
  height / 2, // top
  height / -2, // bottom
  1, // near
  100 // far
);

...
```

그리고 맞춤 카메라가 있습니다. 여기서 우리는 사물을 하나의 점으로 투영하는 것이 아니라 표면으로 투영하는 것이다. 각 투영 선은 평행입니다. 그렇기 때문에 카메라에서 물체가 얼마나 멀리 떨어져 있는지는 중요하지 않습니다. 그래서 기하학을 왜곡하지 않습니다.

직교 카메라의 경우 각 평면이 관점에서 얼마나 떨어져 있는지 정의해야 합니다. 따라서 왼쪽 평면은 왼쪽으로 5단위, 오른쪽 평면은 오른쪽으로 5단위 등입니다.

```undefined
...

camera.position.set(4, 4, 4);
camera.lookAt(0, 0, 0);

...
```

우리가 어떤 카메라를 사용하든 간에, 우리는 또한 그것을 배치하고 방향에 맞춰야 합니다. 만약 우리가 직교 카메라를 사용한다면, 여기 실제 숫자는 별로 중요하지 않다. 개체는 카메라에서 얼마나 멀리 떨어져 있더라도 동일한 크기로 나타납니다. 그러나 중요한 것은 그들의 비율이다.

이 튜토리얼 전체를 통해 우리는 모든 예들을 같은 카메라를 통해 보았습니다. 이 카메라는 모든 축을 따라 같은 단위에 의해 이동되었으며 0,0,0 좌표를 향해 보입니다. 직교 카메라를 배치하는 것은 방향등을 배치하는 것과 같다. 중요한 것은 실제 위치가 아니라 방향이다.

## 씬(scene) 렌더링 방법

그래서 우리는 그 장면과 카메라를 조립할 수 있었습니다. 이제 이미지를 브라우저에 렌더링하는 마지막 부분만 누락되었습니다.

WebGL 렌더러를 정의해야 합니다. 이 작품은 장면과 카메라를 제공할 때 실제 이미지를 HTML 캔버스로 만들 수 있는 작품입니다. 또한 이 캔버스의 실제 크기, 즉 브라우저에 표시되는 캔버스의 너비 및 높이(픽셀 단위)를 설정할 수 있습니다.

```undefined
import * as THREE from "three";

// Scene
const scene = new THREE.Scene();

// Add a cube to the scene
const geometry = new THREE.BoxGeometry(3, 1, 3); // width, height, depth
const material = new THREE.MeshLambertMaterial({ color: 0xfb8e00 });
const mesh = new THREE.Mesh(geometry, material);
mesh.position.set(0, 0, 0);
scene.add(mesh);

// Set up lights
const ambientLight = new THREE.AmbientLight(0xffffff, 0.6);
scene.add(ambientLight);

const directionalLight = new THREE.DirectionalLight(0xffffff, 0.6);
directionalLight.position.set(10, 20, 0); // x, y, z
scene.add(directionalLight);

// Camera
const width = 10;
const height = width * (window.innerHeight / window.innerWidth);
const camera = new THREE.OrthographicCamera(
  width / -2, // left
  width / 2, // right
  height / 2, // top
  height / -2, // bottom
  1, // near
  100 // far
);

camera.position.set(4, 4, 4);
camera.lookAt(0, 0, 0);

// Renderer
const renderer = new THREE.WebGLRenderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
renderer.render(scene, camera);

// Add it to HTML
document.body.appendChild(renderer.domElement);
```

마지막으로, 마지막 줄은 이 렌더링된 캔버스를 HTML 문서에 추가합니다. 그리고 그것이 상자를 만드는 데 필요한 전부입니다. 한 상자로는 좀 무리인 것 같지만, 대부분의 이런 것들은 한 번만 설정하면 됩니다.

이 프로젝트를 진행하고 싶다면, 어떻게 하면 이 게임을 간단한 게임으로 만들 수 있는지 제 유튜브 비디오를 보세요. 비디오에서, 우리는 스택 빌딩 게임을 만듭니다. 우리는 게임 논리, 이벤트 핸들러 및 애니메이션, 심지어 캐논.js를 사용하여 일부 물리학을 추가한다.

이 튜토리얼에 대한 피드백이나 질문이 있으시면 언제든지 @HunorBorbely @Tweet me를 트윗하시거나 YouTube에 댓글을 남겨주세요.