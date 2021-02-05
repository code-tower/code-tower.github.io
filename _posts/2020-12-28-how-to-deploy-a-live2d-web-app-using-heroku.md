---
layout: post
title: "Heroku를 사용하여 Live 2D 웹 앱을 배포하는 방법"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/web-2.gif
tags: undefined
---


## Live2D란?

Live2D는 아티스트들이 기존의 2D 일러스트를 쉽게 변형시켜 유연한 표현과 동작을 연출할 수 있도록 하는 기술이다.

라이브 2D 모델링 및 애니메이션용으로 가장 인기 있는 소프트웨어는 큐비즘(Cubism)으로, 웹, 네이티브 앱, 유니티 게임 개발 엔진을 위한 문서화된 SDK를 제공한다.

본 튜토리얼에서는 Cubism의 공식 Live2D Web SDK 샘플 위에 구축하여 널리 사용되는 클라우드 앱 호스팅 플랫폼인 Heroku에 배포하는 방법에 대해 설명하겠습니다.

## 환경 설정 방법

이 튜토리얼을 따라 하려면 내 GitHubrepo를 복제하고 `start` 지점을 확인하십시오. 완성된 프로젝트는 `개발` 지점에 있다.

유튜브에 비디오 튜토리얼도 녹음해놨어요.

```undefined
git clone https://github.com/RuolinZheng08/heroku-live2d.git
git checkout start

# update the submodule, Cubism's Live2d Web Framework
git submodule update --init
```

Homebrew를 사용하여 Node.js 및 npm 설치:

```undefined
# if you need to install homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# homebrew will install node and npm at the same time
brew install node
```

Visual Studio Code를 기본 IDE로 사용하겠지만 원하는 편집기를 사용하면 됩니다.

## 로컬에서 스타터 코드를 실행하는 방법

디렉토리 구조는 다음과 같습니다. 우리의 웹 앱은 `샘플/TypeScript/Demo`에서 제공될 것입니다.

```undefined
.
├─ .vscode          # Visual Studio Code project setting
├─ Core             # Live2D Cubism Core JavaScript and TypeScript source code
├─ Framework        #  Source code for the rendering and animation features
└─ Samples
   ├─ Resources     # Live2D model files and web image assets
   └─ TypeScript    # [IMPORTANT] TypeScript sample project
```

heroku-live2d 디렉토리에서 다음 명령을 실행합니다.

```undefined
cd Samples/TypeScript/Demo/

npm install

npm run-script build

npm run-script serve
```

http://localhost:5000/샘플/TypeScript/Demo/로 이동하면 Live2D 문자를 볼 수 있습니다.

모델과 상호 작용하려면 마우스 커서를 누른 상태에서 캐릭터의 머리와 눈이 커서를 따릅니다. 특수 애니메이션을 보려면 캐릭터 본문을 누르십시오. 오른쪽 상단 모서리에 있는 기어 아이콘을 누르면 다른 모델 간에 전환됩니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/web.gif)

## Heroku에 배포하는 방법

시작 코드는 npm, TypeScript 및 웹 팩을 사용합니다.

헤로쿠에 우리의 프로젝트를 배치하기 위해서는, 우리는 `패키지`를 만들어야 한다.herku가 프로젝트 루트 디렉토리에서 프로젝트를 빌드하는 데 사용할 수 있는 json` 파일. 우리는 또한 `Sample/TypeScript/Demo/package`를 수정해야 한다.json 및 `Sample/TypeScript/Demo/webpack.config.js`의 웹 팩 구성.

### 최상위 패키지.죤슨

보일러 플레이트 패키지입니다.Node.js Heroku 앱의 json은 다음과 같습니다.

```undefined
{
    "name": "heroku-live2d",
    "description": "Live2D Cubism Heroku Demo",
    "scripts": {
        "start": ...,
        "build": ...
    },
    "dependencies": {
     ...
    }
}
```

샘플/TypeScript/Demo/package의 `dependency` 및 `devDependency` 특성을 검사합니다.json은 두 가지 종속성을 모두 herku-live2d/d/d에 종속성으로 추가한다.제이슨의

로컬에서 빌드 및 서비스할 때 샘플/TypeScript/Demo 디렉토리 내에서 npm run-script [build|serve]를 사용했다는 점을 기억하십시오.

따라서 프로젝트 루트에서 npm 명령을 실행하려면 npm 명령 앞에 `cd 샘플/TypeScript/Demo`를 붙여야 합니다. 예를 들어 빌드 명령은 다음과 같습니다.

```undefined
cd Samples/TypeScript/Demo && npm run-script build
```

이러한 변경으로 최상위 수준 패키지입니다.json은 다음과 같이 보여야 한다.

```undefined
{
    "name": "heroku-live2d",
    "description": "Live2D Cubism Heroku Demo",
    "scripts": {
        "start": "cd Samples/TypeScript/Demo && npm run-script start",
        "build": "cd Samples/TypeScript/Demo && npm run-script build"
    },
    "dependencies": {
        "@typescript-eslint/eslint-plugin": "^2.18.0",
        "@typescript-eslint/parser": "^2.18.0",
        "eslint": "^6.8.0",
        "eslint-config-prettier": "^6.10.0",
        "eslint-plugin-prettier": "^3.1.2",
        "prettier": "^1.19.1",
        "rimraf": "^3.0.1",
        "serve": "^11.3.0",
        "ts-loader": "^6.2.1",
        "typescript": "^3.7.5",
        "webpack": "^4.41.5",
        "webpack-cli": "^3.3.10",
        "webpack-dev-server": "^3.10.1",
        "whatwg-fetch": "^3.0.0"
    }
}

```

### 샘플/TypeScript/Demo/패키지입니다.죤슨

로컬 호스트에서는 포트 5000에서 실행 중입니다. 그러나 Herku는 변수 `$PORT`에 저장된 포트를 웹 앱에 동적으로 할당합니다. 따라서 샘플/TypeScript/Demo/package 내에 `npm run-script start` 명령이 필요합니다.json은 포트 `$PORT`에서 웹팩 서버를 시작합니다.

`scripts > start > webpack-dev-server --progress`에 추가하여 다음과 같이 표시합니다.

```undefined
"scripts": {
    "start": "webpack-dev-server --progress --port $PORT",
    ...
}
```

### 샘플/TypeScript/Demo/webpack.config.js

사용 안 함 추가HostCheck는 위에서 동적으로 구성했으므로 `devServer`의 구성을 확인하고 `port`를 제거합니다.

```js
module.exports = {
    ...,
    devServer: {
        contentBase: path.resolve(__dirname, '../../..'),
        watchContentBase: true,
        inline: true,
        hot: true,
        port: 5000, // delete this line
        host: '0.0.0.0',
        disableHostCheck: true, // add this line
        compress: true,
        useLocalIp: true,
        writeToDisk: true
    },
    ...
}
```

`node_module`이 감시되지 않도록 `watch Options`를 추가합니다. 이렇게 하지 않으면 헤로쿠에 배치할 때 최대 감시자 수를 초과하는 오류가 발생합니다.

```js
module.exports = {
    ...,
    watchOptions: {
     ignored: /node_modules/
    },
    ...
}
```

### 헤로쿠에 배포

Heroku 명령줄 클라이언트를 다운로드하려면

```undefined
brew tap heroku/brew && brew install heroku
```

`heroku 로그인`을 사용하여 명령줄에서 Heroku에 로그인합니다.

Heroku 앱을 만들고 일부 숫자(예: 123)를 앱 이름에 추가하여 고유성을 보장합니다.

```undefined
heroku create heroku-live2d-NUMBERS
```

Node.js를 빌드 팩으로 설정합니다.

```undefined
heroku buildpacks:set heroku/nodejs
```

git를 사용하여 프로젝트를 추가하고 커밋합니다. git push가 반드시 필요한 것은 아닙니다.

```undefined
git add .
git commit -m "Ready to deploy to heroku"
```

당신이 스타트 지점을 따라간다고 가정하면 프로젝트를 헤로쿠로 밀어넣습니다. 지금 있는 분기를 항상 확인하고 해당 분기에서 밀어넣을 수 있습니다.

```undefined
# check which branch we are on
git branch

# the syntax is
# git push heroku GIT_BRANCH_NAME:HEROKU_BRANCH_NAME
git push heroku start:master
```

빌드 프로세스가 완료될 때까지 몇 분 정도 기다려야 할 수 있습니다.

그런 다음 YOUR-HEROKU-APP-NAME.herokuapp.com/Samples/TypeScript/Demo으로 이동합니다. 제 경우 URL은 https://heroku-live2d.herokuapp.com/Samples/TypeScript/Demo/입니다. 라이브 2D 캐릭터가 여러분을 맞이할 것입니다:)

![image](https://www.freecodecamp.org/news/content/images/2020/12/Screen-Shot-2020-12-27-at-16.13.19.png)

### index.html을 샘플/TypeScript/Demo로 리디렉션하는 방법

라이브2D 모델 대신 디렉토리 구조 목록을 보여주는 YOUR-HEROKU-APP-NAME.herokuapp.com이 있을 수 있다. 샘플/TypeScript/Demo로 리디렉션되는 더미 최상위 수준 `index.html`을 추가하여 이를 해결할 수 있다.

```html
<!DOCTYPE html>
<html>

<head>
    <title></title>
    <!-- Just a dummy html to redirect to my subdirectory -->
    <meta http-equiv="refresh" content="0; url=Samples/TypeScript/Demo">
</head>

<body>

</body>

</html>

```

배포 명령 `git push herku start:master`를 다시 실행합니다. 이제 YOUR-HEROKU-APP-NAME.herokuapp.com을 방문하면 Live 2D 모델 페이지로 자동 리디렉션됩니다.

이 튜토리얼을 끝낸 것을 축하합니다! 이제 Herku에 Live 2D 웹 앱이 배포되었습니다.

나는 네가 이 튜토리얼을 즐겼기를 바란다. 계속 연락해요! LinkedIn, GitHub, Medium에서 연결하거나 개인 웹 사이트를 확인하십시오.

### 자원.

이 튜토리얼의 My GitHubrepo

내 헤로쿠 앱

내 YouTube 비디오 튜토리얼

큐비즘의 공식 SDK 설명서