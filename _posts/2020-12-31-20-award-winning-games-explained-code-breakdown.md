---
layout: post
title: "20개의 수상 경력에 빛나는 13킬로바이트 자바스크립트 게임 브라우저에서 플레이할 수 있는 게임 – js13k 2020 수상자"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/js13kgames.png
tags: undefined
---


이 기사에서는 JS13kGames 대회에서 상을 받은 20개의 JavaScript 게임을 보여드리겠습니다. 다시 말해서, 여러분은 20명의 미친 재능 있는 개발자들이 만든 20개의 훌륭한 코드 예들을 보게 될 것입니다.

JS13kGames 대회에 대해 들어본 적이 없다면, 한턱 내세요.

작년 경기의 심판 중 한 명으로서, 나는 내가 본 일의 기준에 완전히 매료되었다. 이러한 개발자들이 13KB의 작은 zip 파일에 적합한 JavaScript를 사용하여 무엇을 구축했는지 정말 놀랍습니다.

## 하지만 먼저, Js13k게임이 무엇인지 물어보면 어떨까요?

Js13kGames는 게임 개발을 시도하고자 하는 모든 사람과 누구에게나 열려 있는 자바스크립트 코딩 대회이다.

게임 개발업계에 직접 있는 개발자가 아닌 개발자의 수준 높은 플레이 필드를 만드는 자바스크립트 사용으로 제한하기 때문에 개인적으로 마음에 듭니다. 많은 웹 개발자들도 참가한다.

이름에서 알 수 있듯이, 모든 코드 및 게임 자산은 13,312바이트(13 x 1024이므로 13,312바이트)보다 작거나 같아야 합니다.

즉, zip 패키지 작성을 지나치게 복잡하게 해서는 안 됩니다. 언제 어디서나 문제 없이 모든 플랫폼에서 짐을 풀어야 합니다. 물론 도움이 되는 경우 JavaScript 소스 코드를 최소화하는 도구를 사용할 수 있습니다.

그 경기는 항상 밝은 쪽으로 진행되도록 되어 있다. 하지만 모든 사람들의 삶을 좀 더 쉽게 만들고 항목들을 좀 더 표준화하기 위해, 여러분이 지켜야 할 몇 가지 규칙이 있습니다. 이러한 규칙은 Js13kGames 웹 사이트에서 가져오며 여기서 전체 집합을 볼 수 있습니다. 지금 살펴보도록 하죠.

## 외부 서비스 또는 라이브러리를 사용할 수 없습니다.

모든 유형의 데이터를 제공하는 서버 또는 서비스에서 호스트되는 라이브러리, 이미지 또는 데이터 파일을 사용할 수 없습니다.

예를 들어 Google 글꼴은 허용되지 않습니다. 그러나 일부 문자 또는 이모티콘을 제대로 표시할 수 없는 장치에서 지원하기 위해 웹 글꼴을 라이브로 로드하도록 사용자에게 요청할 수 있습니다. 여러분은 그것들 없이도 여러분의 게임이 잘 될 수 있도록 해야 합니다.

분석 및 기타 상태 수집 스크립트도 허용되지 않습니다.

모든 게임 자산은 패키지 크기 제한에 적합해야 한다(A-Frame, Babylon.js 및 Three.js 프레임워크는 크기 제한에 반영되지 않지만 WebXR 범주에서만 사용할 수 있다).

좋아하는 라이브러리를 코드 자체를 포함하여 13KB 미만으로 축소할 수 있다면 원하는 대로 사용할 수 있습니다. 13kB 제한만 기억하십시오.

그리고 현실을 직시하자 – 때때로 개발자들이 npm 라이브러리를 스크롤하면서 그들의 문제에 대한 최신의 지름길을 찾으려고 애쓰는 것에 휘말릴 수 있는 세상에서, 그것을 다시 기본으로 되돌리는 것은 좋은 일이다.

## 너는 그 주제를 고수해야 한다.

대회의 주요 테마는 매년 8월경에 발표된다. 심판들이 주의할 것이기 때문에, 저는 여러분이 게임에서 주제를 따르는 것을 강력히 권고합니다.

하지만 여러분은 여러분이 가장 좋다고 느끼는 대로 주제를 자유롭게 해석하고 실행할 수 있습니다. 2020년도의 테마는 모두 404번이었다.

## 오류 및 브라우저 지원 관리

게임은 최신 Firefox와 Chrome의 두 개 이상의 브라우저에서 작동하고 재생 가능해야 합니다. 그러나 지원되는 브라우저가 많을수록 좋습니다.

오류도 없어야 합니다. 게임에서 콘솔에 오류가 있으면 일부 점수를 잃을 수 있습니다. 만약 우리가 당신의 게임을 할 수 없다면, 그것은 받아들여지지 않을 것입니다.

## 몇 개의 게임을 제출할 수 있습니까?

원하는 만큼 게임을 제출할 수 있습니다! 친구, 친구, 반려견과 함께 제출할 수 있습니다. 매우 유연하며 누구나 참여할 수 있습니다:)

이 멋진 대회는 2012년 안드르제즈 마수르가 여가 시간에 만들었다. Andzej는 자신의 저축한 돈을 참가자들을 위해 티셔츠를 인쇄하기 위해 사용했고, 상품을 보냈고, 본질적으로 모든 것을 스스로 운영했습니다.

올해로 8회째를 맞은 이 대회는 전 세계에서 출품된 대회로 세계적인 인정을 받고 있다.

오늘 동영상을 통해 귀하와 귀하의 의견을 공유할 수 있게 되어 매우 영광입니다.

## 2020 Js13k 게임 수상자와 코드 작성에 대한 자부심이 가장 큽니다.

저는 이 비디오를 FreeCode Camp용으로 만들었습니다. 트위터나 인스타그램, 유튜브에서 저를 팔로우하시면 더 많은 콘텐츠를 보실 수 있습니다.

## 수상자 전체 목록과 수상자의 게임 및 코드를 찾을 수 있는 위치:

### 1위

레미 반스틸란트의 닌자 vs EVILCORP

- GitHubrepo: https://github.com/remvst/ninja
- 트위터: https://twitter.com/remvst

### 2위

톰 허먼스가 찾을 수 없는 에지

- GitHubrepo: https://github.com/Auroriax/js13k-2020
- 트위터: https://twitter.com/auroriax

### 3위

코스티크1337번 CHOCHOCH

- GitHubrepo: https://github.com/kostik1337/CHOCH
- 트위터: https://twitter.com/kostik13337

### 4위

트랙을 찾을 수 없다?! 괘로

- GitHubrepo: https://github.com/xem/track-not-found
- 트위터: https://twitter.com/maximeeuziere

### 5위

이안 차오가 훔친 검

- GitHubrepo: https://github.com/chiaogu/stolen-sword
- 트위터: https://twitter.com/chiaogu

### 6위

마이클 페론의 마지막 스파르타인

- GitHubrepo: https://github.com/ferronsays/js13k-TheLastSpartan
- 트위터: https://twitter.com/ferronsays

### 7위

포폴드 바이 사우드

- GitHubrepo: https://github.com/rottencandy/js13k2020
- 트위터: https://twitter.com/rotttencandy

### 8위

마크 바실코프가 만든 게임을 구글로 검색해보고 싶다.

- GitHubrepo: https://github.com/mvasilkov/js13k2020
- 트위터: https://twitter.com/mvasilkov

### 9위

제롬 레콤테로404번길

- GitHubrepo: https://github.com/herebefrogs/highway-404
- 트위터: https://twitter.com/herebefrogs

### 10위

코디 에버슨의 미니펑크

- GitHubrepo: https://github.com/codyebberson/js13k-minipunk
- 트위터: https://twitter.com/codyebberson

### 11위

니클라스 뢰프 / 스누키의 04 찾기

- GitHubrepo: https://github.com/nicklaslof/searching/
- 트위터: https://twitter.com/nicklaslof

### 12위

조니 스미터 3세 by 폴 브런트

- GitHubrepo: https://github.com/supereggbert/JohnnySmiterIII
- 트위터: https://twitter.com/super_eggbert

### 13위

벤이 찾지 못한 섬

- GitHubrepo: https://github.com/SalvatorePreviti/js13k-2020
- 트위터: https://twitter.com/SN74HC00

### 14위

당신은 마크 놀에 의해 발견되었습니다.

- GitHubrepo: https://github.com/markknol/js13k-2020
- 트위터: https://twitter.com/mknol

### 15위

404kph by 자번

- GitHubrepo: https://github.com/jaburns/js13k2020
- 트위터: https://twitter.com/jaburnsnet

### 16위

엘리엇 넬슨의 산탄총을 든 마법사

- GitHubrepo: https://github.com/elliot-nelson/js13k-2020-wizard-with-a-shotgun
- 트위터: https://twitter.com/7tonshark

### 17위

페데리코 티발도의 연결

- GitHubrepo: https://github.com/fedetibaldo/connection-js13kgames2020
- 트위터: https://twitter.com/fedetibaldo

### 18위

소주즈 404 by 마쿠스 피쉬

- GitHubrepo: https://github.com/markusfisch/Sojuz404
- 트위터: https://twitter.com/markusfisch

### 19위

시르시믹에 의해 대칭이 발견되지 않음

- GitHubrepo: https://github.com/sirxemic/js13k-entry-2020
- 트위터: https://twitter.com/sirxemic

### 20위

노트 크래프트 바이 킬드 바이APIXel

- GitHubrepo: https://github.com/KilledByAPixel/NoteCraft
- 트위터: https://twitter.com/KilledByAPixel