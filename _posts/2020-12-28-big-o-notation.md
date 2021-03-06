---
layout: post
title: "큰 O 표기법의 작동 방식 – 케이크와 함께 설명"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1464349095431-e9a21285b5f3?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDEyfHxjYWtlfGVufDB8fHw&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


빅 오 표기법은 알고리즘의 상한을 정의하기 위해 컴퓨터 공학에서 사용된다. 알고리즘의 최대 시간을 입력 크기의 함수로 정의하는 데 주로 사용되지만 메모리 사용량을 정의하는 데도 사용할 수 있다.

이 기사에서는 생일 케이크를 사용하여 개념을 설명하는 가장 일반적인 유형의 `빅 오` 표기법을 살펴보겠습니다. 우리는 파티를 여는 척 할 것이고, 얼마나 많은 사람들이 참석하느냐에 따라 얼마나 많은 케이크를 구울지 결정해야 한다.

## O(1) - 상수 시간

Constant Time 예제의 경우, 생일 파티에 얼마나 많은 사람이 와도 케이크 한 개만 만들 수 있습니다. 그래서 케이크를 만드는 시간은 일정하게 유지됩니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/o-1--constant-time.png)

빅 오 표기법은 상수 시간(케이크 만드는 데 1시간, 4시간)이 걸릴 수 있다는 것을 명시하지 않습니다. 단지 손님의 수에 따라 소요 시간이 늘어나지 않는다고 명시되어 있을 뿐이다.

O(1) 작업의 실제 예는 인덱스로 어레이에 액세스하는 것입니다. 100만 개의 항목 배열에서 요소를 검색하는 것만큼 10개의 항목 배열에서 요소를 검색하는 것도 빠릅니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/o-1--constant-time-grqph.png)

## O(log n) - 로그 시간

로그 타임 예제의 경우 생일 케이크는 사람들이 파티에 제시간에 오도록 유도하는 방법으로 사용됩니다.

제일 먼저 도착한 사람은 케이크를 혼자 챙긴다. 그리고 나서 도착한 다음 두 사람은 케이크를 나눠 먹습니다. 그다음에 4명이서 케익 나눠먹기 등등.

그래서 1인 파티는 케이크 1개가 필요하다. 2인 파티나 3인 파티는 케이크 2개가 필요합니다. 4~7인 파티는 케이크 3개, 8~15인 파티는 케이크 4개가 필요합니다. 일반적으로 `n`인 파티에는 로그 2(n) 케이크가 필요합니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/o-log-n--logarithmic-time.png)

O(log n) 작업의 가장 일반적인 실제 예는 순서 배열의 이진 검색입니다.

이 알고리즘은 배열의 중간을 보고 값이 찾고 있는 값보다 낮거나 높은지 확인합니다. 목록이 정렬되므로 대상 값이 배열의 절반에 속하는지 알 수 있습니다.

그런 다음 배열의 절반을 사용하여 프로세스를 반복합니다. 따라서 16개 항목 배열의 경우, 첫 번째 반복은 검색을 8개 항목으로 좁히고, 그 다음 4개 항목, 2개 항목, 또는 로그 2(16)를 차례로 좁힙니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/o-log-n--logarithmic-time-graph.png)

## O(n) - 선형 시간

Linear Time(선형 시간) 예제의 경우 각 게스트가 직접 케이크를 얻습니다. 파티에 `n` 사람이 오면 `n` 케이크를 만들어야 해요. 그래서 걸리는 시간은 손님의 수와 관련이 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/o-n--linear-time.png)

빅 오 표기법은 시간이 얼마나 걸리는지 명시하지 않고(케이크 만드는 데 1시간, 4시간 정도 소요), 손님 수에 따라 시간이 선형적으로 증가한다고 명시한다.

O(n) 작업의 실제 예는 배열의 항목을 단순하게 검색하는 것입니다. 10개 항목 배열에서는 최악의 경우 원하는 항목을 찾으려면 10개 항목을 모두 찾아야 합니다. 하지만 100만 개의 아이템 배열을 위해서는 100만 개의 아이템을 모두 보아야 할 수도 있습니다.

물론 솔루션을 더 빨리 찾을 수도 있지만 빅 O 표기법은 알고리즘에 소요되는 최대 시간을 지정합니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/o-n--linear-time-graph.png)

## O(n^2) - 2차 시간

2차 시간 예제의 경우 각 게스트는 고유한 케이크를 얻습니다. 게다가, 각각의 케이크에는 맛있는 아이싱과 함께 모든 손님들의 이름이 적혀있다.

이 경우 1인 파티는 하나의 이름이 적힌 케이크를 가지고 있습니다. 2인 파티는 2개의 케이크, 2인 파티는 2개의 이름이 적힌 케이크(총 4개의 이름)와 3인 파티는 3개의 케이크, 모두 3개의 이름이 적힌 케이크(총 9개의 이름)가 있다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/o-n-2--quadratic-time.png)

일반적으로 `n`인 파티는 n*n 이름(n 제곱 또는 2의 힘으로 n)을 써야 하므로 케이크를 만드는 속도(그리고 모든 이름을 쓰는 속도)는 손님의 수의 제곱과 관련이 있다.

O(n^2) 연산의 실제 예는 배열에서 중복을 찾는 순진한 검색이다. 이 시나리오에서는 배열의 모든 항목을 반복하고 각 항목에 대해 배열을 다시 순환하여 일치하는 항목이 있는지 확인합니다.

10개의 항목 배열의 경우, 외부 루프는 10개의 반복을 가지며, 각 반복에는 총 100개의 반복이 10개 있다. 100만 개의 아이템 배열의 경우 1000억 개입니다.

O(n^2)의 보다 일반적인 경우가 있는데, 이때 시간은 2(n^2)의 검정력에 상대적인 대신 c(n^c)의 검정력에 상대적이다. 이것을 보통 다항식 시간이라고 한다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/o-n-2--quadratic-time-graph.png)

## O(n!) - 요인 시간

요인 시간 예제의 경우, 게스트는 페탄크 대회에 참가하고 우승자는 케이크를 집으로 가져갑니다.

그러나 첫 번째 턴을 하는 선수가 불리하다는 점에서 약간의 문제가 있다. 평준화를 돕기 위해, 많은 게임들이 행해지고, 그래서 손님들의 각 순열은 커버되고 모든 사람들이 먼저 할 수 있게 된다. 이 모든 순열들은 케익에 쓰여졌고, 다시 약간의 맛있는 아이싱과 함께 쓰여졌다.

2인 파티는 손님 한 명이 번갈아 가며 먼저 가기 때문에 두 게임을 한다는 뜻이다. 3인 파티에는 6개의 게임이 있습니다(손님이 Anna, Brian, Chris라고 가정하면 순열은 ABC, ACB, BAC, BCA, CAB, CBA).

![image](https://www.freecodecamp.org/news/content/images/2020/12/o-n---factorial-time.png)

일반적으로 `n`인물 파티에는 n! 또는 n개의 요인 게임이 필요하므로 케이크를 만드는 속도는 이와 관련이 있습니다.

n!은 모든 숫자를 n * (n - 1) * (n - 2) … * 2 * 1"로 곱하여 계산합니다. 그래서 2인 파티는 2 * 1 또는 2입니다. 3인 파티의 경우 3 * 2 * 1이고, 6입니다.

O(n!) 운영의 실제 예는 출장 중인 세일즈맨 문제와 같이 순열 목록을 분석해야 하는 모든 것입니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-165.png)

## 결론들

바라건대 생일 케이크가 `빅 오` 표기법을 소화하기 쉽게 만들어 주었기를 바랍니다! 아래 그래프도 알고리즘의 상대적 속도를 보여주는 좋은 메모리 보조 도구입니다(선택 사항이 있는 경우 더 빠른 것을 원함).

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-166.png)

O(nlog n)와 O(c^n)와 같은 다른 `Big O` 표기법이 꽤 있지만 모두 동일한 패턴을 따릅니다. 만약 그것에 대해 더 알고 싶다면, 이 기사를 확인해 보세요.