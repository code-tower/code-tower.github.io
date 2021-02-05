---
layout: post
title: "Firebase를 사용하여 Vue 앱에 인증을 추가하는 방법"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/0_zPahR_9e795a1Vpp-1.jpeg
tags: undefined
---


Firebase는 Vue.js 응용 프로그램에 인증을 추가하는 매우 간단하고 빠른 방법을 제공합니다. 이 기사에서는 사용자의 전자 메일과 암호를 사용하여 응용 프로그램에 등록하는 것이 얼마나 쉬운지 보여드리겠습니다.

Vue CLI를 사용하여 매우 간단한 Vue 애플리케이션을 만들 예정입니다. 기본 비계 어플리케이션을 수정하여 로그인한 사람에게만 표시되는 새로운 사용자, 로그인 페이지, 대시보드 페이지로 등록할 수 있도록 하겠습니다.

사용자는 Firebase의 전자 메일 및 암호 인증 시스템을 사용하여 애플리케이션에 등록할 수 있습니다. 등록 및 로그인하면 대시보드 페이지가 표시됩니다.

저는 Vue CLI를 사용하여 우리가 시작할 프로젝트를 구상할 것입니다. 이를 위해서는 Vue CLI가 시스템에 설치되어 있어야 합니다. 설치되어 있지 않은 경우 다음 명령을 사용하여 전역으로 설치할 수 있습니다.

```undefined
npm install -g @vue/cli
```

이제 Vue CLI를 사용하여 프로젝트를 생성할 수 있습니다. 다음 명령을 사용하여 새 프로젝트를 만듭니다.

```undefined
vue create vue-firebase-auth-tutorial
```

사전 설정을 선택하라는 메시지가 표시됩니다. 수동으로 피쳐 선택을 선택한 후 "바벨", "라우터" 및 "Linter/Formatter"를 선택합니다.

라우터에 기록 모드를 사용할지 묻는 메시지가 표시됩니다. "예"를 선택합니다(기본값이어야 함).

원하는 모든 링터를 선택할 수 있지만 이 튜토리얼에서는 "Elint + Pretty"를 선택합니다.

Vue CLI가 완료되면 방금 만든 새 디렉터리로 변경하는 명령과 서버를 시작하는 명령이 제공됩니다. 그 지시를 따르세요.

서버가 시작되면 브라우저를 `localhost:8080`으로 열 수 있습니다. 다음을 확인해야 합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/vueapp.png)

이 튜토리얼에서는 이미 Firebase 계정을 생성했다고 가정합니다. 그렇지 않은 경우 계속하기 전에 이 작업을 수행해야 합니다.

우리는 우리의 응용 프로그램에서 Firebase SDK를 사용하여 인증 기능을 제공할 것입니다. 다음 명령을 사용하여 프로그램에 Firebase를 설치할 수 있습니다.

```undefined
npm install firebase
```

다음 단계는 Firebase 콘솔에 프로젝트를 추가하는 것입니다. Firebase 콘솔에 로그인합니다. 새 프로젝트를 추가하려면 버튼을 클릭하십시오.

![image](https://www.freecodecamp.org/news/content/images/2021/01/addProject.png)

프로젝트에 Google Analytics를 추가할 수 있지만 이 튜토리얼에서는 추가하지 않습니다. Create Project 버튼을 클릭합니다.

Firebase가 새 프로젝트를 생성했으면 앱에 Firebase를 추가해야 합니다. 웹 아이콘을 클릭합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/addFirebase.png)

앱의 닉네임을 입력하라는 메시지가 표시됩니다. Vue Firebase Auth Tutorial이라는 닉네임을 입력했습니다. 닉네임을 입력한 후 "앱 등록" 버튼을 클릭합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/registerApp.png)

2단계에서는 애플리케이션에 Firebase SDK를 추가하는 방법에 대한 지침을 제공합니다. 앱을 초기화하려면 firebaseConfig와 라인만 복사하면 됩니다.

main.js 파일을 엽니다. Vue 응용 프로그램에서 Firebase를 초기화합니다. 기존 가져오기 줄 아래의 firebaseConfig 및 줄에 붙여넣어 앱을 초기화합니다. Firebase에 대한 가져오기를 추가해야 합니다. main.js 파일은 다음과 같아야 합니다.

```undefined
import Vue from "vue";
import App from "./App.vue";
import router from "./router";
import firebase from "firebase";

var firebaseConfig = {
  apiKey: "YourConfigHere",
  authDomain: "YourConfigHere",
  projectId: "YourConfigHere",
  storageBucket: "YourConfigHere",
  messagingSenderId: "YourConfigHere",
  appId: "YourConfigHere"
};
// Initialize Firebase
firebase.initializeApp(firebaseConfig);

Vue.config.productionTip = false;

new Vue({
  router,
  render: h => h(App)
}).$mount("#app");
```

브라우저에서 Firebase 콘솔을 엽니다. 콘솔에서 방금 만든 프로젝트를 찾아 클릭합니다.

왼쪽 탐색의 맨 위에서 인증을 클릭합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_kYC_j73ZH7guuLxQ.png)

시작 단추를 누릅니다.

인증 메뉴에서 "로그인 방법" 탭을 클릭합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_eFqUqK5d8_jt6O_v.png)

첫 번째 항목 "전자 메일/암호" 위에 마우스를 놓으십시오. 대화 상자를 열려면 연필 아이콘을 클릭합니다. 사용을 선택합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_3z3Aj1_Sut_C5WHg.png)

저장 단추를 누릅니다. 이제 전자 메일 주소와 암호를 사용하여 사용자를 만들고 인증하는 기능을 추가했습니다.

Vue Router로 애플리케이션을 만들 때 애플리케이션을 위한 두 가지 경로가 자동으로 생성되었습니다. 즉, Home(홈) 및 About(정보)입니다. 홈을 응용 프로그램의 로그인으로 사용합니다. About(정보) 페이지를 사용하여 응용 프로그램의 새 사용자로 등록합니다.

등록된 사용자가 애플리케이션에 로그인할 때 대시보드 페이지를 표시하려고 합니다. 또한 사용자가 프로그램에서 로그아웃할 수 있는 방법도 제공하고자 합니다. 현재 이 두 가지 옵션을 모두 응용 프로그램에서 사용할 수 없으므로 지금 추가하겠습니다.

App.vue 파일을 엽니다. 현재 탐색에는 Home(홈)과 About(정보)에 대한 두 개 있습니다. About be register(등록될 정보)를 변경하고 Dashboard(대시보드) 및 Logout(로그아웃)에 대해 두 개의 새 항목을 추가합니다. 다음과 같이 보이도록 네비게이션 업데이트:

```undefined
<div id="nav">
  <router-link to="/">Home</router-link> |
  <router-link to="/register">Register</router-link> |
  <router-link to="/dashboard">Dashboard</router-link> |
  <button @click="logout">Logout</button>
</div>
```

로그아웃 버튼을 클릭하면 로그아웃 메서드가 호출됩니다. 우리는 나중에 그것을 정의할 것이다.

홈을 엽니다.보기 폴더의 vue 파일입니다. 템플릿 섹션의 HTML 코드를 모두 삭제합니다. 매우 기본적인 로그인 양식을 제공하는 이 코드로 대체합니다. 코드는 다음과 같습니다.

```undefined
<div>   
  <form @submit.prevent="login">     
    <h2>Login</h2>     
    <input       
      type="email"       
      placeholder="Email address..."       
      v-model="email"     
    />     
    <input       
      type="password"       
      placeholder="password..."       
      v-model="password"     
    />     
    <button type="submit">
       Login
    </button>   
  </form> 
</div>
```

이제 당사의 애플리케이션을 보시면 다음과 같은 로그인 양식을 홈 페이지에 보실 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_WZxgr8K-wj5VSgpg.png)

우리 양식은 입력란과 버튼이 서로 닿아 조금 붐빈다. 우리는 CSS 스타일링을 추가해서 이것을 바꿀 수 있습니다. 우리는 홈에서 CSS 스타일링을 추가할 수 있습니다.뷰 파일

사용자 등록에 동일한 양식을 사용할 예정이기 때문에 해당 구성 요소에서 동일한 CSS 스타일링을 복제해야 할 것 같습니다. 대신 App.vue 파일에 스타일을 넣으면 로그인 양식과 등록 양식을 모두 스타일링할 수 있습니다.

App.vue 파일을 엽니다. 스타일에서 다음을 추가합니다.

```undefined
input {   
  margin-right: 20px; 
}
```

이제 로그인 양식이 더 좋아졌습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_bM6cZIRgjfNfrvqd.png)

정보를 엽니다.보기 폴더의 vue 파일입니다. 홈에서 HTML 코드를 복사할 수 있습니다.파일을 vue하여 이 파일에 붙여넣습니다. Login to Register(등록)의 모든 참조를 변경합니다. 당신의 정보.vue 파일은 다음과 같아야 합니다.

```undefined
<div>
  <form @submit.prevent="register">
    <h2>Register</h2>
    <input
      type="email"
      placeholder="Email address..."
      v-model="email"
    />
    <input
      type="password"
      placeholder="password..."
      v-model="password"
    />
    <button type="submit">Register</button>
  </form>
</div>
```

현재 등록 페이지를 표시할 URL은 /about입니다. 그것을 /등록으로 바꾸자. 라우터 폴더에서 index.js 파일을 엽니다. 두 번째 경로를 변경해 //등록하려고 합니다. 경로 배열은 다음과 같아야 합니다.

```undefined
const routes = [
    {
        path: '/',
        name: 'Home',
        component: Home,
    },
    {
        path: '/register',
        name: 'Register',
        component: () =>
            import(/* webpackChunkName: "about" */ '../views/About.vue'),
    },
];
```

이 파일에 있는 동안 대시보드 구성 요소를 표시하는 항목을 추가해 보겠습니다. /대시보드를 표시할 세 번째 경로를 추가합니다. 이제 경로 배열은 다음과 같습니다.

```undefined
const routes = [
    {
        path: '/',
        name: 'Home',
        component: Home,
    },
    {
        path: '/register',
        name: 'Register',
        component: () =>
            import(/* webpackChunkName: "about" */ '../views/About.vue'),
    },
    {
        path: '/dashboard',
        name: 'Dashboard',
        component: () =>
            import(/* webpackChunkName: "dashboard" */ '../views/Dashboard.vue'),
    },
];
```

대시보드라는 새 파일을 만듭니다.뷰 폴더에 vue를 입력합니다. 이 페이지는 프로그램에 로그온한 사용자만 볼 수 있습니다.

템플릿 섹션에서 다음과 같은 HTML 코드를 추가합니다.

```undefined
<div>
  <h2>Dashboard</h2>
  <p>This page is only visible to users that are currently logged in</p>
</div>
```

아까 정보 업데이트할 때.사용자를 등록하기 위한 vue 파일 우리는 Register라는 메서드에 대한 호출을 받았다. 신규 사용자 등록을 위해 기능을 추가해야 합니다.

먼저 암호 기반 계정을 만드는 방법에 대한 Firebase 설명서를 확인해 보겠습니다. Firebase Auth에는 Createuser라는 메서드가 있습니다.전자 메일 및 암호와 함께. 사용자의 전자 메일과 암호를 입력해야 합니다. 이 메서드는 사용자를 등록하고 사용자 개체를 반환하거나 오류 메시지를 반환합니다. 이제 이 방법을 실행해 봅시다.

정보를 엽니다.뷰 파일 데이터 개체에 이메일과 암호를 추가해야 합니다. 스크립트 섹션에서 다음 데이터 개체를 추가합니다.

```undefined
data() { 
  return { 
    email: '', 
    password: '', 
  }; 
},
```

다음으로 레지스터라는 하나의 메서드로 메서드 개체를 추가합니다. 우리는 말 그대로 이 방법에 대한 Firebase 문서의 예제를 복사할 수 있습니다. 문서에서 코드를 다음과 같이 변경해야 합니다.

- 사용자 개체를 사용하지 않습니다.
- 로그인 실패 시 알림 표시
- 사용자가 등록된 경우 로그인 페이지로 리디렉션

다음은 레지스터 방법에 대한 코드입니다.

```undefined
methods: {
  register() {
    firebase
      .auth()
      .createUserWithEmailAndPassword(this.email, this.password)
      then(() => {
        alert('Successfully registered! Please login.');
        this.$router.push('/');
      })
      .catch(error => {
        alert(error.message);
      });
  },
},
```

응용 프로그램에 대한 첫 번째 사용자 등록을 테스트해 보겠습니다. 탐색에서 Register(등록)를 클릭합니다. 이메일 주소와 암호를 입력하고 Register(등록) 버튼을 클릭합니다.

사용자가 성공적으로 등록되었으면 알림을 받고 로그인 페이지로 리디렉션해야 합니다.

등록이 실패하면 오류 메시지와 함께 경고가 표시됩니다.

사용자가 성공적으로 등록되었는지 확인하려면 Firebase 콘솔로 이동하여 프로젝트를 클릭합니다. 왼쪽 탐색에서 인증을 클릭합니다. 그런 다음 Users 탭을 클릭합니다. 사용자의 목록이 표시됩니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_zBdB2l8pNamJpc-h.png)

이제 애플리케이션에 대한 신규 사용자 등록을 성공적으로 구현했으므로 사용자가 로그인할 수 있는 기능을 구현해야 합니다.

우리는 새로운 사용자를 등록하기 위해 Firebase에서 제공한 코드를 사용했습니다. Firebase 설명서 페이지에서 이메일 주소와 암호를 사용하여 사용자를 로그인하는 샘플 코드를 제공합니다. 우리가 사용할 Firebase 인증 방법은 InWithEmailAndPassword입니다.

Register와 마찬가지로 샘플 코드도 동일하게 변경할 것입니다. 성공적으로 로그인한 경우 사용자에게 알리고 대시보드 페이지로 리디렉션합니다.

로그인에 실패하면 오류 메시지와 함께 경고가 표시됩니다.

다음은 가정에서 사용해야 하는 로그인 방법입니다.뷰 파일

```undefined
methods: {
  login() {
    firebase
      .auth()
      .signInWithEmailAndPassword(this.email, this.password)
      .then(() => {
        alert('Successfully logged in');
        this.$router.push('/dashboard');
      })
      .catch(error => {
        alert(error.message);
      });
  },
},
```

사용자가 로그인하지 않은 경우 /대시보드로 이동할 수 없도록 합니다. /대시보드용 경로 보호대를 추가하면 이 작업을 수행할 수 있습니다.

라우터 폴더에서 index.js 파일을 엽니다. 인증이 필요하다는 메타 키를 /register 경로에 추가할 것입니다. 업데이트된 경로는 다음과 같습니다.

```undefined
{
  path: '/dashboard',
  name: 'Dashboard',
  component: () =>
    import(/* webpackChunkName: "dashboard" */ '../views/Dashboard.vue'),
  meta: {
    authRequired: true,
  },
},
```

Vue Router가 경로를 처리하기 전에 각각 앞에 메서드가 있습니다. 우리는 메타값을 확인하여 경로가 인증을 필요로 하는지 확인할 수 있습니다.

인증이 필요한 경우 사용자가 로그인했는지 여부를 확인할 수 있어야 합니다. 다행히도 Firebase Auth에 현재 사용자 개체가 있습니다. 사용자가 로그인했는지 여부를 확인하는 데 사용합니다.

현재 로그인되어 있는 경우 Dashboard 페이지가 표시됩니다.

그렇지 않은 경우 사용자가 로그인해야 한다는 알림이 표시되고 사용자가 로그인할 수 있도록 홈 페이지로 리디렉션됩니다.

코드는 다음과 같습니다.

```undefined
router.beforeEach((to, from, next) => {
  if (to.matched.some(record => record.meta.authRequired)) {
    if (firebase.auth().currentUser) {
      next();
    } else {
      alert('You must be logged in to see this page');
      next({
        path: '/',
      });
    }
  } else {
    next();
  }
});
```

응용 프로그램에 마지막으로 추가해야 할 것은 로그아웃 방법입니다. Firebase Auth는 우리가 사용할 SignOut 방법을 제공합니다.

App.vue 파일을 엽니다. 사용자를 로그아웃합니다. 성공하면 알림이 수신되고 홈 페이지로 리디렉션됩니다.

로그아웃에 실패하면 오류 메시지가 포함된 경고를 표시하고 해당 경고를 홈 페이지로 리디렉션합니다.

로그아웃 방법에 대해 이 코드를 추가합니다.

```undefined
methods: {
  logout() {
    firebase
      .auth()
      .signOut()
      .then(() => {
        alert('Successfully logged out');
        this.$router.push('/');
      })
      .catch(error => {
        alert(error.message);
        this.$router.push('/');
      });
  },
},
```

위의 코드에서, 우리는 Firebase를 사용하고 있지만, 우리의 index.js 파일에 그것에 대한 어떠한 참조도 가지고 있지 않다. 우리는 그것을 추가해야 한다. 기존 가져오기 줄이 있는 파일 맨 위로 스크롤합니다. 다음 행 추가:

```undefined
import firebase from 'firebase';
```

이제 추가가 완료되면 새 사용자를 등록하는 연습을 할 수 있습니다. 그런 다음 해당 사용자로 로그인하고 대시보드 페이지로 리디렉션되는지 확인합니다. 그런 다음 로그아웃하고 홈 페이지로 리디렉션되는지 확인합니다.

축하합니다 – Vue 애플리케이션에 Firebase Authentication을 성공적으로 추가했습니다!

여기 GitHub 계정에 완전한 코드가 있습니다. 코드를 받으시면 제 부탁 하나 들어주시고 제 레포를 띄워주세요. 감사합니다!

다른 인증 방법을 사용하여 Vue 응용 프로그램에 Authentication을 추가하는 방법에 대한 후속 기사를 여러 개 작성했습니다.

Auth0을 인증에 사용하려면 이 문서를 읽어 보십시오.

AWS Amply를 인증에 사용하려면 이 문서를 참조하십시오.

Firebase는 Vue 애플리케이션에 인증을 추가하는 매우 효율적인 방법입니다. 이 기능을 사용하면 직접 백엔드 서비스를 작성하고 인증을 구현하지 않고도 인증을 추가할 수 있습니다.

이 기사 잘 보셨기를 바랍니다. 마음에 드시면 공유해 주세요. 읽어주셔서 감사합니다.

원래 2020년 12월 28일 https://www.jenniferbland.com에서 출판되었다.

## 제니퍼 블랜드