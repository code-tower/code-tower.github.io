---
layout: post
title: "개발 생산성을 높일 수 있는 VS 코드 확장 기능"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/vscode.jpg
tags: undefined
---


워크플로우에 적합한 텍스트 또는 코드 편집기를 갖추는 것은 개발자로서 생산성을 높이는 데 매우 중요합니다. VSCode는 기본적으로 많은 기능이 제공되지만, 여기에 워크플로를 한 단계 더 끌어올리는 데 도움이 되는 7가지 확장 기능이 있습니다.

- VS Code란?
- VS 코드 확장
- 하위 텍스트 키맵 및 설정 임포터
- 가져오기 비용
- 들여쓰기의
- 레인보우 브래킷
- 설정 동기화
- 프로필 전환기
- 더 나은 의견
- 복제 작업

## VS Code란?

잘 모르실 경우를 위한 간단한 메모입니다. 비주얼 스튜디오 코드의 줄임말인 VS Code는 마이크로소프트 팀이 관리하는 인기 있는 텍스트 또는 코드 편집기이다.

지난 1, 2년 동안 개발자 시장의 엄청난 점유율이 성장하여 웹 개발자들을 위한 편집자로 자리 잡았습니다.

마이크로소프트가 그것에 많은 시간을 투자하고 있고 독립 개발자들이 엄청난 확장을 하고 있다는 사실과 함께, 당신은 그것을 시도해 보는 것을 잘못할 수 없다.

## VS 코드 확장

VSCode를 훌륭하게 만드는 이유 중 하나는 확장성입니다. 개발자는 Microsoft가 지원하지 않는 기능을 구현하거나 Foam을 사용하여 전체 노트 작성 경험을 구축함으로써 편집기를 다른 수준으로 창의적으로 전환할 수 있습니다.

VS Code Marketplace에는 수천 개의 확장 기능을 사용할 수 있지만, 이러한 7가지 확장 기능은 현재 개발자로서 워크플로우에 매우 중요합니다.

## 하위 텍스트 키맵 및 설정 임포터

VS Code로 옮기기 전에는 Sublime Text 3 사용자였습니다. 여전히 훌륭한 텍스트 편집기이지만 VS 코드로 이동할 때 많은 바로 가기와 키 매핑이 동일하지 않았습니다.

Sublimate Text Keymap 및 Settings Importer를 사용하면 먼저 Sublimate 텍스트에서 내 설정을 가져올 수 있지만 기본 키 매핑도 설정할 수 있습니다. 이를 통해 서브라임에서 사용할 수 있는 바로 가기를 VS 코드에서 즉시 사용할 수 있게 되었습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/vscode-sublime-keyboard-shortcuts.gif)

여기에는 다중 선택(Something을 선택한 다음 CMDB+D / Ctrl+D를 누름) 및 라인 복제(라인에 커서 추가 및 CMDB+Shift+D / Ctrl+D를 누름)와 같은 두 가지 즐겨찾기가 포함됩니다.

서브라임 텍스트 키맵 및 설정 임포터(marketplace.visualstudio.com)

## 가져오기 비용

오늘날의 개발자들은 다양한 출처에서 오는 의존성을 끊임없이 다루어야 한다. 프로젝트를 구축하기 위해 여러 가지 코드를 조합할 때, 추가 코드는 비용이 듭니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/vscode-import-cost.jpg)

Import Cost는 프로젝트 크기에 얼마만큼의 가중치를 더할지 확인할 수 있도록 가져오기 크기에 대한 추정치를 계산합니다.

이를 통해 종속성의 크기를 인식하여 성능에 영향을 미치고 고객의 사용자 경험을 해칠 수 있는 대형 라이브러리의 우발적인 과부하를 방지할 수 있습니다.

가져오기 비용(marketplace.visualstudio.com)

## 들여쓰기의

스타일은 코드를 판독할 수 있게 하는 중요한 요소입니다. 이러한 스타일의 일부는 코드를 들여쓰는 방법이기 때문에 서로 다른 코드 블록의 중첩을 이해합니다.

문제는 때때로 중첩이 상당히 커질 수 있으며 어떤 개구부 태그가 어떤 닫힘 태그에 속하는지 찾기 어려울 수 있다는 것이다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/vscode-indent-rainbow.jpg)

들여쓰기 기능은 들여쓰기 공간에 색상을 추가하여 쉽게 줄을 서서 서로 소속된 태그를 확인할 수 있도록 합니다.

들여쓰기(marketplace.visualstudio.com)

## 레인보우 브래킷

들여쓰기 코드와 마찬가지로 복잡한 코드, 특히 수학을 사용할 때 같은 문에서 괄호를 여러 번 사용할 경우 쉽게 혼동할 수 있습니다.

예를 들어 간단한 계산을 적용하려는 경우:

```undefined
const value = (((1+1)*2)+1)*2;

```

간단한 예이긴 하지만, 쉽게 통제하기 어렵고 추적하기도 어렵습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/vscode-rainbow-brackets.jpg)

레인보우 브래킷은 다른 색상으로 괄호를 강조 표시하여 어떤 오프닝 브래킷이 방정식의 어느 클로징 브래킷에 속하는지 더 잘 알 수 있도록 합니다.

레인보우 브래킷(marketplace.visualstudio.com)

## 설정 동기화

일반적으로 랩톱 두 대 또는 서로 다른 두 환경에서 작업하는 경우 설치에 까다로운 경우 텍스트 편집기를 수동으로 동일하게 유지해야 할 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/vscode-settings-sync.jpg)

설정 동기화를 통해 VS 코드 설정을 GitHub Gist에 저장할 수 있습니다. 이를 통해 여러 VS 코드 설치 간에 이러한 설정을 동기화할 수 있습니다.

설정 동기화(marketplace.visualstudio.com)

참고: 만약 여러분이 더 배우고 싶다면, 저는 이 단계를 단계별로 설정하는 과정을 안내하는 튜토리얼을 썼습니다!

## 프로필 전환기

콘텐츠 제작자로서, 저는 제 화면을 다른 사람들에게 보여줄 때, 사람들이 제가 데모하는 것을 쉽게 볼 수 있도록 접근 가능한 색과 글꼴 크기를 사용할 수 있도록 해야 합니다.

문제는 이러한 설정이 제가 헤드다운 코딩을 할 때 일상적으로 사용하는 설정이 아니라는 것입니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/vscode-profile-switcher.jpg)

Profile Switcher를 사용하면 여러 VS 코드 프로파일을 각각 고유한 구성으로 설정하여 서로 다른 설정 간에 쉽게 전환할 수 있습니다.

프로파일 스위처(marketplace.visualstudio.com)

## 더 나은 의견

코드를 쓸 때는 중요하지 않은 것처럼 보일 수 있지만, 코멘트는 다른 사람이 코드를 이해하는 데 중요한 역할을 합니다. 그것들은 또한 여러분이 일년 후에 그것을 볼 때 그것을 이해하는데 도움을 줍니다.

이러한 댓글은 유용하지만, 일반적으로 모두 회색이기 때문에 반드시 눈에 띄지 않습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/vscode-better-comments.jpg)

바로 여기서 Better Comments(더 나은 의견)가 제공되고, 코드에 강조표시되는 일종의 구문이 추가되며, 코드 주석의 가독성에 도움이 되는 키워드 및 문에 색상이 추가됩니다.

더 나은 의견(marketplace.visualstudio.com)

## 복제 작업

이 마지막 항목은 작은 것으로 보이지만, 어떤 이유에서인지 VSCode는 파일을 마우스 오른쪽 버튼으로 클릭하고 기본적으로 복제하는 기능을 제공하지 않습니다.

코드에서 헤드다운할 때 일반적으로 기존 템플리트와 같은 파일을 복제하여 내용만 변경할 수 있습니다. 이렇게 하면 새 페이지를 보다 생산적으로 만들 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/vscode-duplicate-action.jpg)

복제 작업은 파일이나 폴더를 마우스 오른쪽 단추로 클릭하면 상황에 맞는 메뉴에 파일 또는 폴더 복제 옵션을 추가합니다.

복제 작업(marketplace.visualstudio.com)

## 가장 좋아하는 내선번호는 무엇입니까?

놀라운 일을 할 수 있는 수많은 확장 프로그램이 있습니다. 가장 좋아하는 것은 무엇입니까? 트위터로 공유해서 알려줘!