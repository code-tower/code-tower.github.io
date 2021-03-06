---
layout: post
title: "간단한 4단계 방법으로 코딩 문제를 해결하는 방법"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/iStock-527234840.jpg
tags: undefined
---


15분이나 남았는데, 실패할 줄 알았어요.

나는 첫 번째 기술 면접을 위해 두 달을 공부했습니다.

준비가 된 줄 알았는데, 인터뷰가 끝나자, 코딩을 어떻게 풀어야 할지 전혀 몰랐습니다.

코드를 배울 때 들었던 모든 튜토리얼 중에서 코딩 문제를 해결하기 위한 접근법이 포함된 튜토리얼은 하나도 없었습니다.

나는 문제 해결 방법을 찾아야 했어. 개발자로서의 내 경력은 그것에 달려 있었어.

나는 즉시 방법을 연구하기 시작했다. 그리고 하나 찾았어요. 사실, 제가 발견한 것은 매우 가치 있는 전략이었습니다. 개발자 생태계에서 어떻게든 레이더에 잡혔던 4단계 방식이었다.

이 기사에서는 코딩 문제를 자신 있게 풀기 시작하는 데 사용할 수 있는 이 4단계 문제해결 방법에 대해 알아보겠습니다.

코딩 문제를 해결하는 것은 개발자 직무 인터뷰 프로세스의 일부일 뿐만 아니라 개발자가 하루 종일 수행하는 작업입니다. 결국, 코드를 쓰는 것은 문제를 해결하는 것이다.

## 문제해결방법

이 방법은 George Polya의 "해결 방법"이라는 책에서 나온 것이다. 이 책은 원래 1945년에 나왔고 백만 부 이상이 팔렸다.

그의 문제 해결 방법은 컴퓨터 과학 교수들(Udacity`s Introto CS course by 교수 데이비드 에반스(David Evans)에서 콜트 스틸(Colt Steelle)과 같은 현대의 웹 개발 교사들에 이르기까지 많은 프로그래머들이 사용하고 가르쳐왔다.

4단계 문제해결법을 이용해 간단한 코딩 문제를 푸는 과정을 거치자. 이것은 우리가 그것을 배우면서 그 방법을 실제로 볼 수 있게 해준다. 우리는 자바스크립트를 우리가 선택한 언어로 사용할 것이다. 문제는 다음과 같습니다.

두 숫자를 합쳐서 값을 반환하는 함수를 만듭니다.

문제 해결 방법에는 네 가지 단계가 있습니다.

- 문제를 이해하세요.
- 계획을 세우다.
- 계획을 실행한다.
- 뒤돌아보다.

첫 번째 단계부터 시작하겠습니다.

## 1단계: 문제를 이해합니다.

면접에서 코딩 문제가 발생하면 서둘러 코딩하는 것이 유혹적이다. 이것은 특히 시간 제한이 있는 경우 피하기 어렵다.

하지만, 이 충동을 억누르도록 노력하세요. 문제 해결을 시작하기 전에 문제를 실제로 이해했는지 확인하십시오.

문제를 자세히 읽어 보십시오. 인터뷰에 응한다면, 속도를 늦추는 데 도움이 된다면 문제를 큰 소리로 읽을 수 있을 거예요.

문제를 자세히 읽으면서 이해되지 않는 부분을 명확히 하십시오. 면접 대상인 경우 면접관에게 문제 설명에 대한 질문을 하면 됩니다. 독자 분이 혼자라면, 이해 못할 수도 있는 질문의 일부분을 충분히 생각해 보세요.

우리는 종종 문제를 완전히 이해하는데 시간을 들이지 않기 때문에 이 첫 단계는 필수적이다. 문제를 완전히 이해하지 못할 때, 여러분은 문제를 해결하는 데 훨씬 더 어려움을 겪을 것입니다.

문제를 더 잘 이해하려면 자신에게 다음과 같은 질문을 하십시오.

### 입력 사항은 무엇입니까?

이 문제에 어떤 종류의 입력이 들어갈까요? 이 예에서, 입력은 우리의 함수가 취할 인수이다.

지금까지의 문제 설명을 읽어보면 입력 내용이 숫자가 된다는 것을 알 수 있습니다. 그러나 입력이 어떻게 될 것인가에 대해 좀 더 구체적으로 말하자면 다음과 같은 질문을 할 수 있습니다.

입력은 항상 두 개의 숫자만 됩니까? 만약 우리의 기능이 3개의 입력 번호로 수신된다면 어떻게 될까요?

여기서 우리는 면접관에게 설명을 요구하거나 문제 설명을 더 살펴볼 수 있습니다.

코딩 문제에는 "함수에 두 개의 입력만 예상해야 합니다."라는 메모가 있을 수 있습니다. 만약 그렇다면, 당신은 어떻게 진행해야 하는지 알고 있습니다. 수신되는 입력 유형에 대해 더 많은 질문을 해야 할 수 있기 때문에 보다 구체적으로 파악할 수 있습니다.

입력은 항상 숫자입니까? 입력 "a"와 "b"를 수신할 경우 우리의 기능은 어떻게 해야 합니까? 우리의 기능이 항상 숫자를 받아들일 것인지 아닌지를 명확히 하라.

또는 코드 주석에 가능한 입력 정보를 적어 다음과 같은 정보를 얻을 수 있습니다.

//자주: 2, 4

다음, 질문:

### 생산량은 어떻게 됩니까?

이 기능은 무엇을 반환합니까? 이 경우 출력은 두 숫자 입력의 결과인 하나의 숫자가 됩니다. 어떤 결과가 나올지 확실히 이해하십시오.

### 몇 가지 예를 만듭니다.

문제를 파악하고 가능한 입력과 출력을 파악한 후에는 몇 가지 구체적인 예제에 대한 작업을 시작할 수 있습니다.

예를 들어 최종 문제를 테스트하기 위한 위생 검사로도 사용할 수 있습니다. 면접 중이든, Codewars 또는 HackerRank와 같은 사이트를 사용 중이든 상관없이 대부분의 코드 챌린지 편집기에는 이미 예제 또는 테스트 사례가 작성되어 있습니다. 그렇다 하더라도, 여러분 자신의 예를 적는 것은 여러분이 그 문제에 대한 이해를 확고히 하는 데 도움이 될 수 있습니다.

간단한 예나 두 가지 입력 및 출력부터 시작합니다. 우리의 추가 기능으로 돌아가자.

우리의 기능을 "추가"라고 부르자.

입력 예제는 무엇입니까? 입력 예:

// 추가 (2, 3)

이것의 생산량은 얼마나 됩니까? 예제 출력을 쓰기 위해 다음과 같이 쓸 수 있습니다.

// 추가 (2, 3) ---> 5

이것은 우리 함수가 2와 3의 입력을 받아 5를 출력으로 반환한다는 것을 나타냅니다.

### 복잡한 예를 만듭니다.

좀 더 복잡한 예제를 살펴봄으로써 시간을 내어 고려해야 할 가장 중요한 사례를 찾아볼 수 있습니다.

예를 들어, 만약 우리의 입력이 숫자 대신에 문자열이라면 우리는 어떻게 해야 할까요? 입력으로 두 개의 문자열(예: add(`a`, `b`)이 있으면 어떻게 됩니까?

면접관이 숫자가 아닌 입력이 있는 경우 오류 메시지를 반환하라고 지시할 수 있습니다. 이 경우 이 작업을 수행해야 한다는 것을 기억하는 데 도움이 되는 경우 코드 설명을 추가하여 이 사례를 처리할 수 있습니다.

```js
// return error if inputs are not numbers.
```

또한 인터뷰 진행자는 입력 내용이 항상 숫자일 것이라고 가정하라고 말할 수 있습니다. 이 경우 이 입력 에지 케이스를 처리하기 위해 추가 코드를 작성할 필요가 없습니다.

면접관이 없고 이 문제를 해결하는 중이면 잘못된 입력을 입력할 때 어떤 일이 발생하는지 알 수 있습니다.

예를 들어, 일부 문제는 "영점 입력이 있는 경우 정의되지 않은 반환"이라고 말합니다. 이와 같은 경우에는 선택적으로 주석을 작성할 수 있습니다.

// 입력이 없는지 확인합니다.`

`// 입력이 없으면 정의되지 않은 상태로 돌아갑니다.`

우리의 목적을 위해, 우리는 우리의 입력은 항상 숫자가 될 것이라고 가정할 것이다. 하지만 일반적으로, 가장 중요한 사례에 대해 생각하는 것이 좋습니다.

컴퓨터 과학 교수 에반스는 개발자들이 말하는 방어 코드를 쓰라고 말한다. 무엇이 잘못될 수 있고 코드가 가능한 오류로부터 어떻게 방어할 수 있는지 생각해 보십시오.

2단계로 넘어가기 전에 1단계를 요약하고 문제를 이해하겠습니다.

-문제를 읽어보세요.`

- 입력 내용은 무엇입니까?`

- 결과는 어떻게 됩니까?`

간단한 예를 만든 다음 더 복잡한 예를 만듭니다.`

## 2. 문제 해결을 위한 계획을 세워라.

다음으로, 문제를 어떻게 해결할 것인가에 대한 계획을 세우세요. 계획을 세울 때 유사 코드로 작성하세요.

의사 코드(Pseudocode)는 알고리즘의 단계에 대한 일반 언어 설명이다. 즉, 의사 코드는 문제를 해결하는 방법에 대한 단계별 계획입니다.

문제를 해결하기 위해 취해야 할 단계를 적어라. 좀 더 복잡한 문제라면, 더 많은 단계가 있을 거예요. 이 문제에 대해 다음과 같이 쓸 수 있습니다.

// 합계 변수를 생성합니다.`

addition 연산자를 사용하여 첫 번째 입력을 두 번째 입력에 추가합니다.

`// 두 입력의 값을 합계 변수에 저장합니다.`

// 합계 변수를 출력하여 반환합니다.`

이제 문제를 해결하기 위한 단계별 계획이 있습니다.

좀 더 복잡한 문제에 대해 에반스 교수는 "인간이 어떻게 문제를 해결하는지 체계적으로 생각해 보라"고 지적한다. 즉, 여러분의 코드가 어떻게 문제를 해결할 수 있는지에 대해 잠시 잊고, 인간으로서 그것을 어떻게 해결할 수 있을지 생각해 보세요. 이렇게 하면 단계를 더 명확하게 볼 수 있습니다.

## 3. 계획 실행 (문제 해결!)

![image](https://cdn.pixabay.com/photo/2017/04/06/15/02/hand-2208491_960_720.jpg)

문제 해결 전략의 다음 단계는 문제를 해결하는 것이다. 의사 코드를 가이드로 사용하여 실제 코드를 작성합니다.

에반스 교수는 간단하고 기계적인 해결책에 초점을 맞출 것을 제안한다. 솔루션이 쉽고 간단할수록 올바르게 프로그래밍할 수 있습니다.

의사 코드를 사용하여 다음과 같이 쓸 수 있습니다.

```js
function add(a, b) {
 const sum = a + b;
 return sum;
}
```

에반스 교수는 시기상조적으로 최적화하지 말 것을 기억하라고 덧붙인다. 즉, 여러분은 "잠깐만요, 제가 이 일을 하고 있는데 비효율적인 코드가 될 거예요!"라고 말하고 싶을 수도 있습니다.

우선, 여러분의 간단하고 기계적인 해결책을 꺼내보세요.

만약 당신이 모든 문제를 해결하지 못한다면요? 아직 해결할 방법을 모르는 부분이 있다면요?

콜트 스틸은 다음과 같은 훌륭한 조언을 제공합니다. 만약 당신이 문제의 일부를 해결할 수 없다면, 당신을 화나게 하는 어려운 부분은 무시하세요. 대신, 여러분이 글을 쓰기 시작할 수 있는 다른 모든 것에 집중하세요.

당신이 잘 이해하지 못하는 문제의 어려운 부분은 잠시 무시하고 다른 부분을 써라. 이것이 끝나면, 더 어려운 부분으로 돌아오세요.

이렇게 하면 문제를 최소한 일부라도 끝낼 수 있습니다. 그리고 종종, 여러분은 그 어려운 문제를 해결하는 방법을 다시 한 번 깨닫게 될 것입니다.

## 4단계: 당신이 한 일을 되돌아보세요.

솔루션이 제대로 작동하면 시간을 들여 솔루션을 재고하고 개선 방법을 생각해 보십시오. 지금이 솔루션을 보다 효율적인 솔루션으로 재팩터링하는 시기일 수 있습니다.

작업을 살펴보면서 Colt Steel이 솔루션을 개선할 수 있는 방법을 모색하기 위해 제안하는 몇 가지 질문은 다음과 같습니다.

- 결과를 다르게 도출할 수 있습니까? 실행 가능한 다른 접근법에는 어떤 것들이 있나요?
- 당신은 한눈에 그것을 이해할 수 있습니까? 그게 말이 되는 건가요?
- 결과나 방법을 다른 문제에 사용할 수 있습니까?
- 솔루션 성능을 개선할 수 있습니까?
- 당신은 리팩터링을 할 다른 방법들을 생각할 수 있습니까?
- 다른 사람들은 이 문제를 어떻게 해결했을까?

한 가지 방법은 코드를 보다 간결하게 만들기 위해 문제를 재구성할 수 있습니다. 즉, 변수를 제거하고 암시적 결과를 사용합니다.

```js
function add(a, b) {
 return a + b;
}
```

4단계에서는 문제가 끝나지 않은 것처럼 느껴질 수 있습니다. 위대한 개발자들조차도 나중에 보고 바꾸고 싶은 코드를 여전히 쓰고 있다. 다음은 도움이 될 수 있는 유도 질문입니다.

인터뷰에 아직 시간이 남아 있다면 이 단계를 거쳐 솔루션을 개선할 수 있습니다. 스스로 코딩하는 경우 시간을 내어 이러한 단계를 검토하십시오.

제가 스스로 코딩 연습을 할 때, 저는 거의 항상 제가 생각해낸 것보다 더 우아하거나 효과적인 해결책을 봅니다.

## 마무리 중

이 게시물에서는 코딩 문제를 해결하기 위한 4단계 문제 해결 전략을 살펴보았습니다.

여기서 해당 내용을 검토하겠습니다.

- 1단계: 문제를 이해합니다.
- 2단계: 해결 방법에 대한 단계별 계획을 수립합니다.
- 3단계: 계획을 수행하고 실제 코드를 작성합니다.
- 4단계: 뒤돌아보고 더 나은 해결책이 있다면 리팩터링할 수 있습니다.

이 문제 해결 방법을 연습하는 것은 기술 인터뷰와 개발자로서 제 직업에 큰 도움이 되었습니다.

코딩 문제를 풀 때 자신이 없다면 문제 해결은 시간과 연습으로 누구나 더 잘 할 수 있는 기술이라는 점을 기억하면 된다.

행운을 빕니다.

### 이 게시물이 즐거우셨다면 저의 코딩 클럽에 가입하세요. 우리는 매주 일요일에 코딩 문제를 함께 해결하고 새로운 기술을 배우면서 서로를 지원합니다.

### 이 게시물에 대한 피드백이나 질문이 있으시면 언제든지 @madisonkanna를 트윗해 주십시오.