---
layout: post
title: "이 8가지 가장 일반적인 사용 사례를 통해 Flexbox 알아보기"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/02/Ep5_thumbnail.png
tags: undefined
---


응답성이 뛰어난 웹 사이트 구축과 관련하여 Flexbox는 유연하고 응답성이 뛰어난 레이아웃을 매우 쉽게 만들 수 있도록 지원합니다. 따라서 Front-end 개발자는 Flexbox를 반드시 배워야 합니다.

그러나 많은 튜토리얼이 한 번에 모든 것을 가르치려고 하고 각 개념을 언제, 왜 사용할 것인지 알려주는 것을 잊습니다.

이 튜토리얼에서는 8가지 작업을 함께 해결하여 Flexbox의 가장 일반적인 사용 사례를 보여드리겠습니다. 마지막에는 다음 프로젝트에서 Flexbox를 사용할 준비가 될 것입니다.

여기에서 시동기를 다운로드할 수 있습니다. Flexbox-Tutorial-Starter

다음은 이 기사를 보완하려는 경우 볼 수 있는 비디오입니다.

### 세우다

index.html 파일을 다운로드하여 열면 총 8개의 작업이 표시됩니다. 각 태스크에 대해 컨테이너와 항목이 해당 태스크 안에 있습니다. 폭과 높이가 40px인 div 요소다.

## 과제 1: Flexbox에서 블록 요소를 수평으로 정렬

첫 번째 작업의 경우 블록 요소를 수평으로 정렬합니다. 기본적으로 블록 요소는 서로 쌓입니다. 하지만 플렉스 용기 안에 넣으면:

```css
.container {
  display: flex;
}

```

![image](https://www.freecodecamp.org/news/content/images/2021/02/Screenshot-2021-02-03-at-17.10.46-1.png)

모든 블록 요소가 수평 축에 정렬됩니다. 아주 쉽죠? 😉 첫 번째 과제를 마치겠습니다.

## 과제 2: Flexbox의 용기 중앙에 있는 중앙 항목

다음 작업을 위해 일부 품목은 용기 중앙에 배치해야 합니다. 플렉스 컨테이너에 정당성-콘텐츠:센터(center)와 정렬-아이템:센터(center)로 설정하면 됩니다.

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}

```

![image](https://www.freecodecamp.org/news/content/images/2021/02/Screenshot-2021-02-03-at-17.11.13-1.png)

이제 과제 2를 마치겠습니다. 그러나 다음으로 넘어가기 전에 `정당성-내용`과 `일정성-항목`의 특성에 대해 좀 더 자세히 알아보자.

### 1. 정당성-내용 속성

정당화-콘텐츠를 통해 수평축에 맞춰 아이템을 정렬할 수 있다.

예를 들어 컨테이너의 시작 부분에서 수평 축에 항목을 정렬하려면 다음과 같이 합니다.

```undefined
.container {
  display: flex;
  justify-content: flex-start;
}

```

컨테이너 끝에서 다음 작업을 수행합니다.

```undefined
.container {
  display: flex;
  justify-content: flex-end;
}

```

그리고 용기 중앙에서 이렇게 할 것입니다.

```undefined
.container {
  display: flex;
  justify-content: center;
}

```

![image](https://www.freecodecamp.org/news/content/images/2021/02/flex-1.png)

### 2. 맞춤식 속성

이 속성은 `합리화-콘텐츠`와 유사하지만 수직축에 있습니다. `얼라인 항목`을 사용하면 다음과 같이 컨테이너의 시작 부분에서 수직 축에 있는 항목을 정렬할 수 있습니다.

```undefined
.container {
  display: flex;
  align-items: flex-start;
}

```

다음과 같은 컨테이너의 끝에서:

```undefined
.container {
  display: flex;
  align-items: flex-end;
}

```

- 그리고 컨테이너의 중앙에는 다음과 같은 것들이 있습니다.

```undefined
.container {
  display: flex;
  align-items: center;
}

```

이제 내용 정당화와 정렬 항목을 결합하면 컨테이너 중앙, 오른쪽 하단 모서리, 오른쪽 상단 모서리 등에 항목을 정렬할 수 있습니다.

## 과제 3: Flexbox의 항목 간에 공간 배분

세 번째 작업의 경우 항목 사이에 동일한 공간을 추가해야 합니다. 이것을 성취하기 위해서, 그것은 꽤 간단하다. 우리가 해야 할 일은 플렉스 컨테이너에 `정당성-내용: 공간-between;`을 주는 것이다.

```undefined
.container {
  display: flex;
  justify-content: space-between;
}

```

"content: space-between;"은 우리에게 아이템 사이의 동일한 공간을 제공한다.

예를 들어 항목 사이에 동일한 공간을 두어야 하는 경우 탐색에 매우 유용합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/navigation.png)

그리고 우리는 `공간 사이`와 `합리화-콘텐츠`를 함께 고려하기 때문에 `공간 대등`과 `공간 대비` 가치도 줄 수 있다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/justify.png)

콘텐츠 정당화(prighty-content) 값을 공간 균등하게 부여하면 아이템 간에는 물론 첫 번째 아이템 전후에 공백이 추가된다.

콘텐츠 정당화(prightify-content)를 공간구축(space-round)으로 부여하면 아이템 주변에 동일한 공간이 추가된다.

## 과제 4: Flexbox의 용기 끝까지 항목 밀어넣기

과제 4의 경우 마지막 항목을 수평축 컨테이너 끝으로 밀어넣어야 합니다. 저는 Flexbox를 사용하여 3가지 옵션을 보여드리겠습니다.

컨테이너 안에 2개의 항목이 있으면 `정당한 내용: 공간 사이;`를 사용할 수 있습니다. 첫 번째 항목은 시작 부분으로, 마지막 항목은 컨테이너 끝으로 밀어넣습니다.

```undefined
.container {
  display: flex;
  justify-content: space-between;
}

```

로고와 버튼만 있는 경우를 예에서 볼 수 있습니다.

![image](https://dev-to-uploads.s3.amazonaws.com/i/dtxocmk4n22t3ga8h4ro.png)

또는 로고 및 탐색 항목:

![image](https://dev-to-uploads.s3.amazonaws.com/i/kchezon63sxjjjcr6o31.png)

3개 이상의 아이템으로, 아이템 사이에 플렉스그로우:1이 있는 빈 div를 추가하고자 합니다.

예를 들어 두 번째 항목과 마지막 항목(세 번째 항목) 사이에 `플렉스로 성장: 1`이 있는 `div`를 놓으면 빈 div가 최대한 확장되어 마지막 항목을 컨테이너 끝으로 밀어넣습니다.

```html
  <div class="option-2">
     <div class="container">
        <div class="item sm"></div>

        <div class="item"></div>

        <div class="space"></div>

        <div class="item"></div>
        </div>
  </div>

```

```undefined
  .option-2 .space {
    flex-grow: 1;
  }

```

![image](https://www.freecodecamp.org/news/content/images/2021/02/flex-grow.png)

다음과 같은 복잡한 탐색을 통해 이를 확인할 수 있습니다.

![image](https://dev-to-uploads.s3.amazonaws.com/i/53bomxpqg8dattgno25f.png)

예를 들어, 2개의 항목이 있으면 첫 번째 항목인 `Flex-grow: 1;`를 줄 수 있습니다. 이렇게 하면 첫 번째 항목이 최대한 확장되므로 마지막 항목을 컨테이너 끝으로 밀어넣습니다.

```undefined
  .option-3 .item:first-child {
    flex-grow: 1;
  }

```

![image](https://www.freecodecamp.org/news/content/images/2021/02/flex-grow-2.png)

입력 구성 요소에는 몇 가지 예가 있습니다.

![image](https://dev-to-uploads.s3.amazonaws.com/i/ww5uvqfjntpfab9nah8a.png)

우리는 또한 `마진 왼쪽: auto`를 사용하여 마지막 항목을 컨테이너 끝으로 밀어 넣을 수 있습니다. 예를 들어 옵션 1에서 마지막 항목인 `마진-왼쪽: auto;`를 지정하면 동일하게 작동합니다.

```css
.task-4 .option-1 .container {
  display: flex;
}

.task-4 .option-1 .item:last-child {
  margin-left: auto;
}

```

auto는 정말 유용하지만 다른 기사와 동영상으로 자세히 알아보자.

## 과제 5: Flexbox에서 상대적 크기 열 레이아웃 구축

항목의 플렉스 값을 "flex: {number}"로 지정하면 다른 항목에 비해 항목의 크기를 제어할 수 있습니다. 예를 들어 이 코드:

```css
.task-5 .item-1 {
  flex: 3;
}

.task-5 .item-2 {
  flex: 1;
}

.task-5 .item-3 {
  flex: 1;
}

.task-5 .item-4 {
  flex: 1;
}

```

우리는 방금 총 6개의 열이 있는 레이아웃을 만들었습니다. 항목 1은 3개의 열을 차지하며, 나머지 항목 3개는 1개의 열을 차지합니다.

예를 들어, 테이블 레이아웃에서 유용합니다.

![image](https://dev-to-uploads.s3.amazonaws.com/i/4jsmaoxclhje1bmlxr68.png)

이 레이아웃은 다른 튜토리얼에서 가져온 것입니다. 여기서 Retact + Next.js 응용 프로그램을 처음부터 끝까지 빌드하는 방법을 보여 줍니다. 여기 유투브 링크가 있습니다. 보고 코딩을 하고 싶으시다면요.

## 과제 6: 미디어 쿼리가 있거나 없는 Flexbox에서 응답성이 뛰어난 레이아웃 구축

### 1. 미디어 쿼리 없이 응답 가능한 레이아웃

플렉스 컨테이너 `flex-wrap:rap`을 제공할 경우:

```css
.task-6 .container {
  display: flex;
  flex-wrap: wrap;
}

```

컨테이너 내부에서 항목을 축소하지 않는 대응형 레이아웃을 만들 것입니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/Screenshot-2021-02-03-at-21.44.31.png)

### 2. 미디어 질의 응답형 레이아웃

미디어 조회를 통해 우리는 아이템의 크기를 더 많이 제어할 수 있게 될 것입니다. 플렉스 랩 용기 안에 2개의 기둥을 넣었으면 합니다. 다음과 같은 방법으로 이를 수행할 수 있습니다.

```css
.task-6 .container {
  display: flex;
  flex-wrap: wrap;
}

.task-6 .item {
  flex-basis: 50%;
}

```

이제 항목이 2열 레이아웃으로 배열되어 각 열이 용기의 절반을 차지합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/Screenshot-2021-02-03-at-21.45.25.png)

같은 논리로 화면이 375px보다 넓을 때 4열 배치를 원한다고 하면 모든 항목에 플렉스-베이스: 25%를 줄 수 있다.

```css
@media (min-width: 375px) {
  .task-6 .item {
    display: flex;
    flex-basis: 25%;
  }
}

```

![image](https://www.freecodecamp.org/news/content/images/2021/02/Screenshot-2021-02-03-at-21.47.20.png)

## 과제 7: Flexbox의 항목 순서 변경(일반적이지 않음)

Flexbox를 사용하면 품목 순서를 변경할 수 있습니다. 예를 들어, 플렉스 컨테이너 안에 4개의 아이템이 있는데 첫 번째 아이템을 행 끝에 넣으려고 하면 됩니다. 우리가 해야 할 일은 `주문:1` 항목을 주기만 하면 됩니다.

```css
.task-7 .item-1 {
  order: 1;
}

```

기본적으로 순서 속성의 값은 0이고 음수가 될 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/Screenshot-2021-02-03-at-21.48.20.png)

## 과제 8: 플렉스 컨테이너 내부의 품목 위치 변경(일반적이지 않음)

플렉스 안의 아이템은 얼라인셀프(align-self)를 이용해 스스로 위치를 바꿀 수 있다.

```css
align-self: auto | flex-start | flex-end | center | baseline | stretch;

```

예를 들어 컨테이너 끝에 항목 3을 수직 축에 두고 싶다고 가정해 보겠습니다. 이렇게 할 수 있습니다.

```css
.task-8 .container {
  display: flex;
}

.task-8 .item-3 {
  align-self: flex-end;
}

```

![image](https://www.freecodecamp.org/news/content/images/2021/02/Screenshot-2021-02-03-at-21.49.00.png)

## '변형 방향'

Flexbox에는 기본적으로 `Flex-direction` 속성이 있습니다. flex-direction은 row의 값을 가지며, 이는 아이템이 수평축에 정렬됨을 의미한다.

항목을 수직 축에 정렬하려면 `가변 방향: 열;`을 사용합니다.

예를 들어, 태스크 3에서 플렉스 컨테이너 `Flex-direction: column;`을 제공하는 경우:

```css
.task-3 .container {
  display: flex;

  justify-content: space-between;
  flex-direction: column;
}

```

다음과 같은 이점을 얻을 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/Screenshot-2021-02-03-at-21.50.19.png)

방금 배웠던 flex-direction: row; flex-direction: column;은 여전히 동일하게 동작하지만, 수평축 대신 수직축이 됩니다.

## 결론

이제 Flexbox 및 CSS Grid에 대해 배웠으므로 응답성이 뛰어난 웹 사이트를 구축하여 계속할 수 있습니다. devchallenges.io에서 할 프로젝트 목록을 찾을 수도 있고, 다음 비디오 튜토리얼에 참여하실 수도 있습니다. 여기에서 처음부터 끝까지 전문 웹 사이트를 구축하겠습니다.

이 기사를 읽어주셔서 감사합니다. 이 항목은 학습에서 업데이트할 비디오 시리즈에 속합니다.DevChallenges.io. 최신 정보를 알려면 SNS를 팔로우하거나 유튜브 채널을 구독하세요. 그렇지 않으면, 코딩 작업을 완료하고 다음 비디오 및 👋 기사에서 뵙겠습니다.

________ 🐣 나에 대해____________________________________

저는 풀스택 개발자, UX/UI 디자이너, 콘텐츠 제작자입니다. 이 짧은 비디오를 통해 저를 더 알 수 있습니다.

- 저는 Dev Challenges의 설립자입니다.
- 내 유튜브 채널 구독
- 내 트위터 팔로우
- 불협화음 참여