---
layout: post
title: "React Scripts Start Command – Create-Ract-App NPM 스크립트 설명"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/cra-npm-scripts-explained.png
tags: undefined
---


대응 응용프로그램을 만들려면 Babel 및 Webpack과 같은 빌드 도구를 설정해야 합니다. React의 JSX 구문은 브라우저가 이해하지 못하는 언어이기 때문에 이러한 빌드 도구가 필요합니다.

React 애플리케이션을 실행하려면 JSX를 브라우저가 이해하는 일반 JavaScript로 전환해야 합니다.

CRA(Create React App)는 React 팀이 공식적으로 지원하는 단일 페이지 React 애플리케이션을 만드는 도구입니다.

이 스크립트는 대응 응용 프로그램을 시작하고 브라우저에서 실행하는 데 필요한 파일 및 폴더를 생성합니다. 이렇게 하면 빌드 구성에 구애받지 않고 응용 프로그램을 코딩하는 데 집중할 수 있습니다.

## 응용 프로그램을 만들고 반응하는 종속성

생성된 `패키지`에서 Babel 또는 Webpack이 종속성으로 나열되는 것을 볼 수는 없지만,Json의 파일인 CRA는 여전히 Babel과 Webpack을 후드 아래 사용한다. 단지 `react-scripts` 패키지 안에 구성이 숨겨져 있을 뿐입니다.

`패키지를 들여다보면요.json의 리액션 스크립트 파일은 리액션 작업에 필요한 모든 패키지를 브라우저에 볼 수 있습니다. 31호선부터 88호선까지 58개의 패키지가 있습니다.

정말 많은 소포네요! 이 패키지들이 무엇에 쓰이는지 이해하기 위해 그것을 조금 나누자.

이 문서는 Create React App 버전 4.0.1을 기준으로 작성되었습니다. 이 문서는 Create React App NPM 스크립트를 사용할 때 후드에서 수행되는 작업을 이해하는 데 도움이 됩니다.

### 바벨

Babel의 주요 목적은 이전 브라우저에서 코드를 읽을 수 있도록 하는 것입니다. ES 2015가 출시된 이후, 브라우저는 새로운 자바스크립트 API와 기능을 구현하기 위해 느리지만 꾸준한 진전을 보이고 있다.

Chrome 및 Safari와 같은 최신 브라우저는 새로운 JavaScript 버전을 지원할 수 있지만 JSX는 ES 버전에 속하지 않는 React 전용 기능입니다.

Babel은 최신 JavaScript 코드를 이전 버전으로 변환한 다음, 브라우저에 누락되었지만 앱에 필요한 기능을 구현하는 코드 조각인 폴리필을 추가합니다.

### ESLint

ESLint는 코드를 스캔하고 모든 코드 오류에 플래그를 지정하는 JavaScript 링터입니다. 오류가 있는 경우 라이브러리가 콘솔에서 경고를 표시합니다. VSCode와 같은 현대의 코드 편집기에서도 잘 작동한다.

### 농담

제스트는 리액트와 매우 잘 어울리는 페이스북의 테스트 라이브러리이다. Jest의 종속성을 사용하면 다른 테스트 라이브러리를 설치하지 않고도 응용 프로그램에 대한 테스트 스크립트를 작성할 수 있습니다.

### 포스트CSS

PostCSS는 CSS를 변환하기 위한 JavaScript 플러그인입니다. 포스트CSS 플러그인은 CSS, 지원 변수 및 혼합 구문, 향후 CSS 구문 등을 구성에 따라 전송할 수 있습니다.

### 웹팩

웹 팩은 애플리케이션에 필요한 모든 것을 통합하는 JavaScript용 모듈 번들러입니다. 또한 이 라이브러리는 코드 위에서 Babel, Jest, ESLint 및 PostCSS 실행과 같은 태스크를 실행할 수도 있습니다.

이제 의존성이 어떤 용도로 사용되는지 알 수 있게 되었으니, `react-scripts`가 실제로 어떤 역할을 하는지 계속해서 이해해보자.

## 대응 스크립트의 기능

react-scripts는 React JSX 구문을 프로그래밍 방식으로 일반 JavaScript로 변환하는 데 필요한 빌드 도구를 실행하기 위한 스크립트입니다.

이 패키지에서 제공하는 스크립트는 4개입니다.

스크립트 중 하나를 실행하면 /bin/react-scripts.js가 실행되어 프로세스를 시작합니다. 이 스크립트는 호출에 전달된 인수를 조사합니다. 시작, 빌드, 테스트 및 꺼내기 인수만 허용합니다.

다른 인수를 전달하면 스크립트가 알 수 없는 스크립트를 로그에 반환합니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/cra-unknown-script-2.png)

올바른 인수를 전달하면 `/scripts` 폴더 내에 있는 스크립트가 실행됩니다. 먼저 `start.js` 스크립트를 살펴보겠습니다.

## 대응 스크립트 시작 프로세스의 작동 방식

`start` 인수를 사용하면, NPM은 Retact 애플리케이션에 사용할 수 있는 개발 서버를 만들기 위한 프로세스를 시작합니다. 다음은 이 스크립트에 대한 태스크 목록입니다.

- 노드 및 Babel의 빌드 환경을 `개발`로 설정
- 빌드 프로세스에 대한 환경 변수 읽기 확인
- 프로젝트에 설치된 패키지가 오래되지 않았는지 확인
- 코드가 TypeScript에 있는지 확인합니다.
- 프로세스에 필요한 패키지(대부분 웹 팩 관련 모듈) 가져오기
- 사용 가능한 포트 및 호스트 IP를 확인하십시오. 기본값은 0.0.0.0:3000입니다.
- 컴파일러를 실행하고 웹 팩에서 메시지를 수신합니다. 웹 팩은 Babel, ESLint 및 기타 도구를 사용하여 코드를 준비합니다.
- 웹 팩이 실행되는 동안 스크립트는 브라우저를 열고 개발 서버를 시작합니다.

WebpackDevServer에서 만든 개발 서버는 또한 JavaScript 파일의 변경사항 수신기를 작성합니다. 사용자가 JavaScript 파일을 변경하고 저장하면 개발 서버는 사용자의 코드를 다시 컴파일하고 브라우저를 빠르게 새로 고칩니다.

## retact-scripts build 명령을 사용하는 방법

`build` 명령은 사용자를 위한 프로덕션 준비 응답 앱을 만드는 프로세스를 시작합니다. 빌드 환경을 프로덕션으로 설정하는 것을 제외하고는 대부분 시작 명령과 같은 단계를 수행합니다.

이 스크립트는 사용 가능한 포트를 확인하고 개발 서버를 실행하는 대신 `빌드` 기능을 실행하여 모든 개별 파일을 하나의 `bundle.js` 파일로 번들링합니다. 또한 프로덕션 빌드는 코드가 최적화되고 최소화되어 최상의 성능을 발휘하도록 보장합니다.

이전에 이미 `빌드` 명령을 실행한 경우 스크립트는 현재 파일 크기를 사용하여 다음 빌드와 비교합니다. 파일 크기가 변경된 정도를 보여줍니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/cra-build-result.png)

이 명령의 최종 출력은 프로젝트의 루트에서 생성되는 `빌드/` 폴더에서 찾을 수 있습니다.

## retact-scripts test 명령을 사용하는 방법

test 명령은 Jest를 사용하여 작성한 모든 테스트 스크립트를 실행합니다. 테스트는 노드 환경에서 실행됩니다. Jest는 파일을 저장할 때마다 시작 명령어가 코드를 다시 컴파일하는 것과 같은 테스트를 다시 실행하는 대화형 감시 모드로 실행됩니다.

테스트 파일을 `src/` 폴더 내 어디에나 저장할 수 있으며 스크립트는 `.test.js` 또는 `.spec.js` 확장자를 가진 파일을 찾아서 실행합니다. 또한 `__twin__/` 폴더 아래에서 `.js` 파일을 실행합니다.

테스트 결과는 터미널에서 확인할 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/cra-test-result-1.png)

CRA의 테스트 명령은 안정적인 환경에서 구성 요소 및 비즈니스 로직을 테스트하는 데만 적용된다는 점에 유의하십시오. 브라우저에서 종단 간 테스트를 실행하려면 다른 테스트 라이브러리를 사용해야 합니다.

## retact-scripts 꺼내기 명령을 사용하는 방법

마지막 명령인 `eject`는 `react-scripts`에 대한 종속성을 제거하고 사용자가 수정할 빌드 도구 및 구성을 표시하는 데 사용됩니다.

react-scripts의 모든 구성 파일은 프로젝트 루트의 `config/` 폴더에 복사되고 빌드를 실행할 스크립트는 `scripts/` 폴더에 복사됩니다. 또한 종속성이 루트의 `패키지`로 이동됩니다.json의 파일

이 명령은 단방향 작업입니다. CRA 설정에서 꺼낸 후에는 실행 취소할 수 없습니다. Git과 같은 소스 코드 관리 시스템에 코드를 커밋한 경우 git checkout 또는 git reset으로 변경 사항을 실행 취소할 수 있습니다.

CRA는 이미 중소규모 프로젝트에 적합한 적절한 구성을 제공했으므로 일반적으로 이 명령을 실행할 필요가 없습니다. 자세한 내용을 알고 싶으시면 Retact App을 꺼내는 방법에 대한 게시물을 여기에 작성했습니다.

Create React 앱을 꺼낼까요?

## 결론

더 많은 사람들이 CRA를 사용함에 따라, 개발 팀은 실제 프로젝트에서 툴이 어떻게 사용되는지에 대해 더 많은 피드백을 받게 될 것입니다. 개발 팀에서 얻은 통찰력은 CRA가 최신 툴을 계속 업데이트하고 Retact 앱을 구축하는 모범 사례를 보유할 수 있도록 보장합니다.

읽어주셔서 감사합니다. 이 기사를 통해 CRA가 🙂에서 어떻게 작동하는지 이해하셨기를 바랍니다.

대응에 대한 추가 정보:

- 반응 구성 요소의 화살표 기능을 사용해야 합니까?
- 소품 전달 시 스프레드 속성을 사용해야 합니까?
- React 컨텍스트 API 이해