---
layout: post
title: "RESTFully로 가는 것의 이점 – REST란 무엇이며 왜 REST에 대해 배워야 하는가"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/1_sPLooWMag11pjZnzYXIQCA.png
tags: undefined
---


이 기사에서는 REST(Respational State Transfer) 원칙을 살펴보고 이러한 원칙을 적용하여 얻을 수 있는 이점은 무엇인지 살펴봅니다.

REST를 포함하여 학습하는 이유를 이해하는 것이 중요하다고 생각합니다. 이제 REST 원칙이 어떤 결과를 가져올지 살펴보겠습니다.

## REST란?

REST(Representational State Transfer)는 단순성과 확장성으로 인해 최근 몇 년간 많은 인기를 얻고 있는 아키텍처 스타일이다.

REST가 인기를 얻기 전 SOAP는 실제로 리소스에 액세스하고 웹을 통해 통신하는 방식이었다.

## 왜 REST를 신경써야 하죠?

이 섹션에서는 REST 원칙이 중요한 이유와 REST 원칙에 대해 자세히 알아볼 가치가 있는 이유에 대해 설명하겠습니다. 또한 백엔드 프로젝트에 이를 적용하는 방법도 배울 수 있습니다.

### 1) REST는 이해 및 구현이 용이함

REST는 HTTP에서 작업하는 것을 의미합니다(실제로 HTTP는 REST의 영향을 받았습니다). 따라서 GET, POST, PUT 등 우리 대부분이 알고 있는 HTTP 동사를 사용합니다.

여러분이 이 동사들에 대한 내용을 알지 못한다고 해도, 그 동사들의 이름은 꽤 자명하다. 또한 클라이언트와 서버 코드가 명확하게 구분되어 서로 다른 팀이 애플리케이션의 서로 다른 부분(프론트 엔드 또는 백엔드)에서 쉽게 작업할 수 있습니다.

이해하기 쉽고 구현하기도 쉬우므로 REST 원칙은 개발 팀의 생산성을 높이는 데 도움이 될 수 있습니다. 또한 사람들이 애플리케이션을 개발할 수 있도록 공용 API를 릴리스할 경우에도 중요합니다.

많은 사람들이 REST와 HTTP에 대해 알고 있기 때문에 그들이 당신의 API를 이해하고 사용하는 것이 훨씬 쉬울 것입니다.

![image](https://ucarecdn.com/f9a4640d-ba7f-4f85-82eb-901a56362a9a/)

### 2) REST를 통해 애플리케이션 확장성 향상

REST가 애플리케이션의 확장성을 높이는 데 도움이 되는 두 가지 주요 이유는 다음과 같습니다.

다음 섹션(REST의 원리)에서 볼 수 있듯이, REST의 핵심 원칙 중 하나는 서버 측에서 상태 비저장이라는 것입니다. 따라서 각 요청은 이전 요청과 독립적으로 처리됩니다.

서버 측 상태 또는 세션이 있는 응용 프로그램에서 세션은 로그인한 모든 사용자에 대해 저장됩니다. 이 세션 데이터는 쉽게 비대해지고 서버의 많은 리소스를 차지하기 시작할 수 있습니다.

반면 상태 비저장 서버는 요청을 처리할 때만 리소스(메모리)를 사용하고 요청이 처리되는 즉시 이를 해제합니다.

현재 확장성의 추세는 수평 확장(일반적으로 클라우드에서)이기 때문에 서버측 세션을 저장하면 몇 가지 어려운 문제가 발생하기 때문에 애플리케이션을 확장하기가 어려울 수도 있습니다.

예를 들어 로드 밸런서 뒤에서 작동하는 서버가 많다고 가정해 보겠습니다. 클라이언트가 첫 번째 요청에서 server1에 도달한 경우(서버1에 현재 클라이언트의 세션이 있음) 그리고 나중에 server1에 부하가 걸려 클라이언트가 server1에 저장된 이전 세션 데이터에 대해 알지 못하는 server2에 도달한 경우 어떻게 됩니까? 물론 이 문제에는 해결 방법이 있지만 확장성을 더욱 어렵게 만듭니다.

RESTful API는 일반적으로 JSON을 데이터 교환 형식으로 사용합니다. JSON은 XML에 비해 훨씬 더 작고 컴팩트합니다. XML보다 더 빨리 구문 분석할 수도 있습니다. (소스)

대부분 JSON과 함께 작동하지만, REST API는 여전히 Accept 헤더를 사용하여 다양한 포맷으로 응답할 수 있다는 점도 명심하십시오.

### 3) REST로 캐슁 용이

캐슁은 최신 웹 애플리케이션의 확장성 및 성능에 중요한 요소입니다. 최상의 적중률을 가진 캐시 메커니즘을 잘 설정하면 서버의 평균 응답 시간을 크게 줄일 수 있습니다.

REST는 캐슁을 더 쉽게 만드는 것을 목표로 합니다. 서버가 상태 비저장 상태이고 각 요청을 개별적으로 처리할 수 있으므로 GET 요청은 일반적으로 이전 응답 및 세션에 관계없이 동일한 응답을 반환해야 합니다.

이렇게 하면 GET 요청을 쉽게 캐시할 수 있으며 브라우저에서는 일반적으로 이러한 요청을 처리합니다. 또한 캐시 제어 및 만료 헤더를 사용하여 POST 요청을 캐시 가능으로 설정할 수 있습니다.

### 4) REST는 유연함

즉, 유연성은 수정이 쉽고 XML, JSON 등 다양한 데이터 유형을 요청할 수 있는 많은 클라이언트에 응답할 수 있습니다.

클라이언트는 Accept 헤더(앞서 언급했듯이)를 사용하여 유형을 지정할 수 있으며 REST API는 이에 따라 다른 응답을 반환할 수 있습니다.

언급할 가치가 있는 또 다른 메커니즘은 HATEOAS이다. 용어를 모르는 경우 걱정하지 마십시오. 기본적으로 특정 리소스에 대한 서버 응답의 관련 URL을 반환합니다.

위키백과의 이 예제를 보세요. 클라이언트가 은행 API에서 `account_number`로 계정 정보를 요청하면 다음과 같은 응답을 받습니다.

```undefined

{
    "account": {
        "account_number": 12345,
        "balance": {
            "currency": "usd",
            "value": 100.00
        },
        "links": {
            "deposit": "/accounts/12345/deposit",
            "withdraw": "/accounts/12345/withdraw",
            "transfer": "/accounts/12345/transfer",
            "close": "/accounts/12345/close"
        }
    }
}
```

이 서버는 HATEOAS를 사용하고 해당 작업에 대한 링크를 반환합니다. 이를 통해 API를 쉽게 탐색할 수 있으며, 서버가 엔드포인트를 변경할 수 있도록 하여 API의 유연성을 높일 수 있습니다.

이렇게 생각해 보십시오. 서버가 HEATOAS를 적용하지 않는 경우, 클라이언트는 "/accounts/:account-id/예금"과 같은 엔드포인트를 하드 코딩해야 합니다. 그러나 서버가 URL을 "/accounts/:account-id/ depositMoney"로 변경하면 클라이언트 코드도 변경해야 합니다.

HATEOAS 링크의 도움으로 클라이언트는 이 JSON을 구문 분석하여 링크를 확인하고 쉽게 요청을 할 수 있습니다. 엔드포인트가 변경되면 클라이언트 코드를 변경할 필요 없이 새 엔드포인트와 함께 제공됩니다.

이 주제에 대한 더 많은 정보를 원하시면 로이 필딩의 블로그 게시물을 직접 보실 수 있습니다.

## 결론

이 글에서 나는 왜 내가 REST를 중시하는지, 그리고 왜 당신 또한 그것을 가치있게 여겨야 한다고 믿는지 표현하려고 노력했습니다. 이 글을 읽고 REST 기준을 적용해야 할 이유가 이제 좀 더 명확해졌으면 좋겠습니다.

이 글은 주제에 대해 더 많이 알게 된 동기가 될 수 있다. 좋은 소식이 있습니다. 조만간 REST Best Practice와 일반적인 실수에 대해 쓸 예정입니다.

관심이 있으시다면 제 블로그를 주시거나 구독하시면 됩니다. 이전에 게시한 게시물도 볼 수 있습니다:

질문이 있거나 주제에 대해 더 자세히 논의하고 싶으시면 언제든지 저에게 연락하시면 됩니다.

새해 복 많이 받으시고 읽어주셔서 감사합니다. :)