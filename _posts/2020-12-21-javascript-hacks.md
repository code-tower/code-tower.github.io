---
layout: post
title: "모든 웹 개발자가 알아야 할 10가지 JavaScript 해킹"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1562615202-0b3035d14b6f?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDl8fHNwYW5uZXJ8ZW58MHx8fA&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


이러한 해킹으로 JavaScript 코드를 최적화하면 더 깨끗한 코드를 작성하고 리소스를 절약하며 프로그래밍 시간을 최적화할 수 있습니다.

RedMonk에 따르면 자바스크립트가 가장 인기 있는 프로그래밍 언어라고 한다. 게다가, 슬래시데이터는 약 1240만 명의 개발자들이 커피스크립트와 마이크로소프트의 타이프스크립트를 포함하는 자바스크립트를 사용하는 것으로 추정하고 있다.

이는 수백만의 사람들이 자바스크립트를 사용하여 프로그래머로 일하거나 업워크나 프리랜서 같은 사이트를 통해 프리랜서 긱을 하거나 심지어 웹 개발 사업을 시작하기도 한다는 것을 의미한다.

freeCodeCamp는 자바스크립트에 관한 훌륭한 기초 과정을 가지고 있다. 기본 사항에 대해 이미 잘 알고 있고 JavaScript에 대한 숙련도를 높이려면 다음 10가지 해킹을 학습하여 워크플로우에 통합해야 합니다.

## 1. 조건부로 바로 가기를 사용하는 방법

JavaScript를 사용하면 특정 바로 가기를 사용하여 코드를 쉽게 볼 수 있습니다. 일부 간단한 경우에는 논리 연산자를 사용할 수 있습니다.

`를 보자.

예제 조각:

```undefined
// instead of
if (accessible) {
  console.log("It’s open!");
}

// use
accessible && console.log("It’s open!");
```

|| 연산자는 "or" 절의 역할을 한다. 이제 이 연산자를 사용하면 응용 프로그램의 실행을 방지할 수 있기 때문에 좀 더 까다롭습니다. 하지만, 우리는 그것을 피하기 위한 조건을 추가할 수 있습니다.

예제 조각:

```undefined
// instead of
if (price.data) {
  return price.data;
} else {
  return 'Getting the price’';
}

// use
return (price.data || 'Getting the price');
```

## 2. ~~ 연산자를 사용하여 가장 큰 정수로 변환하는 방법

함수에서 주어진 숫자보다 작거나 같은 가장 큰 정수를 반환하기 위해 "Math.floor"를 사용하는 것은 꽤 긴 문자열일 뿐만 아니라 자원을 필요로 한다. 보다 효율적인 방법은 "~~" 연산자를 사용하는 것입니다.

예는 다음과 같습니다.

```undefined
// instead of
Math.floor(Math.random() * 50);

// use
~~(Math.random() * 50);

// You can also use the ~~ operator to convert anything into a number value.
// Example snippet:
~~('whitedress') // returns 0
~~(NaN) // returns 0
```

## 3. array.length를 사용하여 배열 크기 조정 또는 비우기

때로는 배열 크기를 조정하거나 비워 두어야 합니다. 가장 효율적인 방법은 Array.length를 사용하는 것이다.

예제 조각:

```undefined
let array = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'];

console.log(array.length); // returns the length as 10

array.length = 4;

console.log(array.length); // returns the length as 4
console.log(array); // returns ['a', 'b', 'c', 'd']
```

`Array.length`를 사용하여 지정된 배열에서 모든 값을 제거할 수도 있습니다.

예제 조각:

```undefined
let array = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'];

array.length = 0;

console.log(array.length); // returns the length as 0
console.log(array); // returns []
```

## 4. 서버 과부하를 유발하지 않고 어레이를 병합하는 방법

특히 대용량 데이터 세트를 처리하는 경우 어레이를 병합할 때 서버에 심각한 부담이 될 수 있습니다. 단순성을 유지하고 성능 수준을 유지하려면 Array.concat() 및 Array.push.apply(ar1, arr2) 기능을 사용합니다.

이러한 기능 중 하나를 사용하는 것은 배열 크기에 따라 다릅니다.

소규모 어레이를 처리하는 방법을 살펴보겠습니다.

예제 조각:

```undefined
let list1 = ['a', 'b', 'c', 'd', 'e'];
let list2 = ['f', 'g', 'h', 'i', 'j'];

console.log(list1.concat(list2)); // returns the merged values of both arrays, ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
```

대용량 데이터 세트에 `Array.concat()` 기능을 사용하면 새 어레이를 생성하는 동안 많은 메모리가 사용됩니다. 성능 저하를 방지하려면 새 어레이를 만들지 않고 두 번째 어레이를 첫 번째 어레이로 통합하는 Array.push.apply(ar1,ar2)를 사용하십시오.

예제 조각:

```undefined
let list1 = ['a', 'b', 'c', 'd', 'e'];
let list2 = ['f', 'g', 'h', 'i', 'j'];

console.log(list1.push.apply(list1, list2)); // returns 10, the new length of list1
console.log(list1); // returns ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
```

## 5. 필터와 어레이를 함께 사용하는 방법

배열 필터링은 해당 데이터의 여러 열을 사용할 때 유용합니다. 이 경우 배열의 그룹을 설명하는 특성을 기준으로 데이터를 포함하거나 제외할 수 있습니다.

배열을 필터링하려면 `filter()` 함수를 사용합니다.

예제 조각:

```undefined
const cars = [
  { make: 'Opel', class: 'Regular' },
  { make: 'Bugatti', class: 'Supercar' },
  { make: 'Ferrari', class: 'Supercar' },
  { make: 'Ford', class: 'Regular' },
  { make: 'Honda', class: 'Regular' },
]
const supercar = cars.filter(car => car.class === 'Supercar');
console.table(supercar); // returns the supercar class data in a table format
```

필터()를 `부울`과 함께 사용하여 배열에서 모든 `null` 또는 `정의되지 않은` 값을 제거할 수도 있습니다.

예제 조각:

```undefined
const cars = [
  { make: 'Opel', class: 'Regular' },
  null,
  undefined
]

cars.filter(Boolean); // returns [{ make: 'Opel', class: 'Regular' }] 
```

## 6. 고유한 값을 추출하는 방법

반복 값의 데이터 집합이 있고 이 집합에서 고유한 값을 생성해야 한다고 가정합니다. 스프레드 구문 `...`을(를) 사용하여 이 작업을 수행할 수 있습니다.및 개체 유형 `Set`입니다. 이 접근 방식은 단어와 숫자 모두에서 작동합니다.

예제 조각:

```undefined
const cars = ['Opel', 'Bugatti', 'Opel', 'Ferrari', 'Ferrari', 'Opel'];
const unrepeated_cars = [...new Set(cars)];

console.log(unrepeated_cars); // returns the values Opel, Bugatti, Ferrari
```

## 7. 교체 기능 바로 가기 사용 방법

String.replace() 기능을 숙지해야 합니다. 그러나 문자열은 지정된 줄로 한 번만 대체되고 여기서 멈춥니다. 데이터 세트가 더 크고 이 함수를 여러 번 입력해야 한다고 가정합니다. 시간이 좀 지나면 답답해져요.

생활을 편리하게 하기 위해 정규식 끝에 `/g`를 추가할 수 있으므로 첫 번째 조건에서는 중지하지 않고 모든 일치 조건이 실행 및 대체한다.

예제 조각:

```undefined
const grammar = 'synonym synonym';

console.log(grammar.replace(/syno/, 'anto')); // this returns 'antonym synonym'
console.log(grammar.replace(/syno/g, 'anto')); // this returns 'antonym antonym'
```

## 8. 값을 캐시하는 방법

대규모 어레이를 사용하는 경우 `getElementById()를 사용하여 ID별로 요소를 요청하거나 `getElementByClassName()을 사용하여 클래스 이름별로 요청해야 하는 경우 JavaScript는 각 유사한 요소 요청이 있는 루프의 어레이를 통해 실행됩니다. 이 작업은 많은 자원을 소모할 수 있습니다.

그러나 지정된 선택을 정기적으로 사용하는 경우에는 값을 캐슁하여 성능을 향상시킬 수 있습니다.

예제 조각:

```undefined
const carSerial = serials.getElementById('serial1234');
carSerial.addClass('cached-serial1234');
```

## 9. 객체에 값이 있는지 확인하는 방법

여러 개체를 사용하는 경우 실제 값이 포함된 개체와 삭제할 수 있는 개체를 추적하기가 어렵습니다.

다음은 개체가 비어 있거나 `Object.keys()` 함수가 있는 값이 있는지 확인하는 간단한 해킹 방법입니다.

예제 조각:

```undefined
Object.keys(objectName).length // if it returns 0 then the Object is empty, otherwise it displays the number of values
```

## 10. JavaScript 파일을 최소화하는 방법

큰 JS 파일은 페이지의 로드 및 응답 성능에 영향을 미칩니다. 코드를 작성하는 동안 불필요한 줄, 주석 및 비활성 코드가 표시될 수 있습니다. 파일 크기에 따라 파일이 쌓이고 중복 병목 현상이 발생할 수 있습니다.

개발자의 관점에서 코드를 정리하고 JS 파일을 가볍게 하거나 축소하는 데 도움이 되는 몇 가지 도구가 있습니다. JS 파일을 축소하는 것은 해커가 아니지만 개발자가 알고 구현하는 것이 여전히 유용합니다.

하나는 Google Closure Compiler입니다. 이 컴파일러는 JavaScript를 구문 분석하고, 데드코드를 제거하고, 남은 내용을 다시 쓰고 최소화합니다. 다른 하나는 Microsoft Ajax Minifier로, JavaScript 파일의 크기를 줄임으로써 웹 응용 프로그램의 성능을 향상시킬 수 있습니다.

바로 그겁니다. 이 10개의 해킹을 사용하여 코드를 더 깔끔하게 만들고, 서버 리소스를 절약하고, 프로그래밍 시간을 유지합니다.

### 읽어주셔서 감사합니다!

저는 디지털 마케팅, 웹 개발, 사이버 보안에 열정적인 작가입니다. 링크드인으로 연락하시면 됩니다.

제가 쓴 다른 기사들도 보실 수 있습니다.

- Google 페이지 환경: 2021년 대비해야 할 사항 및 5단계
- 이번 시즌 동안 주의해야 할 웹 호스팅 보안 위협
- 2020년 연휴 나머지 기간 동안 매출 증대 방법