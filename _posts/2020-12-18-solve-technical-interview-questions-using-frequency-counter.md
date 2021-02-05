---
layout: post
title: "기술면접을 위한 문제해결 패턴 : 주파수 카운터 패턴 설명"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/beach.jpg
tags: undefined
---


지난번 기사에서는 소프트웨어 개발자 면접을 준비하는 방법에 대한 생각을 공유했습니다.

이 기사에서는 기어를 약간 바꿔서 기술 면접에서 문제를 해결하기 위해 사용할 수 있는 일반적인 패턴에 대해 이야기하려고 합니다. 주파수 카운터 패턴에 대해 심도 있게 논의하여 효과적으로 해결할 수 있도록 하겠습니다.

## "주파수 카운터" 패턴은 무엇입니까?

Frequency Counter(주파수 카운터) 패턴은 개체 또는 집합을 사용하여 값 및 해당 값의 빈도를 수집합니다.

이 패턴은 종종 `array` 또는 `string`과 함께 사용되며 중첩된 루프(사분위 시간 복잡성 `O(n➡)`를 피할 수 있습니다.

## 주파수 카운터 패턴은 언제 사용해야 합니까?

주파수 카운터 패턴은 서로 비교하려는 데이터가 여러 개일 때 가장 유용합니다. 주파수 카운터가 작동 중인 것을 보기 위해 예를 보여드리겠습니다.

## "동일한 제곱" 연습

- 두 개의 배열을 수용하는 `same squared` 함수 쓰기
- 첫 번째 배열의 모든 값이 두 번째 배열의 해당 값 제곱인 경우 함수는 `true`를 반환해야 합니다.
- 값의 빈도는 동일해야 합니다.

### 최적의 결과는 무엇입니까?

함수가 작성된 후에는 "동일한 제곱" 함수가 이러한 값을 반환할 것으로 예상해야 합니다.

"동일한 제곱([1, 2, 3], [4, 1, 9]; // 참"

"동일한 제곱([1, 2, 3], [1, 9]; // 거짓"

`동일한 제곱([1, 2, 1], [4, 4, 1]; // 거짓`

"동일한 제곱([2, 3, 6, 8, 8], [64, 36, 4, 9, 64]; // 참"

### 시작 중

먼저 `함수` 키워드를 사용하여 식별자 `same squared`로 함수를 생성한다.

```js
function sameSquared() {

```

우리의 함수 `same squared`에는 첫 번째 배열과 두 번째 배열의 두 가지 매개 변수가 필요하다. 이 예에서, 우리는 이 값들 `[1, 2, 3]과 `[4, 1, 9]을 전달하고 있다.

```js
function sameSquared(firstArr, secondArr) {

    
```

### 에지 케이스 확인

기능 블록 내부에서 몇 가지 에지 사례를 다루고자 합니다. 먼저 두 매개 변수 모두 null이 아닌 정의되지 않은 값 등 진실한 값을 가지고 있는지 확인해야 합니다.

우리는 `!` 연산자를 사용하여 잘못된 값을 확인할 수 있습니다. 첫 번째 Arr 또는 두 번째 Arr이 거짓이면 거짓을 반환합니다.

```js
function sameSquared(firstArr, secondArr) {
  if (!firstArr || !secondArr) return false;
```

다음으로 설명하고자 하는 에지 사례는 두 어레이의 길이가 동일한지 확인하는 것입니다. 서로 다르면 동일한 양의 공유 값을 포함할 수 없다는 것을 알 수 있습니다.

두 매개 변수의 `길이` 속성을 확인하여 동일한지 확인할 수 있습니다. 그렇지 않으면 거짓을 반환합니다.

```js
function sameSquared(firstArr, secondArr) {
  if (!firstArr || !secondArr) return false;
  if (firstArr.length !== secondArr.length) return false;
```

### 중첩 루프를 방지하기 위한 "사전" 작성

적어도 하나의 배열에서 모든 값을 추적해야 합니다. 이렇게 하고 중첩 루프를 피하기 위해 해시 테이블(개체)에 이러한 값을 저장할 수 있습니다. 나는 내 것을 `찾아보기`라고 부를 것이다.

```js
function sameSquared(firstArr, secondArr) {
  if (!firstArr || !secondArr) return false;
  if (firstArr.length !== secondArr.length) return false;

  const lookup = {};
```

"for of" 루프를 사용하여 "first Arr"을 반복합니다. "for of" 블록 안에서 "value * value"의 결과에 키를 할당합니다.

이 키/값 쌍의 값은 `firstArr`에서 특정 값이 "보이는" 횟수를 반영하는 주파수 카운터가 됩니다.

먼저 lookup에 `value * value` 항목이 포함되어 있는지 확인하고, 포함되어 있으면 `1`을 추가합니다. 그렇지 않으면 0에 값을 할당한 다음 1을 추가합니다.

```js
function sameSquared(firstArr, secondArr) {
  if (!firstArr || !secondArr) return false;
  if (firstArr.length !== secondArr.length) return false;

  const lookup = {};

  for (value of firstArr) {
    lookup[value * value] = (lookup[value * value] || 0) + 1;
  }
```

첫 번째 Arr 루프가 완료되면 lookup에는 다음과 같은 값이 포함되어야 합니다.

```js
{
  1: 1,
  4: 1,
  9: 1
}
```

### 배열 값 비교

이제 우리는 `1차 Arr`의 모든 값을 반복하여 각각의 제곱 값으로 저장했으므로 이 값들을 `2차 Arr`의 값에 비교하고자 한다.

우리는 또 다른 `for of` 루프를 만드는 것으로 시작한다. 새로운 "for" 블록의 첫 번째 줄에는 "second Arr"의 현재 가치가 "lookup" 안에 있지 않은지 확인하는 조건문을 쓴다. 그렇지 않으면 루프를 중지하고 false를 반환합니다.

두 번째 Arr의 값이 우리의 `찾아보기`에 있다면, 우리는 그 항목의 가치를 줄이고 싶다. 우리는 `-=` 할당 연산자를 사용하여 그렇게 할 수 있습니다.

```js
function sameSquared(firstArr, secondArr) {
  if (!firstArr || !secondArr) return false;
  if (firstArr.length !== secondArr.length) return false;

  const lookup = {};
  for (value of firstArr) {
    lookup[value * value] = (lookup[value * value] || 0) + 1;
  }
  for (secondValue of secondArr) {
    if (!lookup[secondValue]) return false;
      lookup[secondValue] -= 1;
    }
```

두 번째 Arr을 반복하고 나면 다음과 같은 값을 얻을 수 있습니다.

```js
{
  1: 0,
  4: 0,
  9: 0
}
```

### "동일한 제곱" 기능 마무리

거짓을 반환하지 않고 2차 Arr을 통해 반복을 마치면 1차 Arr은 2차 Arr의 제곱 상태에 있는 모든 값을 포함하고 있음을 의미한다. 따라서 우리는 "for" 루프 이외의 "true"를 반환합니다.

```js
function sameSquared(firstArr, secondArr) {
  if (!firstArr || !secondArr) return false;
  if (firstArr.length !== secondArr.length) return false;

  const lookup = {};
  for (value of firstArr) {
    lookup[value * value] = (lookup[value * value] || 0) + 1;
  }
  for (secondValue of secondArr) {
    if (!lookup[secondValue]) return false;
    lookup[secondValue] -= 1;
  }
  return true;
}
```

코딩 평가에서 매우 일반적으로 사용되는 다른 예를 보여드리겠습니다(이 문제를 이전에 보셨을 수도 있음).

## "is Anagram" 연습

- 두 문자열을 받아들이는 `isAnagram`이라는 함수를 작성합니다.
- 두 문자열 매개 변수가 서로 다른 그래프인 경우 함수는 true를 반환해야 합니다.

### 최적의 결과는 무엇입니까?

함수가 작성된 후에는 `isAnagram` 함수가 이러한 값을 반환할 것으로 예상해야 한다.

is Anagram("silent", "listen", // true)

is Anagram("martin", "nitram"); // true

isAnagram("cat", "tag"); // false"

is Anagram("rat", "tar"); // true

### 시작 중

먼저 `함수` 키워드를 사용하여 식별자 `isAnagram`으로 함수를 생성합니다.

```js
function isAnagram() {

```

우리의 함수 isAnagram은 첫 번째 문자열과 두 번째 문자열의 두 가지 매개 변수가 필요하다. 이 예에서 우리는 `침묵`과 `듣기`라는 값을 전달한다.

```js
function isAnagram(firstStr, secondStr) {

```

### 에지 케이스 확인

함수 블록의 처음 몇 줄에서는 첫 번째 예제와 같이 몇 가지 에지 사례를 다루려고 합니다.

isAnagram과 마찬가지로 Null이 아닌 Undefined(정의되지 않은) 등의 두 파라미터가 모두 진실된 값을 갖고 있는지 확인해야 한다. 우리는 `!` 연산자를 사용하여 잘못된 값을 확인할 수 있습니다. 첫째 Str 또는 둘째 Str이 거짓이면 거짓을 반환한다.

```js
function isAnagram(firstStr, secondStr) {
  if (!firstStr || !secondStr) return false;
```

다음으로 설명하고자 하는 에지 사례는 두 어레이의 길이가 동일한지 확인하는 것입니다. 서로 다르면 동일한 수의 공유 값을 포함할 수 없다는 것을 알 수 있습니다.

두 매개 변수의 `길이` 속성을 확인하여 동일한지 확인할 수 있습니다. 그렇지 않으면 거짓을 반환합니다.

```js
function isAnagram(firstStr, secondStr) {
  if (!firstStr || !secondStr) return false;
  if (firstStr.length !== secondStr.length) return false;
```

### 중첩 루프를 방지하기 위한 "사전" 작성

주파수 카운터 패턴을 사용하고 있으므로 적어도 하나의 배열에 있는 모든 값을 추적해야 합니다. 이제 이를 처리하는 가장 좋은 방법은 해시 테이블(개체)에 이러한 값을 저장하는 것임을 알게 되었습니다. 일관성을 유지하기 위해 저는 제 것을 `찾아보기`라고 다시 부르겠습니다.

```js
function isAnagram(firstStr, secondStr) {
  if (!firstStr || !secondStr) return false;
  if (firstStr.length !== secondStr.length) return false;

  const lookup = {};
```

"for of" 루프를 사용하여 "first Str"을 반복한다. `for of` 블록 내부에서는 `value * value`라는 식의 결과에 키를 할당합니다.

이 키/값 쌍의 값은 첫 번째 Str에서 특정 값이 "보이는" 횟수를 반영하는 주파수 카운터가 됩니다.

터미널 연산자를 사용하여 `값 * 값`에 대한 항목이 포함되어 있는지 확인하고, 포함되어 있으면 `+=` 할당 연산자를 사용하여 값을 `1`씩 증가시킨다. 그렇지 않으면 1에 값을 할당하기만 하면 됩니다.

```js
function isAnagram(firstStr, secondStr) {
 if (!firstStr || !secondStr) return false;
    if (firstStr.length !== secondStr.length) return false;

 const lookup = {};

 for (first of firstStr) {

     lookup[first] ? (lookup[first] += 1) : (lookup[first] = 1);

  }
```

첫 번째 Str 루프가 완료되면 lookup에는 다음과 같은 값이 포함되어야 합니다.

```js
{
  s: 1,
  i: 1,
  l: 1,
  e: 1,
  n: 1,
  t: 1
}
```

### 배열 값 비교

이제 우리는 첫 번째 Str의 모든 값을 반복하고 그 값을 저장했으므로 두 번째 Str의 값과 비교하고자 한다.

우리는 또 다른 `for of` 루프를 만드는 것으로 시작한다. 새로운 "for" 블록의 첫 번째 줄에는 "second Str"의 현재 값이 "lookup" 안에 있지 않은지 확인하기 위한 조건문을 쓴다. 그렇지 않으면 반복을 중지하고 false를 반환하려고 합니다.

그렇지 않으면 2str의 값이 우리의 lookup에 있다면 우리는 그 항목의 가치를 줄이고자 한다. 우리는 `-=` 할당 연산자를 사용하여 그렇게 할 수 있습니다.

```js
function isAnagram(firstStr, secondStr) {
  if (!firstStr || !secondStr) return false;
  if (firstStr.length !== secondStr.length) return false;

  const lookup = {};

  for (first of firstStr) {
    lookup[first] ? (lookup[first] += 1) : (lookup[first] = 1);
  }

  for (second of secondStr) {
    if (!lookup[second]) return false;
    lookup[second] -= 1;
  }
```

두 번째 Str을 반복하고 나면, 우리의 lookup은 다음과 같은 값을 가져야 한다.

```js
{
  s: 0,
  i: 0,
  l: 0,
  e: 0,
  n: 0,
  t: 0
}
```

### "isAnagram" 기능 마무리

거짓을 반환하지 않고 제2의 Str을 통해 반복을 마치면 제1의 Str에는 제2의 Str에 있는 모든 값이 들어 있다는 뜻이다. 따라서 우리는 "for" 루프 이외의 "true"를 반환합니다.

```js
function isAnagram(firstStr, secondStr) {
  if (!firstStr || !secondStr) return false;
  if (firstStr.length !== secondStr.length) return false;

  const lookup = {};

  for (first of firstStr) {
    lookup[first] ? (lookup[first] += 1) : (lookup[first] = 1);
  }

  for (second of secondStr) {
    if (!lookup[second]) return false;
    lookup[second] -= 1;
  }
  return true;
}
```

## 요약에서

주파수 카운터 패턴에 대한 이 심층적인 개요가 도움이 되었기를 바랍니다. 패턴이 어떻게 돌아가는지 알게 되었으니, 저는 여러분이 훨씬 더 높은 수준에서 여러분의 실력을 보여주면서 면접관에게 깊은 인상을 줄 수 있을 것이라고 확신합니다.

다음 기사에서, 저는 슬라이딩 윈도우라고 불리는 또 다른 일반적인 문제 해결 패턴에 대해 토론할 것입니다. 읽어줘서 고맙고, 인터뷰도 행복해요!