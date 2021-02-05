---
layout: post
title: "최소 CSS를 사용하여 응답성이 높은 페이지 및 색 테마를 만드는 방법"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/root.jpeg
tags: undefined
---


컬러 테마로 대응력이 뛰어난 웹 사이트를 구축하시겠습니까? 루트에서 시작하세요.

혹시 제 웹사이트에 들르시면, 제가 그것을 약간 꾸미고 있다는 것을 아실 수 있을 거예요. 빅토리아.dev는 이제 사용자의 장치와 기본 설정에 더 잘 대응할 수 있습니다.

대부분의 최신 장치와 웹 브라우저는 사용자가 사용자 인터페이스의 밝은 테마 또는 어두운 테마를 선택할 수 있도록 한다. CSS 미디어 쿼리를 사용하면 사용자 자신의 웹 사이트 스타일을 이 사용자 설정에 맞게 변경할 수 있습니다!

미디어 쿼리는 웹 페이지의 요소를 다른 화면 크기에 맞게 변경하는 일반적인 방법입니다. 이것은 루트 요소에 설정된 사용자 지정 속성과 결합할 때 특히 강력한 도구입니다.

다음은 CSS 미디어 쿼리 및 사용자 지정 속성을 사용하여 몇 줄의 CSS만으로 방문자의 검색 환경을 개선하는 방법입니다.

## 사람들의 색 선호에 맞추는 방법

기본 설정 색 구성표 미디어 기능을 쿼리하여 사용자의 색 구성표를 지원할 수 있습니다. light 옵션은 활성 환경설정이 설정되어 있지 않은 경우 go to version으로, 최신 브라우저에 걸쳐 적절한 지원을 제공한다.

또한 특정 장치에서 읽는 사용자는 일정에 따라 밝은 색과 어두운 색 테마를 설정할 수 있습니다. 예를 들어, 내 전화기는 낮에는 UI 전체에 밝은 색을 사용하고 밤에는 어두운 색을 사용합니다. 당신은 당신의 웹사이트를 팔로잉 할 수 있다.

`:root` 의사 클래스에서 색 테마에 대한 사용자 지정 속성을 설정하여 CSS를 많이 반복하지 않도록 합니다. 지원하려는 각 테마에 대한 버전을 만듭니다. 다음은 구축 가능한 간단한 예입니다.

```css
:root {
    color-scheme: light dark;
}

@media (prefers-color-scheme: light) {
    :root {
        --text-primary: #24292e;
        --background: white;
        --shadow: rgba(0, 0, 0, 0.15) 0px 2px 5px 0px;
    }
}

@media (prefers-color-scheme: dark) {
    :root {
        --text-primary: white;
        --background: #24292e;
        --shadow: rgba(0, 0, 0, 0.35) 0px 2px 5px 0px;
    }
}

```

보시는 것처럼 사용자 지정 속성을 사용하여 모든 종류의 값을 설정할 수 있습니다. 이를 다른 CSS 요소와 함께 변수로 사용하려면 `var()` 함수를 사용합니다.

```css
header {
    color: var(--text-primary);
    background-color: var(--background);
    box-shadow: var(--shadow);
}

```

이 빠른 예에서는 이제 `헤더` 요소가 브라우저 설정에 따라 사용자가 선호하는 색상을 표시합니다.

기본 색 구성표는 브라우저에 따라 사용자가 여러 가지 방법으로 설정합니다. 여기 몇 가지 예가 있습니다.

### Firefox의 명암 모드

주소 표시줄에 about:config를 입력하면 Firefox에서 light 및 dark 모드를 테스트할 수 있습니다. 경고 메시지가 나타나면 동의한 다음 `ui.systemUsDark`를 입력합니다.테마가 검색됩니다.

설정에 대한 `숫자` 값을 선택한 다음 어둡게는 `1`을, 빛은 `0`을 입력합니다.

![image](https://victoria.dev/blog/responsive-pages-and-color-themes-with-minimal-css/firefox-theme-setting.png)

### 용맹한 빛과 어둠의 모드

브레이브를 사용하는 경우, 설정 > 모양 > 브레이브 색상에서 색 테마 설정을 찾으십시오.

![image](https://victoria.dev/blog/responsive-pages-and-color-themes-with-minimal-css/brave-settings.png)

## 가변 스케일링 사용 방법

사용자 지정 속성을 사용하여 사용자의 화면 크기에 따라 텍스트 또는 다른 요소의 크기를 쉽게 조정할 수도 있습니다. 너비` 미디어 기능은 뷰포트의 너비를 테스트합니다.

width:_px는 정확한 크기와 일치하지만 min과 max를 사용하여 범위를 만들 수도 있습니다.

최소 너비: _px`로 쿼리하여 `_` 픽셀 이상의 모든 것을 일치시키고 최대 너비: _px`를 사용하여 쿼리합니다.

다음 쿼리를 사용하여 `:root`에 사용자 지정 속성을 설정하여 비율을 생성합니다.

```css
@media (min-width: 360px) {
    :root {
        --scale: 0.8;
    }
}

@media (min-width: 768px) {
    :root {
        --scale: 1;
    }
}

@media (min-width: 1024px) {
    :root {
        --scale: 1.2;
    }
}

```

그런 다음 `calc()` 함수를 사용하여 요소가 반응하도록 한다. 다음은 몇 가지 예입니다.

```css
h1 {
    font-size: calc(42px * var(--scale));
}

h2 {
    font-size: calc(26px * var(--scale));
}

img {
    width: calc(200px * var(--scale));
}

```

이 예에서는 초기 값을 `--scale` 사용자 지정 속성으로 곱하면 머리글과 이미지의 크기가 사용자의 장치 너비에 맞게 마법처럼 조정될 수 있습니다.

상대 유닛 렘도 비슷한 효과를 낼 것이다. 루트 요소에 선언된 글꼴 크기에 상대적인 요소의 크기를 정의하는 데 사용할 수 있습니다.

```css
h1 {
    font-size: calc(5rem * var(--scale));
}

h2 {
    font-size: calc(1.5rem * var(--scale));
}

p {
    font-size: calc(1rem * var(--scale));
}

```

물론 두 가지 사용자 지정 속성을 곱할 수도 있습니다. 예를 들어, `:root`에서 `--max-img`를 사용자 지정 속성으로 설정하면 여러 위치에서 픽셀 값을 업데이트할 필요가 없으므로 나중에 시간을 절약할 수 있습니다.

```css
img {
    max-width: calc(var(--max-img) * var(--scale));
}

```

## 대응력 향상 게임

당신의 방문자의 기기와 선호도에 맞는 웹사이트를 위해 이러한 쉬운 승리를 경험해 보세요. 이제 victoria.dev에 잘 쓰도록 했습니다. 네가 어떻게 좋아하는지 알려줬으면 좋겠어!

이 게시물을 즐기셨다면, 이 게시물이 어디에서 왔는지 더 많은 것이 있습니다. 먼저 새로운 기사를 보려면 victoria.dev에 가입하십시오.