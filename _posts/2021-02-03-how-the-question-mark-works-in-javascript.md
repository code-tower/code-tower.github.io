---
layout: post
title: "자바스크립트에서 물음표(?) 연산자의 작동 방식"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--5--1.png
tags: undefined
---


조건 또는 물음표 연산자는 자바스크립트에서 가장 강력한 기능 중 하나이다. ? 연산자는 조건부 문에서 사용되며, 다음과 쌍을 이룰 경우 if...else 문장의 컴팩트한 대안으로 기능할 수 있다.

하지만 그것에는 눈에 보이는 것 이상의 것이 있다. `?` 연산자의 용도는 크게 세 가지가 있는데, 그 중 두 가지는 사용하지 않거나 심지어 듣지 못할 수도 있다. 그들에 대해 자세히 알아보자.

## JavaScript에서 물음표('?')에 대한 세 가지 주요 용도:

- 터너리 연산자
- 선택적 체인
- 무효화 결합

이 각각에 대해 자세히 알아보겠습니다. 가장 일반적인 방법인 `?` 연산자가 터미널 연산자로 사용되는 것을 볼 수 있습니다.

## 1. Ternary 연산자

용어란 세 가지 항목 또는 부분으로 구성된 것을 말한다. ? 연산자는 ternary 연산자라고도 불리는데, terminary 연산자(단수 연산자)는 엄격한 등가(===)나 나머지(%)와 달리 3개의 연산자를 사용하는 연산자뿐이기 때문이다.

`??`로 시작하여 왼쪽에는 조건을 추가하고 오른쪽에는 값을 추가하여 조건이 참일 때 반환합니다. 그런 다음 콜론(`:`)을 추가한 다음 조건이 거짓이면 반환할 값을 추가합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--1-.png)

종말 연산자는 기본적으로 전통적인 if...otherse 문장의 지름길이다.

ternary 연산자를 더 긴 `if...other` 문과 비교해보자.

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--22-.png)

여기서 터미널 연산자는 코드 한 줄만 사용하는 반면 if...else는 7줄을 사용합니다.

터미널 운영자를 사용하는 것이 훨씬 효과적이죠?

## 2. 옵션 체인

2020년에는 옵션 체인으로 알려진 멋진 새로운 기능이 도입되었다.

작동 방식을 이해하려면 이 시나리오를 상상해 보십시오.

존재하지 않는 개체 속성을 호출하여 런타임에 오류를 트리거하는 코드가 있다고 가정해 보겠습니다. 데이터베이스 또는 API에 없거나 정의되지 않은 값이 있기 때문일 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--23--2.png)

![image](https://www.freecodecamp.org/news/content/images/2021/02/Screenshot-2021-01-25-00-56-06.png)

선택적 체인 덕분에 속성 이름과 다음 속성 사이의 기간 사이에 `?`를 삽입할 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--24-.png)

이를 통해 추악한 오류를 범하지 않고 정의되지 않은 오류만 반환하게 된다.

선택적 체인은 JavaScript 개발자를 위한 진정한 삶의 변화 기능입니다.

## 3. 무효화 연합

경우에 따라 누락된 속성 이름 또는 값에 대한 기본값을 설정해야 합니다.

예를 들어, 우리가 온도, 습도, 풍속, 압력, 일출과 일몰의 시간, 그리고 도시의 그림을 가져오는 날씨 앱을 만든다고 가정해 보자. 예를 들어, Bangalore라고 하는 장소를 입력했는데, 어떤 이유에서인지 데이터베이스에 이미지가 없습니다.

앱에서 데이터를 가져오고 표시하면 사진이 공백이 되어 보기 흉할 수 있습니다. 우리가 할 수 있는 것은, 그런 경우, 이미지가 없는 도시들을 위한 기본 그림을 설정하는 것입니다. 우리의 경우 방갈로르입니다.

이렇게 하면 앱에서 데이터를 표시할 때 기본 사진은 이미지가 없는 도시에 표시됩니다.

논리 OR 연산자로 알려진 `||` 연산자를 사용하여 이 작업을 수행할 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--4-.png)

그러나 기본값을 제공하기 위해 `||`를 사용하는 경우 일부 값(예: ``` 또는 `0`)을 사용할 수 있는 것으로 간주할 경우 예기치 않은 동작이 발생할 수 있습니다.

변수의 값이 0 또는 빈 문자열인 시나리오를 고려해 보십시오. (`||`)를 사용하면 정의되지 않음 또는 NULL로 간주되어 수정된 일부 기본값을 반환합니다.

논리 OR(`|`) 연산자 대신 이중 물음표(`??)를 사용할 수 있습니다.`), 또는 무효화 병합.

예를 들어 배우자.

여기서는 변수 1에 `0`과 `기본 문자열`이 있습니다. 콘솔에 값을 기록하면 `기본 문자열`이 나오는데 이상해요. 0이 정의되지 않았거나 null이 아니므로 기본 문자열 대신 0이 와야 합니다. 그래서 `||`는 여기서 그 일을 하지 못한다.

마찬가지로 값 2도 마찬가지입니다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--25-.png)

하지만 만약 우리가 `||`를 ``로 대체한다면0에 빈 줄이 생기니까 시원하다.

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--26-.png)

Nullish Coalescing은 논리 OR 연산자와 동일하게 작동하지만, 왼쪽 값이 `defined` 또는 `null`일 때 오른쪽 값을 얻게 됩니다.

다른 말로 하자면, `??`는 `ㄹ`과 `ㄹ` 값만 허용하고 빈 문자열(``)이나 `0`은 허용하지 않는다.

## 결론

이제 자바스크립트에서 `?` 연산자가 어떻게 동작하는지 이해하셨기를 바랍니다. 단순해 보이지만, 언어에서 가장 강력한 문자 중 하나입니다. 그것은 세 가지 놀랍지만 다른 방법으로 통사당을 제공한다.

그것들을 시험해 보고 어떤지 나에게 알려줘.

즐거운 배움!