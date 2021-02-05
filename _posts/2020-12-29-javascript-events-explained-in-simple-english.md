---
layout: post
title: "간단한 영어로 설명하는 브라우저 이벤트"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/events.jpg
tags: undefined
---


## 브라우저 이벤트란?

이벤트는 프로그래밍하는 시스템에서 발생하는 동작 또는 발생을 말합니다. 그런 다음 필요에 따라 이벤트에 응답할 수 있도록 사용자에게 이벤트에 대해 알립니다.

이 글에서, 나는 웹 브라우저의 맥락에 있는 이벤트에 초점을 맞출 것이다. 기본적으로 이벤트는 적절한 응답을 할 수 있도록 특정 작업이 수행되었음을 나타내는 지표입니다.

내가 말하는 것을 설명하자면, 당신이 안전하게 도로를 건널 수 있도록 신호등이 바뀌기를 기다리는 횡단보도에 서 있다고 상상해 보자. 이 이벤트는 신호등의 변화로 인해 이후에 조치를 취하게 됩니다. 즉, 이 경우 도로를 건너게 됩니다.

웹 개발에서도 마찬가지로 관심이 있는 이벤트가 발생할 때마다 조치를 취할 수 있습니다.

웹 개발에서 흔히 볼 수 있는 몇 가지 이벤트는 다음과 같습니다.

- 마우스 이벤트

- 찰칵찰칵
- 딸깍딸깍
- 무브먼트
- `오버`
- `유동차`
- `외출`하다
- `패턴
- 쥐죽은
- `업업`

2. 터치 이벤트

- 터치 스타트
- 터치 무브
- 칙칙한 소리
- 터치 취소

3. 키보드 이벤트

- 키다운
- 키프레스
- 키업

4. 이벤트 형성

- 초점
- ➡➡➡➡➡➡➡➡➡➡ ➡
- 변화하다`
- ➡➡➡➡➡➡➡➡➡➡ ➡

5. 윈도우 이벤트

- ➡➡➡➡➡➡➡➡➡➡ ➡
- ➡➡➡➡➡➡➡➡➡➡ ➡
- `변동
- 짐을 싣다
- ➡➡➡➡➡➡➡➡➡➡ ➡

이벤트의 전체 목록과 이벤트가 속하는 다른 카테고리의 경우 MDN 설명서를 참조할 수 있습니다. 나열된 이벤트 중 일부는 공식 사양의 표준 이벤트이고, 다른 이벤트 중 일부는 특정 브라우저에서 내부적으로 사용되는 이벤트입니다.

## 이벤트 핸들러란?

위에서 언급한 바와 같이, 우리는 이벤트가 발생했다는 통보를 받을 때마다 프로그램이 적절한 조치를 취할 수 있도록 이벤트를 모니터링합니다.

이 작업은 이벤트 수신기라고도 하는 이벤트 핸들러라는 함수에서 종종 수행됩니다. 이벤트가 발생하여 이벤트 핸들러가 호출되면 이벤트가 등록되었다고 말합니다. 이는 아래 코드에 설명되어 있습니다.

`id` `btn`인 버튼을 클릭하면 이벤트 핸들러가 호출되고 "Button has clicked"(버튼 클릭됨) 텍스트가 표시된 경고가 표시됩니다. 클릭 시 속성이 이벤트 핸들러인 함수에 할당되었습니다. 이 방법은 DOM 요소에 이벤트 핸들러를 추가하는 세 가지 방법 중 하나입니다.

```undefined
const button = document.getElementById("btn");
button.onclick = function(){
   alert("Button has been clicked");
}

```

이벤트 핸들러는 대부분 함수로 선언되지만 객체가 될 수도 있다는 점을 지적할 만하다.

## 이벤트 핸들러를 할당하는 방법

HTML 요소에 이벤트 핸들러를 연결하는 방법은 여러 가지가 있습니다. 아래에서는 이러한 방법과 장단점에 대해 논의하겠습니다.

### HTML 특성을 가진 이벤트 핸들러 할당

HTML 요소에 이벤트 핸들러를 연결하는 가장 쉬운 방법이지만 권장되지는 않습니다. 여기에는 `on<event>라는 이름의 인라인 HTML 이벤트 속성(이벤트 핸들러 값)이 사용됩니다. 예를 들어 on click, on change, on submit 등이 있다.

HTML 속성은 대소문자를 구분하지 않기 때문에 클릭 시, 변경 시 또는 제출 시라는 HTML 이벤트 속성을 자주 찾을 수 있습니다. 기본적으로 온클릭 온클릭 온클릭 온클릭 온클릭 온클릭 온클릭을 사용하는 것이 구문적으로 옳다. 하지만 소문자로 남겨두는 것이 일반적입니다.

```html
<button onclick = "alert('Hello world!')"> Click Me </button>
<button onclick = "(() => alert('Hello World!'))()"> Click Me Too </button>
<button onclick = "(function(){alert('Hello World!')})()"> And Me </button>

```

위의 예에서 JavaScript 코드는 문자 그대로 HTML 이벤트 속성에 할당되었습니다.

마지막 두 개의 `버튼` 요소에서 즉시 호출되는 함수 식(IIFE) 형식을 기록해 두십시오. 이것이 쉽고 간단해 보이지만, 인라인 HTML 이벤트 속성을 할당하는 것은 비효율적이고 유지 관리가 어렵습니다.

마크업에서 해당 버튼이 20개 이상 있다고 가정합니다. 각 버튼마다 동일한 자바스크립트 코드를 작성하면 반복됩니다. 여러 HTML 파일에 동일한 코드를 쉽게 사용할 수 있도록 JavaScript를 자체 파일에 쓰는 것이 항상 좋습니다.

또한 여러 줄의 JavaScript 코드를 인라인으로 설정할 수 없습니다. 인라인 자바스크립트 코드는 앞에서 언급한 이유로 인해 안티패턴으로 간주된다. 그러니 여러분이 빠른 것을 시도하지 않는 한 피하도록 노력하세요.

### 'script' 태그에서 이벤트 핸들러 선언

위의 작업을 수행하는 대신 이벤트 핸들러를 `script` 태그로 선언하고 아래와 같이 인라인으로 호출할 수도 있습니다.

```html
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="stylesheet" href="./index.css" type="text/css" />
    <script>
      function onClickHandler(){
         alert("Hello world!");
       }
    </script> 
  </head>
  <body>
    <div class="wrapper">
       <button onclick = "onClickHandler()"> Click me </button>
    </div>
  </body>
</html>

```

그러나 함수 이름을 `onClick = onClickHandler`와 같은 HTML 이벤트 특성의 값으로 할당하면 작동하지 않습니다. HTML 속성의 값과 마찬가지로 호출을 따옴표로 묶어서 위와 같이 호출해야 합니다.

### DOM 속성을 사용하여 이벤트 핸들러 할당

위에서 설명한 인라인 HTML 이벤트 속성을 사용하는 대신 DOM 요소의 이벤트 속성 값으로 이벤트 핸들러를 할당할 수도 있습니다. 이것은 `script` 태그 내부 또는 JavaScript 파일에서만 가능합니다.

이 접근 방식의 한 가지 제한 사항은 동일한 이벤트에 대해 여러 이벤트 핸들러를 가질 수 없다는 것입니다. 아래 그림과 같이 동일한 이벤트에 대해 여러 처리기가 있는 경우 마지막 처리기만 적용됩니다. 나머지 항목은 덮어쓰게 됩니다.

```undefined
const button = document.getElementById("btn");
button.onclick = function(){
   alert("Button has been clicked");
}
// Only this is applied
button.onclick = function(){
   console.log("Button has been clicked");
}

```

이벤트 수신기를 `onclick` 이벤트에서 제거하려면 `button.onclick`을 `null`로 다시 할당하면 됩니다.

```undefined
button.onclick = null

```

### 이벤트 수신기를 추가하는 DOM 방법을 향상시키는 방법

위의 이벤트 수신기를 추가하는 방법은 인라인 JavaScript를 사용하는 것보다 더 좋습니다. 그러나 한 요소가 각 이벤트에 대해 하나의 이벤트 핸들러만 가지도록 제한하는 제한 사항이 있습니다.

예를 들어 요소의 클릭 이벤트에 대해 여러 이벤트 핸들러를 적용할 수 없습니다.

이러한 한계를 해소하기 위해 이벤트 청취자 추가와 이벤트 청취자 제거가 도입되었다. 이렇게 하면 동일한 요소의 동일한 이벤트에 대해 여러 이벤트 핸들러를 추가할 수 있습니다.

```undefined
const button = document.getElementById('btn');
button.addEventListener('click', () => {
  alert('Hello World');
})
button.addEventListener('click', () => {
  console.log('Hello World');
})

```

위의 코드에서 id `btn`인 요소를 선택한 다음 두 개의 이벤트 핸들러를 연결하여 클릭 이벤트를 모니터링한다. 첫 번째 이벤트 핸들러가 호출되고 헬로월드라는 알림 메시지가 뜬다. 이후 헬로월드도 콘솔에 기록된다.

위의 예에서 알 수 있듯이 `element.addEventListener`의 함수 서명은 다음과 같습니다.

```undefined
element.addEventListener(event, eventHandler, [optional parameter])

```

- 이벤트성

첫 번째 매개 변수인 `event`(필수 매개 변수)는 이벤트의 이름을 지정하는 문자열입니다. 예를 들어 "click" ips" mouse over "mouse out" 등이 있습니다.

2. 이벤트 핸들러

첫 번째 매개 변수도 필요하지만 두 번째 매개 변수는 이벤트가 발생할 때 호출되는 함수입니다. 이벤트 개체가 첫 번째 매개 변수로 전달됩니다. 이벤트 개체는 이벤트 유형에 따라 다릅니다. 예를 들어 클릭 이벤트에 대해 `MouseEvent` 개체가 전달됩니다.

3. 선택적 파라미터

세 번째 매개 변수인 선택적 매개 변수는 다음과 같은 속성을 가진 개체입니다.

- `원스`: 이 값은 부울입니다. true이면 수신기가 트리거된 후 제거됩니다.
- ➡: 그것의 값 또한 부울이다. 버블링 또는 캡처 단계에서 이벤트를 처리해야 하는 단계를 설정합니다. 기본값은 `false`이므로 버블 단계에서 이벤트가 캡처됩니다. 여기서 자세히 보실 수 있습니다. 역사적 이유로 옵션이 참 또는 거짓일 수도 있습니다.
- `수동`: 그것의 값 또한 부울이다. true이면 처리기에서 preventDefault()를 호출하지 않습니다. preventDefault()는 이벤트 객체의 메서드입니다.

마찬가지로 `클릭` 이벤트 모니터링을 중지하려면 `element.removeEventListener`를 사용할 수 있습니다. 그러나 이 기능은 이벤트 수신기가 `element.addEventListener`를 사용하여 등록된 경우에만 작동합니다. 함수 서명은 element.addEventListener와 유사합니다.

```undefined
element.removeEventListener(event, eventHandler, [options])

```

element.removeEventListener를 사용하여 event를 제거하려면 element.addEventListener에 두 번째 인수로 전달된 함수는 eventlistener를 추가할 때 명명된 함수여야 합니다. 이렇게 하면 제거하려는 경우 동일한 기능을 `element.removeEventListener`에 전달할 수 있습니다.

또한 여기서 선택적 인수를 이벤트 핸들러에 전달한 경우 동일한 선택적 인수를 `removeEventListener`에도 전달해야 한다는 점을 언급할 필요가 있습니다.

```undefined
const button = document.getElementById('btn');
button.removeEventListener('click', clickHandler)


```

## 이벤트 개체란 무엇입니까?

이벤트 핸들러에는 이벤트에 대한 추가 정보를 저장하는 이벤트 개체라는 매개 변수가 있습니다.

이벤트 개체에 저장된 정보는 이벤트 유형에 따라 다릅니다. 예를 들어, 클릭 이벤트 핸들러에 전달된 이벤트 개체에는 클릭 이벤트가 발생한 요소를 참조하는 대상이라는 속성이 있습니다.

아래 예에서 요소를 `id` `btn`으로 클릭하면 `event.target`이 이를 참조합니다. 모든 클릭 이벤트 핸들러에는 `target` 속성이 있는 이벤트 개체가 전달됩니다. 이미 지적한 바와 같이, 여러 이벤트에는 서로 다른 정보를 저장하는 이벤트 개체 매개 변수가 있습니다.

```undefined
const button = document.getElementById("btn");
button.addEventListener("click", event => {
  console.log(event.target);
})

```

## this의 값

이벤트 핸들러에서 이 값은 이벤트 핸들러가 등록되는 요소입니다. 이벤트 핸들러가 등록된 요소는 이벤트가 발생한 요소와 동일하지 않을 수 있습니다.

예를 들어 아래 코드에서 이벤트 핸들러는 래퍼에 등록됩니다. 일반적으로 this 값은 event.currentTarget과 동일합니다. 버튼을 클릭하면 onClickHandler 안에 있는 this 값이 div가 아닌 div가 된다. 왜냐하면 클릭이 버튼에서 시작되었는데도 이벤트 핸들러가 등록된 div이기 때문이다.

이것을 `사건 전파`라고 한다. 관심이 있다면 여기서 읽을 수 있는 매우 중요한 개념이다.

```html
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="stylesheet" href="./index.css" type="text/css" />
    <script>
      function onClickHandler(){
         console.log(this)
         alert("Hello world!");
       }
       const wrapper = document.querySelector(".wrapper");
       wrapper.addEventListener("click", onClickHandler);
    </script> 
  </head>
  <body>
    <div class="wrapper">
       <button> Click me </button>
    </div>
  </body>
</html>

```

## 결론

이 기사에서는 다음을 살펴보았습니다.

- 브라우저 이벤트 및 이벤트 내용
- DOM 요소에 이벤트 핸들러를 추가하는 다양한 방법
- 이벤트 핸들러에 대한 이벤트 개체 매개 변수
- 이벤트 핸들러에서 "this" 값