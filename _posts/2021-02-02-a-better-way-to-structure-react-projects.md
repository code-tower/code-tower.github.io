---
layout: post
title: "React 프로젝트를 구조화하는 더 나은 방법
 "
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/02/z02wxvp94dwg84c4ifhj.jpeg
tags: undefined
---


안녕하세요 여러분!
 많은 e- 잉크가 상대적으로 쉬운 선택 인“React에서 X 수행하기”또는“기술 X와 함께 React 사용하기”에 이미 쏟아져 나왔습니다.
 

그래서 저는 DelightChat과 이전 회사에서 처음부터 프런트 엔드를 구축 한 경험에 대해 이야기하고 싶습니다.
 

이러한 프로젝트는 React에 대한 더 깊은 이해와 프로덕션 환경에서의 확장 된 사용을 필요로합니다.
 

## 소개
 

요컨대 복잡한 React 프로젝트는 이와 같이 구성되어야합니다.
 프로덕션에서 NextJS를 사용하지만이 파일 구조는 모든 React 설정에서 매우 유용합니다.
 

```undefined
src
|---adapters
|---contexts
|---components
|---styles
|---pages

```

참고 : 위의 파일 구조에서 자산 또는 정적 파일은 프레임 워크의`public *`폴더 변형이 무엇이든 상관없이 배치되어야합니다. *
 

위의 각 폴더에 대해 우선 순위에 따라 설명하겠습니다.
 

## 1. 어댑터
 

`어댑터`는 애플리케이션과 외부 세계를 연결하는 커넥터입니다.
 외부 서비스 또는 클라이언트와 데이터를 공유하기 위해 발생해야하는 모든 형태의 API 호출 또는 웹 소켓 상호 작용은 어댑터 자체 내에서 발생해야합니다.
 

일부 데이터가 모든 어댑터간에 항상 공유되는 경우가 있습니다. 예를 들어 AJAX (XHR) 어댑터에서 쿠키, 기본 URL 및 헤더를 공유하는 경우가 있습니다.
 xhr 폴더에서 초기화 한 다음 다른 어댑터 내부로 가져 와서 더 사용할 수 있습니다.
 

이 구조는 다음과 같습니다.
 

```undefined
adapters
|---xhr
|---page1Adapter
|---page2Adapter

```

axios의 경우`axios.create`를 사용하여 기본 어댑터를 만들고이 초기화 된 인스턴스를 내보내거나 get, post, patch 및 delete에 대해 다른 함수를 만들어 추가로 추상화 할 수 있습니다.
 이것은 다음과 같습니다.
 

```undefined
// adapters/xhr/index.tsx

import Axios from "axios";

function returnAxiosInstance() {
  return Axios.create(initializers);
}

export function get(url){
  const axios = returnAxiosInstance();
  return axios.get(url);
}

export function post(url, requestData){
  const axios = returnAxiosInstance();
  return axios.post(url, requestData);
}

... and so on ...

```

기본 파일 (또는 파일)을 준비한 후 앱의 복잡성에 따라 각 페이지 또는 각 기능 집합에 대해 별도의 어댑터 파일을 만듭니다.
 이름이 잘 지정된 함수를 사용하면 각 API 호출이 수행하는 작업과 수행해야하는 작업을 매우 쉽게 이해할 수 있습니다.
 

```undefined
// adapters/page1Adapter/index.tsx

import { get, post } from "adapters/xhr";
import socket from "socketio";

// well-named functions
export function getData(){
  return get(someUrl);
}

export function setData(requestData){
  return post(someUrl, requestData);
}

... and so on ...

```

그러나 이러한 어댑터는 어떻게 사용됩니까?
 다음 섹션에서 알아 보겠습니다.
 

## 2. 구성 요소
 

이 섹션에서는 컨텍스트에 대해 이야기해야하지만 먼저 구성 요소에 대해 이야기하고 싶습니다.
 이것은 복잡한 응용 프로그램에서 컨텍스트가 필요한 이유를 이해하기위한 것입니다.
 

`구성 요소`는 애플리케이션의 생명선입니다.
 그들은 당신의 애플리케이션에 대한 UI를 보유 할 것이며, 때때로 비즈니스 로직과 유지해야하는 모든 상태를 보유 할 수 있습니다.
 

구성 요소가 UI로 비즈니스 로직을 표현하기에는 너무 복잡해지면 루트 index.tsx가 모든 함수와 핸들러를 가져 오는 별도의 bl.tsx 파일로 분할 할 수있는 것이 좋습니다.
 

이 구조는 다음과 같습니다.
 

```undefined
components
|---page1Components
        |--Component1
        |--Component2
|---page2Component
        |--Component1
               |---index.tsx
               |---bl.tsx

```

이 구조에서 각 페이지는 구성 요소 내부에 자체 폴더를 가지므로 어떤 구성 요소가 무엇에 영향을 미치는지 쉽게 파악할 수 있습니다.
 

구성 요소의 범위를 제한하는 것도 중요합니다.
 따라서 구성 요소는 데이터 가져 오기에 `어댑터`만 사용하고 복잡한 비즈니스 로직을위한 별도의 파일을 가지고 UI 부분에만 집중해야합니다.
 

```undefined
// components/page1Components/Component1/index.tsx

import businessLogic from "./bl.tsx";

export default function Component2() {
  
  const { state and functions } = businessLogic();

  return {
    // JSX
  }
}

```

BL 파일은 데이터를 가져 와서 반환합니다.
 

```undefined
// components/page1Components/Component1/bl.tsx

import React, {useState, useEffect} from "react";
import { adapters } from "adapters/path_to_adapter";

export default function Component1Bl(){
  const [state, setState] = useState(initialState);

  useEffect(() => {
    fetchDataFromAdapter().then(updateState);
  }, [])
}


```

그러나 모든 복잡한 앱에서 공통적 인 문제가 있습니다.
 상태 관리 및 원격 구성 요소간에 상태를 공유하는 방법.
 예를 들어, 다음 파일 구조를 고려하십시오.
 

```undefined
components
|---page1Components
        |--Component1
               |---ComponentA
|---page2Component
        |--ComponentB

```

위의 예에서 일부 상태를 ComponentA와 B에서 공유해야하는 경우 모든 중간 구성 요소와 상태와 상호 작용하려는 다른 구성 요소를 통해 전달되어야합니다.
 

이를 해결하기 위해 Redux, Easy-Peasy 및 React Context와 같이 사용할 수있는 몇 가지 솔루션이 있으며 각각 고유 한 장단점이 있습니다.
 일반적으로 React Context는이 문제를 해결하기에 "충분히"충분해야합니다.
 컨텍스트와 관련된 모든 파일을 `컨텍스트`에 저장합니다.
 

## 3. 컨텍스트
 

`contexts`폴더는 이러한 구성 요소간에 공유해야하는 상태 만 포함하는 최소 폴더입니다.
 각 페이지에는 여러 개의 중첩 된 컨텍스트가있을 수 있으며 각 컨텍스트는 아래쪽 방향으로 만 데이터를 전달합니다.
 그러나 복잡성을 방지하려면 컨텍스트 파일이 하나만있는 것이 가장 좋습니다.
 이 구조는 다음과 같습니다.
 

```undefined
contexts
|---page1Context
        |---index.tsx (Exports consumers, providers, ...)
        |---Context1.tsx (Contains part of the state)
        |---Context2.tsx (Contains part of the state)
|---page2Context
        |---index.tsx (Simple enough to also have state)

```

위의 경우 `page1`이 좀 더 복잡 할 수 있으므로 자식 컨텍스트를 부모에게 자식으로 전달하여 일부 중첩 컨텍스트를 허용합니다.
 그러나 일반적으로 상태를 포함하고 관련 파일을 내보내는 단일`index.tsx` 파일이면 충분합니다.
 

React 상태 관리 라이브러리의 구현 부분은 각각 자체의 짐승이고 고유 한 장점과 단점이 있으므로 다루지 않겠습니다.
 따라서 최선의 방법을 배우기 위해 사용하기로 결정한 모든 것에 대한 튜토리얼을 진행하는 것이 좋습니다.
 

컨텍스트는 `어댑터`에서 가져 와서 외부 효과를 가져오고 반응 할 수 있습니다.
 React Context의 경우 공급자는 페이지 내에서 가져 와서 모든 구성 요소에서 상태를 공유하며,이 데이터를 활용할 수 있도록`useContext`와 같은 것이 이러한`components` 내부에 사용됩니다.
 

마지막 주요 퍼즐 조각 인 `페이지`로 이동합니다.
 

## 4. 페이지
 

이 부분의 프레임 워크에 편향되는 것을 피하고 싶지만 일반적으로 경로 수준 구성 요소를 배치 할 특정 폴더가있는 것이 좋습니다.
 

Gatsby & NextJS는 `pages`라는 폴더에 모든 경로를 적용합니다.
 이것은 경로 수준 구성 요소를 정의하는 읽기 쉬운 방법이며 CRA 생성 응용 프로그램에서이를 모방하면 코드 가독성이 향상됩니다.
 

경로의 중앙 위치는 (Cmd 또는 Ctrl) + 가져 오기를 클릭하여 파일로 이동하여 대부분의 IDE의 "파일로 이동"기능을 활용하는 데 도움이됩니다.
 

이를 통해 코드를 신속하고 명확하게 이동할 수 있습니다.
 또한 `페이지`와 `컴포넌트`사이의 명확한 구분 계층을 설정합니다. 여기서 페이지는 컴포넌트를 가져와 표시 할 수 있으며 비즈니스 로직은 물론 다른 작업도 수행 할 수 없습니다.
 

하지만 페이지 내에서 컨텍스트 제공자를 가져와 하위 구성 요소가 사용할 수 있습니다.
 또는 NextJS의 경우 getServerSideProps 또는 getStaticProps를 사용하여 구성 요소에 데이터를 전달할 수있는 서버 측 코드를 작성하십시오.
 

## 5. 스타일
 

마지막으로 스타일에 대해 설명합니다.
 내가 가야 할 방법은 Styled-Components와 같은 CSS-in-JS 솔루션을 사용하여 UI 내부에 스타일을 삽입하는 것이지만 CSS 파일에 전역 스타일 세트를 포함하는 것이 때때로 도움이됩니다.
 

평범한 오래된 CSS 파일은 프로젝트간에 더 많이 공유 할 수 있으며 스타일이 지정된 구성 요소가 도달 할 수없는 구성 요소 (예 : 타사 구성 요소)의 CSS에도 영향을 미칠 수 있습니다.
 

따라서 이러한 모든 CSS 파일을`styles` 폴더에 저장하고 원하는 곳에서 자유롭게 가져 오거나 연결할 수 있습니다.
 

제 생각이었습니다.
 이 문제를 개선 할 수있는 방법에 대해 논의하거나 더 많은 의견이 있으시면 언제든지 이메일을 보내주세요!
 

추가 업데이트 나 토론이 필요하면 여기 Twitter에서 저를 팔로우 할 수 있습니다.
 

freeCodeCamp에 대한 저의 마지막 기사는 여기에서 읽을 수있는 URL 단축기를 구축하여 Deno를 시작하는 방법에 대해 작성되었습니다.
 