---
layout: post
title: "auth0을 사용하여 Vue 앱에 인증을 추가하는 방법"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/0_j4pVnDlQTDvfWtw_-1.jpeg
tags: undefined
---


Auth0은 애플리케이션에 인증 및 인증 서비스를 추가할 수 있는 유연한 드롭인 솔루션입니다. 사용자의 전자 메일 주소와 암호를 사용하여 사용자를 등록하고 로그인할 수 있도록 Vue 응용 프로그램에 추가하는 것이 얼마나 쉬운지 확인하십시오.

Vue CLI를 사용하여 매우 간단한 Vue 애플리케이션을 만들 예정입니다. Auth0를 사용하여 새 사용자를 등록하거나 기존 사용자를 로그인할 수 있도록 기본 비계 애플리케이션을 수정할 것입니다. 사용자가 로그인하면 정보 페이지를 볼 수 있습니다.

사용자는 Auth0의 전자 메일 및 암호 인증 시스템을 사용하여 응용 프로그램에 등록할 수 있습니다.

저는 Vue CLI를 사용하여 우리가 시작할 프로젝트를 구상할 것입니다. 이를 위해서는 Vue CLI가 시스템에 설치되어 있어야 합니다. 설치되어 있지 않은 경우 다음 명령을 사용하여 전역으로 설치할 수 있습니다.

```undefined
npm install -g @vue/cli
```

이제 Vue CLI를 사용하여 프로젝트를 생성할 수 있습니다. 다음 명령을 사용하여 새 프로젝트를 만듭니다.

```undefined
vue create vue-authentication-auth0
```

사전 설정을 선택하라는 메시지가 표시됩니다. 수동으로 피쳐 선택을 선택한 후 "바벨", "라우터" 및 "Linter/Formatter"를 선택합니다.

라우터에 기록 모드를 사용할지 묻는 메시지가 표시됩니다. "예"를 선택합니다(기본값이어야 함).

원하는 모든 링터를 선택할 수 있지만 이 튜토리얼에서는 "Elint + Pretty"를 선택합니다.

Vue CLI가 완료되면 방금 만든 새 디렉터리로 변경하는 명령과 서버를 시작하는 명령이 제공됩니다. 그 지시를 따르세요. 서버가 시작되면 브라우저를 `localhost:8080`으로 열 수 있습니다. 다음을 확인해야 합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_aULwhJQrKCD0RZ8t.png)

Auth0 계정이 아직 없는 경우 먼저 계정을 만들어야 합니다. 계정을 만들 수 있습니다. 여기서 무료 계정을 만들 수 있습니다.

무료 Auth0 계정을 생성했으면 계정에 로그인합니다. 왼쪽 탐색에서 응용 프로그램을 클릭합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_dx-jheyJRHChE5ET.png)

여기서 Create Application 버튼을 클릭합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_zXLpqqkLENVyAASt.png)

프로그램 이름을 제공하고 만들 프로그램 유형을 지정할 수 있는 대화 상자가 표시됩니다.

내 애플리케이션의 이름은 Vue Authentication Aut0입니다. 지원서의 이름을 원하는 대로 넣을 수 있습니다.

응용프로그램 유형에 대해 단일 페이지 웹 응용프로그램을 선택합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_44vQOJ9golspep06.png)

응용 프로그램을 만든 후 빠른 시작 탭은 가장 널리 사용되는 JavaScript 프레임워크를 사용하여 웹 앱에서 Auth0을 구현하는 방법에 대한 지침을 제공합니다.

애플리케이션에 Vue.js를 사용하고 있으므로 Vue 아이콘을 클릭합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_jGC1dkmWfYbUhXQL.png)

Auth0은 Authentication-As-Service 제품을 구현하는 방법에 대한 자세한 지침을 제공합니다. 이 튜토리얼에서는 이미 만든 Vue 앱에서 해당 지침을 구현합니다.

페이지 상단의 설정 탭을 클릭하여 설정에 액세스할 수 있습니다.

기본 정보 아래에 도메인 및 클라이언트 ID가 표시됩니다. 애플리케이션이 작동하려면 이러한 값을 저장해야 하므로 나중에 다시 살펴보겠습니다.

응용 프로그램 URI 섹션에서 허용된 콜백 URL, 허용된 로그아웃 URL 및 허용된 웹 원본을 정의해야 합니다.

응용 프로그램을 로컬에서 테스트하기 위해 http://localhost:8080의 URL을 사용합니다.

참고: Netlifify 또는 Heroku와 같은 곳에서 프로그램을 호스팅하기로 결정한 경우 호스트된 애플리케이션의 URL로 이러한 설정을 모두 업데이트해야 합니다.

힘내세요>허용된 콜백 URL, 허용된 로그아웃 URL 및 허용된 웹 원본은 http://localhost:8080입니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_nX1DoL-RXVC1x4oD.png)

Vue 응용 프로그램으로 돌아가 다음 명령을 사용하여 Auth0 Client SDK를 추가합니다.

```undefined
npm install @auth0/auth0-spa-js
```

Auth0 SDK를 사용하려면 Vue 응용 프로그램이 시작되기 전에 초기화해야 합니다.

Vue에는 SDK를 초기화하는 데 사용할 수 있는 라이프사이클 후크가 있습니다. App.vue 파일에서 a beforeCreate 후크를 사용할 수 있지만 작동하지 않을 수 있습니다. 이유를 보여드리죠.

다음은 Vue 라이프사이클 후크의 이미지입니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_NuSvkkm1kohKVJbt.png)

BeforeCreate는 Vue 라이프사이클 후크를 처음으로 발사하는 것입니다. 그러나 이 이미지에서는 Vue 응용 프로그램이 새 Vue()를 사용하여 생성된 후 실행된다는 점에 유의하십시오.

Vue 애플리케이션을 생성하는 새 Vue() 전에 Auth0 SDK를 초기화할 수 있어야 합니다. Vue는 Vue 플러그인을 사용하여 이를 수행할 수 있는 메커니즘을 제공합니다.

플러그인을 사용하려면 Vue.use() 명령을 사용하여 플러그인을 호출해야 합니다. 이 명령은 앱을 시작하기 전에 새 Vue()를 호출하여 수행해야 합니다.

우리가 만들 Authentication Wrapper는 실제로 Vue 플러그인이 될 것이다.

src 디렉토리에서 auth라는 새 디렉토리를 생성합니다. 인증 디렉토리 내에 index.js라는 파일을 작성합니다.

빠른 시작 탭에서 제공된 코드를 복사하여 이 파일에 붙여넣습니다. 코드는 다음과 같습니다.

```undefined
import Vue from "vue";
import createAuth0Client from "@auth0/auth0-spa-js";
/** Define a default action to perform after authentication */
const DEFAULT_REDIRECT_CALLBACK = () =>
  window.history.replaceState({}, document.title, window.location.pathname);
let instance;
/** Returns the current instance of the SDK */
export const getInstance = () => instance;
/** Creates an instance of the Auth0 SDK. If one has already been created, it returns that instance */
export const useAuth0 = ({
  onRedirectCallback = DEFAULT_REDIRECT_CALLBACK,
  redirectUri = window.location.origin,
  ...options
}) => {
  if (instance) return instance;
// The 'instance' is simply a Vue object
  instance = new Vue({
    data() {
      return {
        loading: true,
        isAuthenticated: false,
        user: {},
        auth0Client: null,
        popupOpen: false,
        error: null
      };
    },
    methods: {
      /** Authenticates the user using a popup window */
      async loginWithPopup(options, config) {
        this.popupOpen = true;
try {
          await this.auth0Client.loginWithPopup(options, config);
        } catch (e) {
          // eslint-disable-next-line
          console.error(e);
        } finally {
          this.popupOpen = false;
        }
this.user = await this.auth0Client.getUser();
        this.isAuthenticated = true;
      },
      /** Handles the callback when logging in using a redirect */
      async handleRedirectCallback() {
        this.loading = true;
        try {
          await this.auth0Client.handleRedirectCallback();
          this.user = await this.auth0Client.getUser();
          this.isAuthenticated = true;
        } catch (e) {
          this.error = e;
        } finally {
          this.loading = false;
        }
      },
      /** Authenticates the user using the redirect method */
      loginWithRedirect(o) {
        return this.auth0Client.loginWithRedirect(o);
      },
      /** Returns all the claims present in the ID token */
      getIdTokenClaims(o) {
        return this.auth0Client.getIdTokenClaims(o);
      },
      /** Returns the access token. If the token is invalid or missing, a new one is retrieved */
      getTokenSilently(o) {
        return this.auth0Client.getTokenSilently(o);
      },
      /** Gets the access token using a popup window */
getTokenWithPopup(o) {
        return this.auth0Client.getTokenWithPopup(o);
      },
      /** Logs the user out and removes their session on the authorization server */
      logout(o) {
        return this.auth0Client.logout(o);
      }
    },
    /** Use this lifecycle method to instantiate the SDK client */
    async created() {
      // Create a new instance of the SDK client using members of the given options object
      this.auth0Client = await createAuth0Client({
        ...options,
        client_id: options.clientId,
        redirect_uri: redirectUri
      });
try {
        // If the user is returning to the app after authentication..
        if (
          window.location.search.includes("code=") &&
          window.location.search.includes("state=")
        ) {
          // handle the redirect and retrieve tokens
          const { appState } = await this.auth0Client.handleRedirectCallback();
// Notify subscribers that the redirect callback has happened, passing the appState
          // (useful for retrieving any pre-authentication state)
          onRedirectCallback(appState);
        }
      } catch (e) {
        this.error = e;
      } finally {
        // Initialize our internal authentication state
        this.isAuthenticated = await this.auth0Client.isAuthenticated();
        this.user = await this.auth0Client.getUser();
        this.loading = false;
      }
    }
  });
return instance;
};
// Create a simple Vue plugin to expose the wrapper object throughout the application
export const Auth0Plugin = {
  install(Vue, options) {
    Vue.prototype.$auth = useAuth0(options);
  }
};
```

플러그인에 전달된 옵션 객체는 앞서 언급했던 clientId 및 도메인 값을 제공하는 데 사용되며, 나중에 확인하겠다고 했습니다.

응용 프로그램의 루트 디렉터리에 auth_config.json이라는 새 파일을 생성합니다. 도메인 및 클라이언트 ID에 대한 응용 프로그램의 값을 채웁니다. 이 코드를 auth_config.json 파일에 넣고 응용 프로그램 값으로 업데이트해야 합니다.

```undefined
{   
  "domain": "yourAppValuesHere",   
  "clientId": "yourAppValuesHere"
}
```

이 구성 파일에는 Auth0 응용 프로그램과 관련된 민감하지 않은 값이 포함되어 있습니다. 이 파일을 소스 제어에 커밋해서는 안 됩니다. 파일 이름을 .gitignore 파일에 추가하면 됩니다.

.gitignore 파일을 열고 파일에 `auth_config.json`을 추가합니다.

이제 우리는 우리의 플러그인을 만들었기 때문에 Vue에게 그것을 사용하도록 말할 필요가 있다. main.js 파일을 엽니다. auth_config.json 파일에서 플러그인과 도메인 및 클라이언트 ID를 가져오는 다음 두 개의 가져오기 문을 추가하십시오.

```undefined
// Import the Auth0 configuration
import { domain, clientId } from "../auth_config.json";
// Import the plugin here
import { Auth0Plugin } from "./auth";
```

다음은 Vue에게 우리의 플러그인을 사용하라고 말해야 합니다. 가져오기 명령문 뒤에 이 코드를 추가합니다.

```undefined
// Install the authentication plugin here
Vue.use(Auth0Plugin, {
  domain,
  clientId,
  onRedirectCallback: appState => {
    router.push(
      appState && appState.targetUrl
        ? appState.targetUrl
        : window.location.pathname
    );
  }
});
```

auth/index.js 파일의 플러그인 코드를 보면 다음과 같은 두 가지 로그인 방법이 제공됩니다.팝업을 사용하여 리디렉션으로 로그인합니다.

Auth0은 응용 프로그램이 응용 프로그램에 로그인하거나 사용자를 등록하는 데 사용할 수 있는 호스트 로그인 페이지를 제공합니다.

LoginWithRedirect 메서드는 호스팅된 로그인 페이지에 액세스합니다. 즉, 사용자가 로그인 버튼을 클릭하면 URL이 변경되어 사용자가 로그인 세부 정보를 입력할 Auth0 웹 사이트를 가리킵니다. 그들이 성공적으로 인증을 받으면 그들은 우리의 어플리케이션으로 다시 방향을 바꿀 것이다.

이 리디렉션을 수행하지 않으려면 Auth0에서 웹 사이트에 표시되는 팝업을 통해 로그인하거나 사용자를 등록할 수 있는 옵션을 제공합니다.

이 두 가지 로그인 방법을 모두 사용하는 방법을 알려드리겠습니다.

App.vue 파일을 엽니다. 네비게이션에는 현재 홈 페이지와 정보 페이지에 대한 두 개의 항목이 있습니다. 로그인에 두 개의 버튼을 추가해야 합니다. 다음과 같은 모양의 이 코드를 내비게이션에 추가하십시오.

```undefined
<div id="nav">
  <router-link to="/">Home </router-link>|
  <router-link to="/about">About</router-link> |
  <div v-if="!$auth.loading">
    |
    <button @click="login" v-if="!$auth.isAuthenticated">
      Login
    </button>
    |
    <button @click="loginPopup" v-if="!$auth.isAuthenticated">
      Login Popup
    </button>
    |</div>
</div>
```

버튼은 $auth.loading이 거짓인지 확인하는 지시어로 포장되어 있습니다. 당사의 플러그인에 대한 코드를 검토하면 값이 인증됨인 데이터 섹션이 있습니다. 사용자가 Auth0으로 인증할 경우 이 값이 설정됩니다. 사용자가 인증되면 두 개의 로그인 버튼을 표시하지 않습니다.

Div를 추가하면 Home(홈) 및 About(정보) 버튼의 링크 아래 행에 버튼이 나타납니다. 나는 그들이 모두 같은 줄에 있기를 바라며 CSS 스타일을 다음과 같이 업데이트한다.

```undefined
#nav { 
  display: flex; 
  justify-content: center; 
  padding: 30px; 
} 
#nav a { 
  font-weight: bold; 
  color: #2c3e50; 
  padding: 0 5px; 
}
```

이제 응용 프로그램을 보면 두 개의 단추가 표시됩니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_LyHE1bybFhyso-Db.png)

두 버튼은 로그인 및 로그인 팝업을 호출하는 메소드입니다. 지금 실행해 봅시다.

두 가지 메서드를 사용하여 메서드 개체를 추가합니다. 코드는 다음과 같습니다.

```undefined
methods: { 
  login() { 
    this.$auth.loginWithRedirect(); 
  }, 
  loginPopup() { 
    this.$auth.loginWithPopup(); 
  }, 
}
```

이거.$auth는 플러그인의 핸들입니다. 그런 다음 우리는 플러그인에서 사용 가능한 방법을 호출합니다.

이제 응용 프로그램으로 돌아가십시오. 만약 당신이 로그인 단추를 클릭하 Auth0의 호스팅 된 로그인 페이지로 이동되어야 한다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_BopphiRqeQ3ReXlI.png)

Login 팝업 버튼을 클릭하면 프로그램에 로그인 모달이 표시됩니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_e40CPdd19xjobDw-.png)

어떤 항목을 선택하든 로그인 또는 등록할 수 있는 옵션이 있음을 알 수 있습니다. 계정을 만드십시오. 응용 프로그램으로 돌아가면 두 로그인 버튼이 모두 숨겨져 있는 것을 볼 수 있습니다. 플러그인의 isAuthentified 값이 이제 true이기 때문에 이러한 값이 숨겨집니다.

다음 단계는 로그아웃을 구현하는 것입니다. App.vue 파일을 엽니다. 다음과 같은 로그아웃 단추 추가:

```undefined
<button @click="logout" v-if="$auth.isAuthenticated">
  Logout
</button>
```

여기에는 사용자가 현재 인증된 경우에만 이 단추를 표시하라는 지침이 있습니다. 응용 프로그램으로 돌아가면 로그아웃 단추가 표시됩니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_qp0QOUNUP-wz3iUn--1-.png)

이 방법을 추가하여 로그아웃 기능을 구현합니다.

```undefined
logout() { 
  this.$auth.logout(); 
  this.$router.push({ path: '/' }); 
}
```

이 방법으로 플러그인의 로그아웃 함수를 호출합니다. 인증된 사용자만 볼 수 있는 페이지에 있는 경우 사용자를 홈 페이지로 리디렉션합니다.

현재 의 응용 프로그램에는 홈 페이지와 정보 페이지가 있습니다. 새 페이지를 만드는 대신 사용자가 로그인한 경우에만 정보 페이지를 표시하도록 설정합니다.

사용자가 로그인한 경우에만 탐색에 정보 페이지를 표시하려고 합니다. 로그아웃 버튼을 표시하는 데 사용하는 것과 동일한 지시어를 사용하여 탐색의 정보 페이지에 표시합니다. 다음과 같이 탐색을 업데이트합니다.

```undefined
<router-link v-if="$auth.isAuthenticated" to="/about">About</router-link>
```

사용자가 현재 인증되지 않은 경우 탐색에서 정보 페이지 링크를 숨겼습니다. 그러나 사용자는 페이지로 직접 이동하려는 URL을 입력할 수 있습니다. 인증되지 않은 사용자가 해당 페이지에 액세스할 수 있음을 나타냅니다. 경로 가드를 사용하면 이 문제를 피할 수 있습니다.

auth 디렉터리에서 authGuard.js라는 새 파일을 생성합니다.

파일에 이 코드를 추가합니다.

```undefined
import { getInstance } from "./index";
export const authGuard = (to, from, next) => {
  const authService = getInstance();
const fn = () => {
    // If the user is authenticated, continue with the route
    if (authService.isAuthenticated) {
      return next();
    }
// Otherwise, log in
    authService.loginWithRedirect({ appState: { targetUrl: to.fullPath } });
  };
// If loading has already finished, check our auth state using `fn()`
  if (!authService.loading) {
    return fn();
  }
// Watch for the loading property to change before we check isAuthenticated
  authService.$watch("loading", loading => {
    if (loading === false) {
      return fn();
    }
  });
};
```

이 코드는 사용자가 현재 인증되었는지 확인합니다. 그렇지 않은 경우 사용자가 로그인할 수 있는 Auth0 호스트 로그인 페이지가 나타납니다. 사용자가 로그인하지 못하거나 성공적으로 로그인할 수 없는 경우, 라우트 가드가 있는 액세스하려는 페이지에서 사용자를 리디렉션합니다.

이제 Vue 라우터에 이 경로 가드를 구현해 보겠습니다. 라우터 디렉토리에서 index.js 파일을 엽니다.

파일 맨 위에 방금 만든 authGuard 파일에 대한 가져오기를 추가합니다.

```undefined
import { authGuard } from "../auth/authGuard";
```

다음에는 경로 경비원을 노선에 추가해야 합니다. /정보 라우트를 다음과 같이 업데이트합니다.

```undefined
{ 
  path: '/about', 
  name: 'About', 
  component: () => import(/* webpackChunkName: "about" */ '../views/About.vue'), 
  beforeEnter: authGuard 
}
```

응용 프로그램으로 돌아가십시오. 현재 인증되지 않은 경우 프로그램에 로그인합니다. 탐색에서 정보 항목을 볼 수 있습니다) 이제 응용 프로그램을 로그아웃합니다. 수동으로 url/about으로 이동합니다. Auth0 호스팅된 로그인 페이지로 리디렉션해야 합니다.

축하합니다! Vue 응용 프로그램에 Auth0 인증을 성공적으로 추가했습니다.

여기 GitHub 계정에 완전한 코드가 있습니다. 코드를 받으시면 제 부탁 하나 들어주시고 제 레포를 띄워주세요. 감사합니다!

다른 인증 방법을 사용하여 Vue 응용 프로그램에 Authentication을 추가하는 방법에 대한 후속 기사를 여러 개 작성했습니다.

Firebase를 인증에 사용하려면 이 문서를 참조하십시오.

AWS Amply를 인증에 사용하려면 이 문서를 참조하십시오.

Auth0은 응용 프로그램에 추가할 수 있는 Authentication-As-Service 제품입니다. 이 제품은 매우 사용하기 쉬운 인증을 제공합니다.

이 기사 잘 보셨기를 바랍니다. 마음에 드시면 공유해 주세요. 읽어주셔서 감사합니다.

원래 2020년 12월 31일 https://www.jenniferbland.com에서 출판되었다.