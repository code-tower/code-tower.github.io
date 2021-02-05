---
layout: post
title: "사용자 인증을 통해 첫 번째 서버 무응답 네이티브 앱을 구축하는 방법"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1508921340878-ba53e1f016ec?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDR8fHVzZXJzfGVufDB8fHw&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


React Native는 모바일 애플리케이션 개발 분야에서 매우 중요한 도구가 되었습니다.

사랑하지 않는 게 뭐야? 이 제품은 빠르고 크로스 플랫폼이며, 네이티브 모듈에 연결되며, 프런트 엔드 개발자들에게 친숙한 언어와 패턴을 사용합니다.

또한, 서버리스 기술은 개발자에게 기존 서버 인프라의 오버헤드 없이 엔터프라이즈급 애플리케이션을 배포할 수 있는 능력을 부여했습니다. 이 솔루션은 생산성을 높이는 동시에 애플리케이션의 백엔드 관리와 관련된 관리 작업을 제거합니다.

이 걱정 없는 플러그 앤 플레이 인프라는 Return 및 React Native와 같은 프레임워크와 잘 결합됩니다. 이는 개인과 소규모 팀이 오버헤드 비용 없이 운영 애플리케이션을 쉽게 확장할 수 있도록 하기 때문입니다.

사용자 인증을 사용하여 React Native 애플리케이션을 생성하는 방법에 대해 살펴보겠습니다. 그런 다음 이 프로세스를 서버 없는 데이터베이스와 통합하는 방법에 대해 설명하겠습니다.

현재 저의 예시 앱은 상태 저장 사용자 인증에 대한 간단한 데모일 뿐 아니라 창의력을 발휘하여 관심사를 파악해 보십시오! 이 데모는 결국 전체 서버가 없는 공동 작업관리 목록 모바일 앱으로 바뀔 것입니다.

## 목차:

- 프로젝트 설정 방법
- 등록/로그인 워크플로우
- 백엔드 플러그인 방법
- 결론

## 프로젝트 설정 방법

리액트 프로젝트에는 서버리스 구현 방법이 여러 가지가 있지만, 우리는 이 프로젝트를 위해 쉬운 베이스 리액트 라이브러리를 사용할 것입니다. 이 함수는 상태 저장성이며 반응 및 반응 네이티브를 위해 설계되었습니다.

React Native 프로젝트로 이동하여 `npm install easy base-react`를 수행합니다.

React Native 프로젝트를 만드는 방법을 모를 경우 콘솔에서 npx 생성-반응-원본-앱 마이네이션-앱을 통해 생성-반응-원본-앱을 사용할 수 있습니다. 이 작업이 완료되면 위에서 설명한 대로 라이브러리를 설치합니다.

이 때 테스트할 플랫폼에 따라 `npm runios` 또는 `npm run Android`를 실행하여 응용프로그램을 열 수 있습니다. 시작점은 다음과 같습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/Screen_Shot_2020-12-26_at_2.57.32_PM_1_33.png)

## 등록/로그인 워크플로우

응용프로그램에 대한 워크플로우를 설정할 때, 사용자가 로그인하지 않은 경우 기본적으로 이 보기가 표시되어야 합니다. 간결함을 위해, 제 예시의 스타일링은 매우 초보적이지만, 독자 분의 스타일링에는 독특합니다!

사용자 로그인 여부에 따라 두 개의 다른 보기를 구분할 수 있도록 몇 가지 기본 라우팅부터 시작하겠습니다. 현재로서는 적절한 후크를 구현할 때까지 자동으로 `false`를 반환하도록 하겠습니다.

사용자가 로그인하지 않은 경우 로그인하거나 등록할 수 있는 보기가 표시됩니다. 사용자가 로그인하면 확인 메시지가 표시됩니다.

```undefined
import React, { useState, useEffect } from 'react';
import { StyleSheet, Text, View, TextInput, Button } from 'react-native';

export default function App() {
  return (
    <Router />
  );
}

function Router() {
  const isUserSignedIn = () => false;

  return (
    isUserSignedIn() ?
      <Text>Congrats! You're signed in.</Text>
      :
      <Account />
  )
}
```

이 `계정` 구성 요소에는 익숙한 것처럼 보이는 로그인/가입 템플릿이 포함됩니다. React Native(원본 반응)에서 이 보기는 다음과 같은 형태로 나타날 수 있습니다.

```undefined
function Account() {
  const [userVal, setUserVal] = useState("");
  const [passVal, setPassVal] = useState("");

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Welcome to React-flix!</Text>
      <TextInput value={userVal} onChangeText={e => setUserVal(e)} style={styles.accountInput} placeholder="Username" />
      <TextInput value={passVal} onChangeText={e => setPassVal(e)} style={styles.accountInput} placeholder="Password"/>
      <View style={ display: "flex", flexDirection: "row", marginTop: 30 }>
        <Button title="Sign In" />
        <Button title="Sign Up" />
      </View>
    </View>
  )
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  accountInput: {
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    width: "75%",
    margin: 10,
    fontSize: 22,
    textAlign: "center"
  },
  title: {
    fontSize: 30,
    fontWeight: "500",
    fontStyle: "italic",
    marginBottom: 30
  }
});
```

이 보기는 다소 기본적이지만, 안전한 기능적 사용자 인증 인터페이스에 필요한 모든 것을 제공합니다. 참고로 이 시점의 응용 프로그램 스크린샷은 다음과 같습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/Screen_Shot_2020-12-26_at_3.47.48_PM_33.png)

## 백엔드 플러그인 방법

이제 Native 앱을 서버 없는 백엔드에 연결하여 사용자 인증 및 토큰 관리를 처리할 예정입니다.

React and React Native에 서버리스 기능을 구현하려는 다양한 라이브러리가 있습니다. 우리가 사용할 것은 이지베이스입니다. 무엇보다도, 이 서비스는 React + 서버를 극도로 직관적이지 않게 만드는 것을 목표로 합니다.

개발자는 서비스의 프로젝트 관리 인터페이스를 활용하여 애플리케이션을 쉽고 효과적으로 확장할 수 있습니다. 이 인터페이스를 통해 프로젝트 사용자를 관리할 수 있습니다. 이 서비스의 웹 애플리케이션(아래 스크린샷)은 easy base-react npm 패키지와 예외적으로 통합된다.

제가 이 패키지를 사용하기로 선택한 이유는 두 가지입니다. 첫째, 하나의 구성 파일로 설치 및 구성 프로세스가 매우 간단합니다.

둘째, 세션 토큰 스토리지 및 네트워킹과 같은 사용자 인증 모듈 구현에 상당한 오버헤드가 있습니다. Easybase Provider 구성 요소는 이러한 오버헤드의 대부분을 처리하므로 우리는 바로 작업할 수 있습니다.

Easybase에 로그인하고 새 테이블을 만듭니다. 계정이 없는 경우 계정을 빨리 만듭니다(무료). 여기에서 다음과 같은 새 프로젝트를 만듭니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/Screen-Shot-2020-12-26-at-4.15.43-PM.png)

그런 다음 여기에서 프로젝트 토큰을 다운로드합니다(나중에 몇 가지 테이블을 만들겠습니다).

![image](https://www.freecodecamp.org/news/content/images/2020/12/Screen-Shot-2020-12-26-at-4.54.34-PM.png)

새로 다운로드한 `ebconfig.js`를 App.js 옆에 있는 React Native 프로젝트 폴더에 다음과 같이 배치합니다.

```undefined
├── android/
├── ios/
├── node_modules/
├── App.js
├── ebconfig.js <---
├── index.js
└── ...
```

다음으로, `App.js`에서 두 가지를 가져올 것입니다.

- "/ebconfig"에서 ebconfig 가져오기
- "Easybase-react"에서 {EasybaseProvider, Easybase} 가져오기

그런 다음 ebconfig를 해당 소품으로 전달하여 이 `Easybase Provider` 컴포넌트로 앱을 포장합니다. 변경 사항은 다음과 같습니다.

```undefined
import ebconfig from "./ebconfig";
import { EasybaseProvider, useEasybase } from "easybase-react";

// ...

export default function App() {
  return (
    <EasybaseProvider ebconfig={ebconfig}>
      <Router />
    </EasybaseProvider>
  )
}

// ...
```

이 시점에서는 use Easybase() 후크를 사용하여 다양한 서버 없는 애플리케이션 기능에 액세스할 수 있습니다. 여기에는 시그인, 시그업, 사용자 속성 설정 등의 기능이 포함된다. 생성된 사용자와 관련 속성이 Easybase의 `Users` 섹션에 나타납니다.io의

use Easybase 후크에 대한 설명서는 여기에서 확인할 수 있습니다. 정보는 Github repo에서도 이용할 수 있다.

이제 버튼의 `on Press` 소품을 `Easybase` 후크에서 제공하는 해당 기능으로 채움으로써 `계정` 구성 요소를 완성할 수 있습니다.

```undefined
function Account() {
  const [userVal, setUserVal] = useState("");
  const [passVal, setPassVal] = useState("");

  const { signIn, signUp } = useEasybase();

  const clearInputs = () => {
    setUserVal("");
    setPassVal("");
  }

  const handleSignInPress = async () => {
    await signIn(userVal, passVal);
    clearInputs();
  }

  const handleSignUpPress = async () => {
    const res = await signUp(userVal, passVal, {
      created_at: new Date().toString
    });
    if (res.success) {
      await signIn(userVal, passVal);
    }
    clearInputs();
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Welcome to React-flix!</Text>
      <TextInput value={userVal} onChangeText={e => setUserVal(e)} style={styles.accountInput} placeholder="Username" />
      <TextInput value={passVal} onChangeText={e => setPassVal(e)} style={styles.accountInput} placeholder="Password"/>
      <View style={ display: "flex", flexDirection: "row", marginTop: 30 }>
        <Button title="Sign In" onPress={handleSignInPress} />
        <Button title="Sign Up" onPress={handleSignUpPress} />
      </View>
    </View>
  )
}
```

마지막으로, 우리는 라우터 컴포넌트에 사용되는 isUserSignedIn 함수를 처리해야 합니다. 다행히 easybase 사용 후크도 같은 이름으로 이 기능을 제공한다. 저걸 꽂기만 하면 조건부 렌더링에 사용할 수 있습니다.

```undefined
function Router() {
  const { isUserSignedIn } = useEasybase();

  return (
    isUserSignedIn() ?
      <Text>Congrats! You're signed in.</Text>
      :
      <Account />
  )
}
```

이와 마찬가지로, React Native에서 안전한 사용자 인증 워크플로우를 구현했습니다. 앱을 닫거나 다시 로드하면 사용자가 대부분의 모바일 플랫폼에서 표준 로그인 상태로 유지됩니다.

### 로그아웃 단추를 추가하는 방법

마지막으로 로그인한 사용자를 위한 로그아웃 버튼을 추가하겠습니다. 그러기 위해서는 현재의 축배를 바꿔야 할 것이다... 서명된 사용자에 대한 텍스트 요소입니다.

다행히 use Easybase 후크는 이 이름을 가진 기능을 가지고 있으므로 다음과 같이 Router 구성 요소를 편집할 수 있습니다.

```undefined
function Router() {
  const { isUserSignedIn, signOut } = useEasybase();

  return (
    isUserSignedIn() ?
      <View style={styles.container}>
        <Text>Congrats! You're signed in.</Text>
        <Button title="Sign Out" onPress={signOut} />
      </View>
      :
      <Account />
  )
}
```

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen_Shot_2021-01-02_at_11.38.36_AM_34.png)

이 새 단추를 클릭하면 현재 사용자의 인증 취소가 처리됩니다. 이렇게 하면 `이지베이스 공급자`의 상태가 변경되고 `isUserSignedIn()`이 거짓으로 반환되므로 앱이 `계정` 구성 요소로 다시 라우팅됩니다.

## 결론

Easybase의 `Users` 섹션으로 이동하면 현재 사용자가 모두 표시됩니다. 참고로 일련의 예제 사용자를 생성한 후의 모습은 다음과 같습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-02-at-11.44.05-AM.png)

이 메뉴에는 사용자를 삭제하거나 해당 속성을 편집할 수 있는 옵션이 있습니다. setUserAttribute()를 사용하여 사용자 속성을 개별적으로 설정할 수도 있습니다. 여기서 `getUserAttributes()` 기능으로 프론트 엔드에서 속성을 검색할 수 있습니다.

React and React Native를 사용한 서버리스에 대한 자세한 내용은 Easybase의 React 페이지를 참조하십시오. 아직 제 데모에 표현되지 않은 다른 주제들에 대한 좋은 디테일이 있습니다만, 그 내용은 나중에 알아보도록 하겠습니다.

읽어주셔서 정말 감사합니다! 이러한 사용자 인증 구현 방법이 React Native로 소프트웨어 개발을 조사하는 사람들에게 도움이 되기를 바랍니다.

다음 기사에서는 이 인증 워크플로우를 서버 없는 데이터베이스와 함께 사용하는 방법에 대해 알아봅니다. 이 데이터베이스에는 사용자 권한 및 개별 레코드 쿼리가 있습니다.