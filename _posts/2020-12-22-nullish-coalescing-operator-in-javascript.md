---
layout: post
title: "Nullish 병합 연산자의 JavaScript 작동 방식"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/nullish-2.jpeg
tags: undefined
---


ES11은 다음과 같이 이중 물음표로 표시된 무효화 결합 연산자를 추가했다.`.

이 기사에서는 이것이 왜 그렇게 유용한지, 그리고 어떻게 사용하는지에 대해 알아보겠습니다.

시작합시다.

## 배경 정보

JavaScript에는 단락 논리적 OR 연산자 `||가 있다.

> || 연산자는 첫 번째 'truthy' 값을 반환합니다.

다음은 자바스크립트에서 `falsy` 값으로 간주되는 `단 6` 값이다.

- 거짓의
- 정의되지 않은
- 무효의
- ""(빈 문자열)
- NaN
- 0

따라서 위의 목록에 없는 것이 있다면, 그것은 `진실` 가치로 간주될 것이다.

Truthy와 Falsey 값은 true로 강제되는 부울이 아닌 값입니다.
또는 특정 작업을 수행할 때 `false`를 선택합니다.

```undefined
const value1 = 1;
const value2 = 23;

const result = value1 || value2; 

console.log(result); // 1
```

|| 연산자가 위의 코드에서 첫 번째 `truthy` 값을 반환함에 따라, `result`는 `value1` 즉 `1`에 저장된 값이 된다.

값 1이 null, 정의되지 않음, 비어 있음 또는 기타 잘못된 값이면 || 연산자 뒤의 다음 피연산자가 평가되어 전체 식의 결과가 된다.

```undefined
const value1 = 0;
const value2 = 23;
const value3 = "Hello";

const result = value1 || value2 || value3; 

console.log(result); // 23
```

여기서 value1은 0이므로 value2를 확인합니다. 이 값이 참 값이기 때문에 전체 식의 결과는 값 2가 됩니다.

> || 연산자의 문제는 그것이 거짓, 0, 빈 문자열, NaN, Null, 정의되지 않은 문자열들을 구분하지 않는다는 것이다. 이들은 모두 거짓된 가치로 간주된다.

이들 중 하나라도 ||의 첫 번째 피연산자라면, 우리는 그 결과로 두 번째 피연산자를 얻게 될 것이다.

## JavaScript에서 Nullish 병합 연산자가 필요한 이유

|| 연산자는 잘 작동하지만 때때로 첫 번째 피연산자가 `null` 또는 `정의되지 않은` 경우에만 다음 식을 평가하기를 원한다.

따라서 ES11은 null 병합 연산자를 추가했습니다.

x? 라는 표현으로? 네, 네,

- x가 null이거나 정의되지 않은 경우 결과만 y가 됩니다.
- x가 null 또는 정의되지 않은 x가 아닌 경우 결과는 x가 됩니다.

이렇게 하면 조건부 검사 및 디버깅 코드가 쉬운 작업이 됩니다.

## 직접 확인해 보십시오!

```undefined
let result = undefined ?? "Hello";
console.log(result); // Hello

result = null ?? true; 
console.log(result); // true

result = false ?? true;
console.log(result); // false

result = 45 ?? true; 
console.log(result); // 45

result = "" ?? true; 
console.log(result); // ""

result = NaN ?? true; 
console.log(result); // NaN

result = 4 > 5 ?? true; 
console.log(result); // false because 4 > 5 evaluates to false

result = 4 < 5 ?? true;
console.log(result); // true because 4 < 5 evaluates to true

result = [1, 2, 3] ?? true;
console.log(result); // [1, 2, 3]

```

위의 모든 사례에서 볼 때, 그 수술의 결과가 `x?? y는 x가 ➡ 또는 ➡일 때만 y이다.

다른 모든 경우 작업의 결과는 항상 `x`가 됩니다.

## 결론

보셨듯이 null 병합 연산자는 모든 변수에 대해 `null` 또는 `정의되지 않은` 값만 신경쓸 때 유용합니다.

ES6부터는 자바스크립트에 다음과 같은 유용한 추가사항이 많다.

- ES6 파괴
- 구문 가져오기 및 내보내기
- 화살표 함수
- 약속들
- 비동기/대기
- 선택적 체인 연산자

그리고 더 많은 것을.

모든 ES6+ 기능에 대한 자세한 내용은 Mastering Modern JavaScript 책을 참조하십시오.

마스터링 모던 자바스크립트 북은 40% 할인된 가격으로 구입하실 수 있습니다.

제 주간 뉴스레터를 구독하시면 1,000명 이상의 다른 가입자와 함께 여러분의 받은 편지함에 직접 놀라운 팁, 요령, 기사 및 할인 혜택을 받으실 수 있습니다.