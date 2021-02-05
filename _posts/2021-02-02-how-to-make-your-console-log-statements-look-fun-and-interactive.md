---
layout: post
title: "콘솔 출력을 JavaScript 및 Node.js에서 재미 있고 인터랙티브하게 만드는 방법
 "
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1496024840928-4c417adf211d?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDJ8fGZ1bnxlbnwwfHx8&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


이 자습서에서는 JavaScript 및 Node.js의`console.log` 문에 무작위 지연을 추가하는 방법을 알아 봅니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/ezgif.com-gif-maker.gif)

## 왜 이렇게 하시겠습니까?
 

우선 프로그래밍은 재미 있어야합니다.
 그리고`console.log`와 같은 지루한 것을 멋지게 보이게하는 것은 매우 즐겁습니다.
 

소스 코드에 빠르게 액세스하려면이 GitHub 저장소를 확인하세요.
 

## 1 단계 : 문자열을 받아 console.log에 전달하는 함수 만들기
 

모든 단계가 명확한 지 확인하기 위해 작게 시작하여 문자열을 매개 변수로 받아들이고 콘솔에 기록하는 함수를 만듭니다.
 

```js
const log = (s) => {
  console.log(s);
}
```

## 2 단계 : 문자열의 문자를 하나씩 기록
 

개별 문자의 출력 사이에 지연을 추가하기 전에 실제로 분할되었는지 확인해야합니다.
 

문자열의 각 문자를 반복하여 콘솔에 출력하는 `for`루프를 추가해 보겠습니다.
 

```js
const log = (s) => {
  for (const c of s) {
    console.log(c);
  }
}
```

## 3 단계 : 줄 바꿈 문제를 해결하는 방법
 

이제`console.log`를 호출 할 때마다 빈 줄이 추가되므로 각 문자가 새 줄에 인쇄됩니다.
 

`console.log`를 본질적으로 동일한 작업을 수행하지만 출력 뒤에 새 줄을 추가하지 않는`process.stdout.write`로 대체합니다.
 

그러나 이제 우리는 출력의 끝에서 개행을 잃어 버렸습니다. 이것은 여전히 바람직합니다.
 `\ n` 문자를 명시 적으로 인쇄하여 추가합니다.
 

```js
const log = (s) => {
  for (const c of s) {
    process.stdout.write(c);
  }
  process.stdout.write('\n');
}
```

## 4 단계 : 'sleep'기능 구현
 

JavaScript에서는 일정 시간 동안 동기 코드의 실행을 단순히 멈출 수 없습니다.
 이를 위해서는 우리 자신의 함수를 작성해야합니다.
 수면이라고합시다.
 

단일 매개 변수 `ms`를 허용하고 `ms`밀리 초 지연 후 해결되는 Promise를 반환해야합니다.
 

```js
const sleep = (ms) => {
  return new Promise(resolve => setTimeout(resolve, ms));
};
```

## 5 단계 : 지연 추가
 

이제 출력에 지연을 추가 할 준비가되었습니다!
 여기에 몇 가지가 필요합니다.
 

- 함수`log`에`delay` 매개 변수 추가
 
- 키워드`async`를 추가하여`log` 함수를 비동기로 만듭니다.
 
- 다음 루프 반복을`delay` 밀리 초만큼 지연시키는`sleep` 함수를 호출합니다.
 

```js
const sleep = (ms) => {
  return new Promise(resolve => setTimeout(resolve, ms));
};

const log = async (s, delay) => {
  for (const c of s) {
    process.stdout.write(c);
    await sleep(delay);
  }
  process.stdout.write('\n');
}
```

## 6 단계 : 무작위 지연 구현
 

타이밍을 무작위로 지정하면 출력이 더 좋아 보일 것입니다.
 

함수`log`에 또 다른 부울 매개 변수`randomized`를 추가해 보겠습니다.
 참이면 `sleep`에 전달 된 인수는 `0`에서 `delay`밀리 초 사이 여야합니다.
 

```js
const sleep = (ms) => {
  return new Promise(resolve => setTimeout(resolve, ms));
};

const log = async (s, delay, randomized) => {
  for (const c of s) {
    process.stdout.write(c);
    await sleep((randomized ? Math.random() : 1) * delay);
  }
  process.stdout.write('\n');
}
```

삼항 연산자를 사용했지만 일반`if` 문으로 바꿀 수 있습니다.
 

```js
if (randomized) {
  sleep(Math.random * delay);
} else {
  sleep(delay);
}
```

## 7 단계 : 로그를 구성 가능하게 만들기
 

지금 우리는 우리가 원하는 거의 모든 것을 구현했습니다.
 그러나 우리가 무언가를 콘솔에 출력하고 싶을 때마다`delay`와 randomization 플래그를 전달해야하기 때문에 호출하는 것은 매우 깨끗하지 않습니다.
 

```js
log('Hello, world!', 100, true);
log('What\'s up?', 100, true);
log('How are you?', 100, true);
```

출력하려는 문자열 인 단일 매개 변수로 호출 할 수있는 구성 가능한 로그를 가질 수 있다면 좋을 것입니다.
 

이렇게하려면 코드를 다시 작성해야합니다.
 계획은 다음과 같습니다.
 

- 현재의 모든 기능을 `delay`및 `randomized`필드 2 개가있는 개체를받는 단일 함수 `funkylog`로 래핑합니다.
 
- `funkylog`는 익명의 화살표 함수를 반환해야합니다.
 구현은 1 ~ 6 단계에서 구현 한`log`와 동일해야합니다.
 
- `delay` 및`randomized` 매개 변수는`funkylog`에서 전달되므로`log` 함수에서 제거해야합니다.
 

```js
const funkylog = ({ delay, randomized }) => {
  const sleep = (ms) => {
    return new Promise(resolve => setTimeout(resolve, ms));
  };
    
  return async (s) => {
    for (const c of s) {
      process.stdout.write(c);
      await sleep((randomized ? Math.random() : 1) * delay);
    }
    process.stdout.write('\n');
  }
};
```

## 8 단계 : 마무리 작업 추가
 

우리가 가진 것을 살펴 보자 :
 

```js
const log = funkylog({ delay: 100, randomized: true });

log('Hello, world!');
log('What\'s up?');
log('How are you?');
```

- `funkylog`함수를 사용하여 구성 가능한 로거를 만들 수 있습니다.
 
- 원하는 지연을 선택할 수 있습니다.
 
- 로거를 사용한다고해서 호출 할 때마다 `지연`을 전달할 필요는 없습니다.
 

우리가 할 수있는 또 하나의 개선은`delay` 매개 변수에 기본값을 제공하는 것입니다.
 

```js
const funkylog = ({ delay = 100, randomized }) => {
    ..
    ..
```

이제 인수없이`funkylog`를 만들 수 있으며 여전히 작동합니다!
 

```js
const log = funkylog();

console.log('Hello, world!');
```

## 개선 아이디어
 

처음부터 말씀 드렸듯이 우선 프로그래밍은 재미 있어야합니다.
 그렇지 않으면 그것은 일상이 될 것이고 당신은 그것을 즐기지 않을 것입니다.
 

`funkylog`를 추가로 개선하고 결과가 어떻게 표시되는지 알려주세요!
 예를 들어, 색상을 지정하여 출력을 멋지게 꾸밀 수 있습니다.
 이를 위해`npm` 모듈`chalk`를 사용할 수 있습니다.
 

그런 다음 다른 색상을 구현 한 후 문자열의 단어 사이에 추가 지연을 추가하는 다른 플래그를 추가 할 수 있습니다.
 

전체 튜토리얼을 진행하는 동안 나와 함께 해주셔서 감사합니다!
learn.coderslang.com에서 프로그래밍 블로그를 작성하고 Full Stack JS 과정을 구축합니다.
 

### 이 튜토리얼에 대한 피드백이나 질문이 있으면 언제든지 @coderslang을 트윗하거나 Telegram @coderslang_chat에서 토론에 참여하십시오.
 