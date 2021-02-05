---
layout: post
title: "React 프로젝트에 서버리스 데이터베이스를 추가하는 방법
 "
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1600267165477-6d4cc741b379?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDExN3x8c2VydmVyfGVufDB8fHw&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


React는 여전히 가장 인기있는 프론트 엔드 자바 스크립트 라이브러리 중 하나입니다.
 연례 Stack Overflow 개발자 설문 조사에 따르면 React는 인터페이스 구축을위한 가장 인기있는 프런트 엔드 라이브러리이며 전체적으로 두 번째로 인기있는 웹 프레임 워크입니다.
 

더욱 인상적인 것은 그 인기가 매년 계속 증가하고 있다는 것입니다.
 

지난 몇 년 동안 수많은 경쟁자들이 React를 무너 뜨리려고했지만 React가 개발자들 사이에서 계속해서 인기를 끌고 싶어하는 이유는 무엇입니까?
 

이 질문에 대한 완전한 답은 매우 기술적 일 수 있으므로 짧고 달콤하게 만들기 위해 최선을 다할 것입니다.
 

첫째, React의 가상 DOM은 빠르고 효율적입니다.
 둘째, 선언적 JSX 구문은 배우기 쉽고 개발자가 친숙한 프로그래밍 패턴을 특징으로합니다.
 

이러한 이점으로 인해 React는 다양한 애플리케이션 유형에 이상적입니다.
 또한 개인과 소규모 팀은 웹 앱으로 React를 계속 선택합니다.
 

최신 웹 애플리케이션의 일반적인 요구 사항은 실시간 데이터를 제공하고 쿼리하는 백엔드 데이터베이스입니다.
 백엔드 데이터베이스의 기존 구현은 종종 매우 불안정하고 비용 효율적일 수 있습니다.
 

고맙게도 지난 5 년 동안 서버리스 기술은 최신 애플리케이션 개발의 최전선이되었습니다.
 

이러한 맥락에서 서버리스는 개발자가 데이터베이스 및 기타 백엔드 서비스를 호스팅하기 위해 실제 서버를 설정하고 관리 할 필요가 없음을 의미합니다.
 대신 보안 공급자를 사용하여 백엔드를 호스팅하고 프런트 엔드 애플리케이션 코드에서 직접 연결합니다.
 확장 성 및 시스템에 대해 걱정할 필요가 없습니다.
 

이 애플리케이션 아키텍처는 비교적 새롭지 만 비용 효율적이고 생산성을 크게 향상시킵니다.
 이러한 이점은 React를 사용하여 현대적인 프로덕션 애플리케이션을 구축하는 사람들에게 잘 적용됩니다.
 또한 Easybase와 같은 서비스는 상태 저장 React 구성 요소를 위해 특별히 구축 된 서버리스 라이브러리를 만들었습니다.
 

이 기사는`easybase-react` 라이브러리를 사용하여 새로운 React 프로젝트에서 상태 저장, 서버리스 데이터베이스를 구현하는 것이 얼마나 쉬운 지 보여줄 것입니다.
 아래 예제는 간단한 메모 작성 앱이지만 서버리스 아키텍처는 모든 종류의 애플리케이션을 간소화 할 수있는 잠재력을 가지고 있습니다.
 

## 목차 :
 

- React 프로젝트 및 구성 요소를 초기화하는 방법
 
- 서버리스 데이터베이스를 설정하는 방법
 
- 가변 데이터베이스 배열
 

## React 프로젝트 및 구성 요소를 초기화하는 방법
 

새로운 React 프로젝트를 생성하기 위해 인기있는`create-react-app` 라이브러리를 사용할 것입니다 (머신에 Node가 설치되어 있는지 확인하십시오).
 

React 프로젝트를 수동으로 설정하는 데 익숙하지 않은 사람들에게이 라이브러리를 사용하면 적절하게 구성된 빈 프로젝트가 생성되므로이 라이브러리를 사용하는 것이 좋습니다.
 

새 프로젝트를 만들려는 위치에서 다음 명령을 실행합니다.
 

```undefined
npx create-react-app serverless-database-app
```

완료되면 서버리스 라이브러리를 설치하겠습니다.
 

```undefined
cd serverless-database-app && npm install easybase-react
```

마지막으로 프로젝트를 시작할 수 있습니다.
 

```undefined
npm run start
```

애플리케이션은 기본 브라우저에서 자동으로 열립니다.
 표시되는 루트 구성 요소는`src / App.js`에 있으며 여기에서 주요 변경 사항이 적용됩니다.
 

서버리스 공급자에 들어가기 전에`App.js`의 코드를 단순화하겠습니다.
 앱과 카드의 두 가지 구성 요소가 있습니다.
 `App.js`는 이제 다음과 같이 표시됩니다.
 

```undefined
import './App.css';

function App() {
  return (
    <div className="App" style={{ display: "flex", justifyContent: "center" }}>
      <Notes />
    </div>
  );
}

function Notes() {
  const backendData = [
    { title: "Grocery List", description: "Milk, Soup, Bread", createdat: "01-18-2021" },
    { title: "Math Homework", description: "Remember to finish question 8-10 before monday", createdat: "12-01-2020" },
    { title: "Call James", description: "Ask him about the company party.", createdat: "12-30-2020" }
  ]

  const noteRootStyle = {
    border: "2px #0af solid",
    borderRadius: 9,
    margin: 20,
    backgroundColor: "#efefef",
    padding: 6
  };

  return (
    <div style={{ width: 400 }}>
      {backendData.map(ele => 
        <div style={noteRootStyle}>
          <h3>{ele.title}</h3>
          <p>{ele.description}</p>
          <small>{ele.createdat}</small>
        </div>
      )}
    </div>
  )
}

export default App;

```

backendData라는 몇 가지 예제 데이터를 추가했지만 다음 단계에서이를 실시간 데이터베이스로 대체하겠습니다.
 다음은 참조 용으로 현재 구현 된 스크린 샷입니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-26-at-6.19.02-PM.png)

간결함을 위해이 애플리케이션의 스타일은 매우 초보적입니다.
 하지만 자신의 애플리케이션에 고유 한 모양과 느낌을 부여해야합니다!
 

## 서버리스 데이터베이스를 설정하는 방법
 

주변에 일반적인 서버리스 백엔드 제공 업체가 많이 있습니다 (AWS, Google Cloud 등).
 이러한 공급자의 기능간에 차이가 있습니다.
 일부는 모바일 애플리케이션이나 병렬 처리 또는 기계 학습 등에 더 적합합니다.
 

Easybase의 플랫폼에는 서버리스 애플리케이션 용으로 빌드 된 React 전용 라이브러리가 있기 때문에 저는 Easybase를 사용할 것입니다.
 이 패키지가 코드에서 얼마나 빠르고 쉽게 설정되는지 아래에서 볼 수 있습니다.
 

저는이 플랫폼을 여러 프로젝트에 사용했으며`easybase-react`의 가장 중요한 측면은 자동 세션 캐싱과 보안 데이터 가져 오기입니다.
 이러한 모듈을 수동으로 구현하는 것은 큰 번거 로움이며 그 자체로 전체 프로젝트가 될 수 있습니다.
 

먼저 `App.js`를 두 가지로 변경하겠습니다.
 먼저 `App.js`상단에 임포트 라인을 추가하여 앞서 설치 한 `easybase-react`패키지를 사용해 보겠습니다.
 EasybaseProvider 및 useEasybase를 가져옵니다.
 

둘째, EasybaseProvider 구성 요소에 Notes 구성 요소를 래핑합니다.
 

`App.js`는 이제 다음과 같이 보일 것입니다.
 React에서 useEffect 후크도 가져 왔습니다.
 

```undefined
import './App.css';
import { EasybaseProvider, useEasybase } from 'easybase-react';
import { useEffect } from 'react';

function App() {
  return (
    <div className="App" style={{ display: "flex", justifyContent: "center" }}>
      <EasybaseProvider>
        <Notes />
      </EasybaseProvider>
    </div>
  );
}

// ...
```

EasybaseProvider 구성 요소는 필요한 구성을 전달하면 모든 하위 구성 요소에 useEasybase 후크에 대한 유효한 액세스 권한을 부여합니다.
 

EasybaseProvider에는 React 프로젝트 내에서 모든 연결을 인증하고 보호하는 단일 파일 인`ebconfig`라는 prop이 있습니다.
 

사용자 지정 데이터 테이블과 연결된`ebconfig` 토큰을 얻는 방법은 다음과 같습니다.
 

- Easybase에 로그인하거나 무료 계정을 만드십시오.
 
- 왼쪽 하단 버튼 그룹의 `+`버튼을 통해 테이블 만들기 대화 상자를 엽니 다.
 
- 테이블에 이름을 지정하고 예제 배열 (제목, 설명, 생성 위치)에 해당하는 열을 만듭니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-27-at-10.54.21-AM.png)

참조를 위해 backendData 배열의 예제 행을 수동으로 추가 할 것이지만이 단계는 필요하지 않습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-27-at-11.02.27-AM.png)

- 통합 탭으로 이동하여 새 React 통합을 만듭니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-27-at-1.32.45-PM.png)

- 오른쪽 서랍에서 활성, 테스트 모드를 활성화하고 권한을 읽고 쓸 수 있습니다.
 그런 다음 React 토큰을 다운로드하고 오른쪽 상단의 저장을 클릭하십시오.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-27-at-6.37.13-PM.png)

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-27-at-6.37.16-PM.png)

- 새로 다운로드 한 ebconfig.js 파일을 프로젝트의`src /`폴더에 넣습니다.
 

```undefined
├── README.md
├── node_modules/
├── package.json
├── public/
└── src/
    ├── ebconfig.js   <---
    ├── App.css
    ├── App.js
    ├── index.css
    ├── index.js
    └── ...
```

- 마지막으로이 파일을`App.js`로 가져와 EasybaseProvider의`ebconfig` prop으로 다음과 같이 전달합니다.
 

```undefined
import './App.css';
import { EasybaseProvider, useEasybase } from 'easybase-react';
import { useEffect } from 'react';
import ebconfig from './ebconfig';

function App() {
  return (
    <div className="App" style={{ display: "flex", justifyContent: "center" }}>
      <EasybaseProvider ebconfig={ebconfig}>
        <Notes />
      </EasybaseProvider>
    </div>
  );
}

// ...
```

마찬가지로 우리 프로젝트는 서버리스 기능을 위해 구성됩니다.
 이제 남은 일은`useEasybase` 후크에서 제공하는 함수를 활용하는 것뿐입니다. 다음 섹션에서 수행 할 것입니다.
 

서버리스 아키텍처에서 React 또는 React Native를 사용하는 방법에 대한 자세한 내용은이 연습을 참조하세요.
 

프로젝트가 보안 로그인 인증으로 개별 사용자를 처리하는 경우 간단한 React 통합이 아닌 프로젝트 탭을 사용하십시오.
 

React 사용자 인증에 대한 정보는 Easybase 프로젝트 워크 플로우에 대한 freeCodeCamp 기사에서 찾을 수 있습니다.
 

## 가변 데이터베이스 어레이
 

이제 백엔드를 올바르게 설정 했으므로 EasybaseProvider의 하위 구성 요소가 useEasybase 후크에 액세스 할 수 있습니다.
 이 후크는 원격 데이터에 액세스하는 데 필요한 필수 기능을 제공합니다.
 

세 가지 기능을 가져 오는 것으로 시작하겠습니다.
 `const {Frame, sync, configureFrame} = useEasybase ();`가있는 Notes 구성 요소의 configureFrame, sync 및 Frame.
 

컴포넌트가 처음 마운트 될 때 데이터베이스의 처음 10 개 항목 인 NOTES APP을 가져 오도록 프레임을 구성하려고합니다.
 프레임은 상태 저장 데이터베이스 배열로 작동하며 sync를 호출하면 백엔드 데이터베이스의 변경 사항으로 모든 로컬 변경 사항이 정규화됩니다.
 

```undefined
function Notes() {
  const { Frame, sync, configureFrame } = useEasybase();

  useEffect(() => {
    configureFrame({ tableName: "NOTES APP", limit: 10 });
    sync();
  }, []);

  const noteRootStyle = {
    border: "2px #0af solid",
    borderRadius: 9,
    margin: 20,
    backgroundColor: "#efefef",
    padding: 6
  };

  return (
    <div style={{ width: 400 }}>
      {Frame().map(ele => 
        <div style={noteRootStyle}>
          <h3>{ele.title}</h3>
          <p>{ele.description}</p>
          <small>{String(ele.createdat).slice(0, 10)}</small>
        </div>
      )}
    </div>
  )
}
```

동기화는 필요한 백엔드 프로세스를 자동으로 처리합니다.
 더 중요한 것은 프레임의 새로운 데이터로 컴포넌트를 다시 렌더링한다는 것입니다.
 

응용 프로그램을 다시 빌드하면 표시되는 새 메모는 데이터 테이블에있는 것과 동일합니다.
 축하합니다. 서버리스 데이터베이스를 사용하고 있습니다!
 

새 노트를 Easybase에 푸시하고 그에 따라 애플리케이션을 렌더링하는 버튼을 추가하여 좀 더 재미있게 보겠습니다.
 

NewNoteButton이라는 새 구성 요소를 만듭니다.
 useEasybase 후크에서 동기화 및 프레임 함수를 가져옵니다.
 

절대 위치를 사용하여 창의 왼쪽 상단에이 버튼을 배치하겠습니다.
 사용자가이 버튼을 클릭하면 내 컴포넌트가 사용자로부터 새 제목과 설명을 받고 프레임 및 동기화를 사용하여 Easybase에 게시합니다.
 

새로 생성 된이 구성 요소를 EasybaseProvider 내의 Notes 구성 요소 아래에 놓습니다.
 

```undefined

function App() {
  return (
    <div className="App" style={{ display: "flex", justifyContent: "center" }}>
      <EasybaseProvider ebconfig={ebconfig}>
        <Notes />
        <NewNoteButton />
      </EasybaseProvider>
    </div>
  );
}

// ...

function NewNoteButton() {
  const { Frame, sync } = useEasybase();

  const buttonStyle = {
    position: "absolute",
    left: 10,
    top: 10,
    fontSize: 21
  }

  const handleClick = () => {
    const newTitle = prompt("Please enter a title for your note");
    const newDescription = prompt("Please enter your description");
    
    Frame().push({
      title: newTitle,
      description: newDescription,
      createdat: new Date().toISOString()
    })
    
    sync();
  }

  return <button style={buttonStyle} onClick={handleClick}>📓 Add Note 📓</button>
}
```

내 구현은 기본 프롬프트 기능을 통해 사용자가 원하는 제목과 설명을 수집하지만 프로덕션 앱에는 더 강력한 입력 솔루션이 필요할 수 있습니다.
 그래도 데모에서는 잘 작동합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-27-at-8.20.09-PM.png)

화면의 오른쪽 상단에있는 새 버튼을 확인하십시오.
 이것을 클릭하면 두 개의 텍스트 상자가 나타납니다.
 완료 후 Notes 구성 요소는 새 항목을 표시하는 동기화 호출 후 다시 렌더링됩니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-27-at-8.22.01-PM.png)

이러한 변경 사항은 Easybase 테이블에 즉시 표시되므로 자유롭게 변경할 수 있습니다!
 

## 결론
 

숫자는 거짓말이 아닙니다. React는 강력하고 성숙하며 개발자들에게 사랑 받고 있습니다.
 오픈 소스 커뮤니티는 1500 명이 넘는 기여자와 함께 프로젝트를 실제로 수용했습니다.
 

이 라이브러리는 아름다운 고성능 인터페이스를 만드는 가장 좋은 방법 중 하나로 입증되었습니다.
 실제로 React 프로젝트를 Github 페이지에 바로 배포 할 수도 있습니다.
 

서버리스와 함께 React를 사용하는 것은 쉬운 일이 아닙니다.
 이 확장 가능한 기술의 채택이 크게 증가했습니다.
 지난 8 년 동안 `서버리스`라는 용어에 대한 Google 트렌드 차트를 살펴보세요.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-28-at-2.32.12-PM.png)

이 기술을 통해 개발자는 기존의 오버 헤드없이 훨씬 적은 비용으로 확장 가능한 엔터프라이즈 급 애플리케이션을 배포 할 수 있습니다.
 풍부한 리소스를 가진 사람들이 전통적으로 사용할 수있는 도구를 잠금 해제함으로써 서버리스 기술은 개발자가 아이디어를 현실로 바꾸도록 지속적으로 권장합니다.
 