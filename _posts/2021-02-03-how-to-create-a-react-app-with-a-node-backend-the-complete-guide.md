---
layout: post
title: "노드 백엔드를 사용하여 응답 앱을 생성하는 방법: 전체 가이드"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/02/how-to-build-a-react-app-with-a-node-backend-alt.png
tags: undefined
---


노드 백엔드에 연결된 React frontend는 빌드하려는 모든 애플리케이션에 대해 견고한 조합입니다.

본 가이드는 React를 통해 가능한 한 쉽게 풀 스택 프로젝트를 만들 수 있도록 설계되었습니다.

반응 및 노드를 사용하여 전체 프로젝트를 처음부터 웹에 배포하는 방법에 대해 살펴보겠습니다.

> React 및 Node 앱을 직접 구축 및 구축하시겠습니까? 이와 같은 전체 스택 React 프로젝트를 구축하는 방법을 보여 주는 제 과정 시리즈를 확인해 보십시오.

## 필요한 도구

- 컴퓨터에 Node 및 NPM이 설치되어 있는지 확인합니다. nodejs.org에서 두 가지를 모두 다운로드할 수 있습니다(NPM은 노드 설치에 포함되어 있습니다).
- 선택한 코드 편집기를 사용합니다. 사용 중이며 개인적으로 VSCode 사용을 권장합니다. VSCode는 code.visualstudio.com에서 다운로드할 수 있습니다.
- 컴퓨터에 Git이 설치되어 있는지 확인합니다. 이것은 Herku와 함께 우리의 애플리케이션을 배치하는 데 필요합니다. git-scm.com에서 구입하실 수 있습니다.
- heroku.com의 계정. 우리는 Herku를 이용하여 전적으로 무료로 웹에 앱을 게시할 것입니다.

## 1단계: 노드(Express) 백엔드 생성

먼저 프로젝트의 폴더를 생성합니다. 예를 들어 `react-node-app`이라고 합니다.

그런 다음 해당 폴더를 코드 편집기로 끕니다.

Node 프로젝트를 생성하려면 터미널에서 다음 명령을 실행하십시오.

```undefined
npm init -y
```

패키지가 생성됩니다.json 파일을 사용하면 모든 앱 스크립트를 추적하고 노드 앱에 필요한 종속성을 관리할 수 있습니다.

서버 코드는 `서버`라는 동일한 이름의 폴더에 저장됩니다. 그 폴더를 만들어 봅시다.

이 파일에는 단일 파일이 배치되며, 이 파일 중 `index.js`라는 서버가 실행됩니다.

환경 변수 `PORT`에 대한 값이 제공되지 않을 경우 Express를 사용하여 포트 3001에서 실행되는 간단한 웹 서버를 만들 것입니다(Heroku는 앱을 배포할 때 이 값을 설정합니다).

```undefined
// server/index.js

const express = require("express");

const PORT = process.env.PORT || 3001;

const app = express();

app.listen(PORT, () => {
  console.log(`Server listening on ${PORT}`);
});
```

그런 다음 터미널에서 Express를 종속적으로 설치하여 사용할 것입니다.

```undefined
npm i express
```

그런 다음, 우리는 패키지로 스크립트를 작성할 것입니다.npm start(npm start)로 실행할 때 웹 서버를 시작하는 json:

```undefined
// server/package.json

...
"scripts": {
  "start": "node server/index.js"
},
...
```

마지막으로 터미널에서 npm start를 실행하여 이 스크립트를 사용하여 앱을 실행할 수 있으며 포트 3001에서 실행 중인지 확인해야 합니다.

```undefined
npm start

> node server/index.js

Server listening on 3001
```

## 2단계: API Endpoint 생성

우리는 우리의 노드 및 익스프레스 서버를 API로 사용하여 그것이 우리의 리액트 앱 데이터를 주고, 그 데이터를 변경하거나, 서버만이 할 수 있는 다른 작업을 할 수 있기를 원한다.

우리의 경우, JSON 객체에 "서버에서 안녕!"이라는 메시지를 간단히 Relect 앱에 보낼 것입니다.

아래 코드는 `/api` 경로에 대한 끝점을 생성합니다.

Retact 앱이 해당 경로에 GET 요청을 하면 JSON 데이터로 (응답의 약자인 `res`를 사용하여) 응답합니다.

```undefined
// server/index.js
...

app.get("/api", (req, res) => {
  res.json({ message: "Hello from server!" });
});

app.listen(PORT, () => {
  console.log(`Server listening on ${PORT}`);
});
```

참고: `app.listen` 함수 위에 이 값을 배치하십시오.

노드 코드를 변경했으므로 서버를 다시 시작해야 합니다.

이렇게 하려면 Command/Ctrl + C를 눌러 터미널에서 시작 스크립트를 종료합니다. 그런 다음 `npm start`를 다시 실행하여 다시 시작합니다.

이를 테스트하기 위해 브라우저에 있는 `http://localhost:3001/api`를 방문하면 다음과 같은 메시지를 볼 수 있습니다.

## 3단계: 반응 프런트 엔드 만들기

백엔드를 생성한 후 프런트 엔드로 이동하겠습니다.

다른 터미널 탭을 열고 Create-react-app을 사용하여 `client`라는 이름으로 새 React 프로젝트를 만듭니다.

```undefined
npx create-react-app client
```

그런 다음 모든 종속성을 갖춘 Retact 앱을 설치하겠습니다.

우리가 해야 할 유일한 변화는 `프록시`라는 자산을 패키지에 추가하는 것이다.json 파일

이렇게 하면 네트워크 요청을 할 때마다 실행 중인 오리진(http://localhost:3001)을 제공하지 않고도 Node 서버에 대한 요청을 할 수 있습니다.

```undefined
// client/package.json

...
"proxy": "http://localhost:3001",
...
```

그런 다음 노드 서버와 동일한 시작 스크립트를 실행하여 React 앱을 시작할 수 있습니다. 먼저 새로 만든 클라이언트 폴더에 `cd`를 넣어야 합니다.

이후 localhost:3000에서 시작합니다.

```undefined
cd client
npm start

Compiled successfully!

You can now view client in the browser.

Local:            http://localhost:3000
```

## 4단계: 노드에 대응에서 HTTP 요청 만들기

이제 Retact 앱이 작동되고 있으므로 API와 상호 작용하기 위해 사용하고 싶습니다.

앞에서 생성한 `/api` 끝점에서 데이터를 가져오는 방법을 살펴보겠습니다.

이를 위해, 우리는 `src` 폴더에 있는 `App.js` 컴포넌트로 이동하여 useEffect를 사용하여 HTTP 요청을 할 수 있습니다.

FETC API를 사용하여 백엔드로 간단한 GET 요청을 한 다음 데이터를 JSON으로 반환하도록 하겠습니다.

데이터가 반환되면 메시지 속성(서버에서 보낸 인사말 캡처)을 가져와 데이터라는 상태 변수에 넣습니다.

이렇게 하면 해당 메시지가 있는 경우 페이지에 해당 메시지를 표시할 수 있습니다. JSX에서 조건부 데이터를 사용하여 데이터가 아직 없으면 "Loading.."이라는 텍스트를 표시하려고 합니다..".

```undefined
// client/src/App.js

import React from "react";
import logo from "./logo.svg";
import "./App.css";

function App() {
  const [data, setData] = React.useState(null);

  React.useEffect(() => {
    fetch("/api")
      .then((res) => res.json())
      .then((data) => setData(data.message));
  }, []);

  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>{!data ? "Loading..." : data}</p>
      </header>
    </div>
  );
}

export default App;
```

## 5단계: Heroku를 사용하여 웹에 앱 배포

마지막으로, 애플리케이션을 웹에 배포하겠습니다.

먼저 클라이언트 폴더 내에서 자동으로 초기화되는 Gitrepo를 create-react-app으로 제거해야 합니다.

이것은 앱 배포에 필수적인데, 왜냐하면 우리는 `클라이언트`가 아니라 프로젝트의 루트 폴더(`react-node-app`)에 Gitrepo를 설치할 것이기 때문이다.

```undefined
cd client
rm -rf .git
```

배포할 때 노드 백엔드 및 대응 프런트엔드 모두 동일한 도메인(즉, 내 쿨 앱)에서 제공됩니다.herokuapp.com).

Node API에서 요청을 처리하는 방법을 알 수 있으므로 사용자가 요청하면(예: 앱의 홈 페이지로 이동할 때) React 앱을 표시하는 코드를 작성해야 합니다.

다음 코드를 추가하여 `server/index.js`에서 이 작업을 다시 수행할 수 있습니다.

```undefined
// server/index.js
const path = require('path');
const express = require('express');

...

// Have Node serve the files for our built React app
app.use(express.static(path.resolve(__dirname, '../client/build')));

// Handle GET requests to /api route
app.get("/api", (req, res) => {
  res.json({ message: "Hello from server!" });
});

// All other GET requests not handled before will return our React app
app.get('*', (req, res) => {
  res.sendFile(path.resolve(__dirname, '../client/build', 'index.html'));
});
```

이 코드를 사용하면 먼저 노드가 정적 파일에 대해 `express.static` 기능을 사용하여 빌드된 Retact 프로젝트에 액세스할 수 있습니다.

그리고 만약 GET 요청이 우리의 `/api` 경로로 처리되지 않는다면, 우리의 서버는 우리의 Retact 앱으로 응답할 것입니다.

이 코드를 사용하면 React 및 Node 앱을 동일한 도메인에 함께 배포할 수 있습니다.

그러면 서버 패키지에 `빌드` 스크립트를 추가하여 Node App에 이 방법을 알려줄 수 있습니다.프로덕션용 React 앱을 빌드하는 json 파일:

```undefined
// server/package.json

...
"scripts": {
    "start": "node server/index.js",
    "build": "cd client && npm install && npm run build"
  },
...
```

또한 프로젝트를 빌드하는 데 사용 중인 노드 버전을 지정할 수 있는 "엔진" 필드를 제공하는 것이 좋습니다. 배포에 사용됩니다.

노드 -v를 실행하여 노드 버전을 얻을 수 있으며, 그 결과를 "엔진"에 넣을 수 있습니다(예: 14.15.4).

```undefined
// server/package.json

"engines": {
  "node": "your-node-version"
}
```

이후 Heroku를 사용하여 배포할 준비가 되었으므로 Heroku.com에 계정이 있는지 확인하십시오.

로그인한 후 대시보드를 보고 있으면 New(새로 만들기) > Create New App(새 앱 만들기)을 선택하고 고유한 앱 이름을 제공합니다.

그런 다음 Git을 사용하여 변경할 때마다 앱을 배포할 수 있도록 컴퓨터에 Heroku CLI를 설치합니다. 다음을 실행하여 CLI를 설치할 수 있습니다.

```undefined
sudo npm i -g heroku
```

설치가 완료되면 `heroku 로그인` 명령을 사용하여 CLI를 통해 Heroku에 로그인합니다.

```undefined
heroku login

Press any key to login to Heroku
```

로그인한 후에는 "Deploy" 탭에서 생성한 앱의 배포 지침을 따르면 됩니다.

다음 네 가지 명령은 프로젝트를 위해 새로운 Gitrepo를 초기화하여 파일을 추가하고 커밋한 다음 Heroku를 위한 Git 리모콘을 추가합니다.

```undefined
git init
heroku git:remote -a insert-your-app-name-here
git add .
git commit -am "Deploy app to Heroku"
```

그리고 마지막 단계는 방금 추가한 Heroku Git 리모콘을 사용하여 앱을 게시하는 것입니다.

```undefined
git push heroku master
```

축하합니다! NAT의 전체 스택 Retact and Node 앱이 활성 상태입니다! 🎉

앱을 계속 변경하고 배포하려면 Git를 사용하여 파일을 추가하고 커밋한 다음 Heroku 리모컨으로 푸시하기만 하면 됩니다.

```undefined
git add .
git commit -m "my commit message"
git push heroku master
```

## 리액트와 함께 유튜브, 인스타그램, 트위터 같은 실제 앱을 만들고 싶으십니까? 건배!

매월 말에는 Retact를 사용하여 완벽한 애플리케이션 클론을 처음부터 끝까지 구축하는 방법을 보여주는 독점 코스를 출시할 예정입니다.

다음 코스가 중단되면 알려드릴까요? 여기에 대기자 명단에 참여하세요.