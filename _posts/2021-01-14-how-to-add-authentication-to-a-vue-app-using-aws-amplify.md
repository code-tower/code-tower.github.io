---
layout: post
title: "AWS Amplify를 사용하여 Vue 앱에 인증을 추가하는 방법
 "
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/0_QrOUXeTdCaxjv6o_-1.jpeg
tags: undefined
---


이 기사에서는 Vue CLI를 사용하여 매우 간단한 Vue 애플리케이션을 만들 것입니다.
 새 사용자로 등록 할 수있는 양식, 로그인 페이지 및 로그인 한 사용자에게만 표시되는 대시 보드 페이지를 제공하도록 기본 스캐 폴드 애플리케이션을 수정합니다.
 

사용자는 이메일과 비밀번호를 사용하여 등록 할 수 있습니다.
 등록하고 로그인하면 대시 보드 페이지가 표시됩니다.
 

Vue CLI를 사용하여 시작할 프로젝트를 스캐 폴드 할 것입니다.
 이를 위해서는 시스템에 Vue CLI가 설치되어 있어야합니다.
 설치되어 있지 않은 경우 다음 명령을 사용하여 전역 적으로 설치할 수 있습니다.
 

```undefined
npm install -g @vue/cli
```

이제 Vue CLI를 사용하여 프로젝트를 만들 수 있습니다.
 다음 명령을 사용하여 새 프로젝트를 만듭니다.
 

```undefined
vue create vue-amplify-auth-tutorial
```

사전 설정을 선택하라는 메시지가 표시됩니다.
 "수동으로 기능 선택"을 선택한 다음 "바벨", "라우터"및 "Linter / 포맷터"를 선택합니다.
 

라우터에 기록 모드를 사용할 것인지 묻는 메시지가 표시됩니다.
 "예"를 선택합니다 (기본값이어야 함).
 

linter의 경우 "오류 방지 기능 만있는 ESLint"를 선택합니다.
 

Vue CLI가 완료되면 방금 생성 한 새 디렉토리로 변경하라는 명령과 서버를 시작하는 명령이 제공됩니다.
 그 지시를 따르십시오.
 

서버가 시작되면 브라우저에서`localhost : 8080`을 열 수 있습니다.
 다음이 표시되어야합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_S9E-Jj_1zY76iZBj.png)

AWS Amplify는 함께 또는 단독으로 사용할 수있는 도구 및 서비스 세트를 포함하는 Amazon에서 생성 한 오픈 소스 프레임 워크입니다.
 

도구 중 하나는 Amplify Auth입니다.
 Amplify Auth를 사용하면 보안 인증을 빠르게 설정하고 사용자가 애플리케이션에서 액세스 할 수있는 항목을 제어 할 수 있습니다.
 

Amplify 프레임 워크는 Amazon Cognito를 기본 인증 공급자로 사용합니다.
 Amazon Cognito는 사용자 등록, 인증, 계정 복구 및 기타 작업을 처리하는 강력한 사용자 디렉터리 서비스입니다.
 

시작하려면 여기에서 AWS 계정을 만들어야합니다.
 AWS 계정이없는 경우 여기의 지침에 따라 계정을 만드십시오.
 

Amplify CLI는 앱에 대한 AWS 클라우드 서비스를 생성하기위한 통합 도구 체인입니다.
 다음 명령을 사용하여 전역 적으로 설치할 수 있습니다.
 

```undefined
npm install -g @aws-amplify/cli
```

다음으로 다음 명령을 실행하여 Amplify를 구성해야합니다.
 

```undefined
amplify configure
```

이 명령은 새 브라우저 창을 열고 AWS 콘솔에 로그인하도록 요청합니다.
 로그인 한 후 터미널로 돌아가 `Enter`를 누릅니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_SBiQgDy2bw0OGeX3.png)

AWS 리전을 지정하라는 메시지가 표시됩니다.
 가장 가까운 지역을 선택하십시오.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_Wx3wr2Ohnd7_2RAG.png)

새 IAM 사용자의 사용자 이름을 지정해야합니다.
 Enter 키를 눌러 사용할 수있는 기본 이름을 제공하거나 자신의 이름을 지정할 수 있습니다.
 제 사용자를`auth-demo`라고 부르겠습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_z0qKKxKSjp_1K98H.png)

`Enter`를 누르면 브라우저로 돌아갑니다.
 

다음 : 권한 버튼을 클릭합니다.
 

다음 : 태그 버튼을 클릭합니다.
 

다음 : 검토 버튼을 클릭합니다.
 

사용자 생성 버튼을 클릭합니다.
 

이제 터미널로 돌아가서`Enter`를 눌러 계속하십시오.
 

방금 만든 사용자의`accessKeyId`를 입력하고`Enter`를 누릅니다.
 

방금 생성 한 사용자의 `secretAcessKey`를 입력하고 `Enter`를 누릅니다.
 

프로필 이름을 입력하라는 메시지가 표시됩니다.
 `Enter`를 눌러 제공된 값 (기본값)을 수락합니다.
 

모든 것이 완료되면 새 사용자가 성공적으로 설정되었다는 메시지가 터미널에 표시됩니다.
 

이제 실행중인 Vue 앱이 있으므로 앱을 지원하는 데 필요한 백엔드 서비스를 만들 수 있도록 Amplify를 설정할 차례입니다.
 Vue 애플리케이션의 루트에서 다음을 실행하십시오.
 

```undefined
amplify init
```

Vue 애플리케이션에 인증 서비스를 추가해야합니다.
 Vue 애플리케이션의 루트 디렉토리에 다음 명령을 입력하십시오.
 

```undefined
amplify add auth
```

Amplify를 초기화하면 애플리케이션에 대한 몇 가지 정보를 입력하라는 메시지가 표시됩니다.
 프로젝트 이름을 입력하십시오.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_0Q7RiIPnBCAo90Kf.png)

백엔드 환경 이름을`dev`로 설정합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_SMbI1iNM5XELFdfp.png)

때때로 CLI는 파일을 편집하라는 메시지를 표시합니다.이 편집기를 사용하여 해당 파일을 엽니 다.
 선호하는 코드 편집기 소프트웨어를 선택하십시오.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_juPUaS2SIkR0UnxL.png)

Amplify는이 백엔드 환경에 연결할 프런트 엔드 애플리케이션에 대한 구성 파일을 제공합니다.
 Vue는 JavaScript를 기반으로하므로 여기서 선택하겠습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_enPauC_uAMYzoDFV.png)

Vue를 사용하고 있으므로 JavaScript 프레임 워크로 선택합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_xOxbC5xEGdudv-ej.png)

Vue CLI는`. / src` 폴더 아래에 프로젝트의 소스 파일을 설정합니다.
 소스 디렉토리 경로로`src`를 선택하십시오.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_iLN4pnHKGUGB3tCz.png)

프로젝트를 호스팅 할 준비가되면 Vue는 공용으로 사용할 수있는 웹 사이트를`dist`라는 폴더에 생성합니다.
 이것이 기본값이므로 계속하려면 `Enter`를 누르기 만하면됩니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_u1tw63qKuNAsPJ9B.png)

Amplify의 자동화 된 배포는 게시 용 애플리케이션을 구축하는 데 필요한 단계를 알아야합니다.
 여기에서는 Vue CLI의 기본 빌드 스크립트로 설정합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_SqFEoy03S2eingpb.png)

Amplify가 개발 모드에서 애플리케이션을 실행해야하는 경우 개발 서버를 시작하는 방법을 알아야합니다.
 다시 한 번 Vue CLI의 기본 스크립트를 사용합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_WR5XjxUw9TmYlTUv.png)

마지막으로 Amplify는 백엔드 서비스 생성을 시작할 수 있도록 연결할 AWS 계정이 필요합니다.
 이전에`amplify configure` 명령으로 생성 한 프로필입니다.
 `y`를 입력하고 `Enter`를 눌러 `예`를 선택합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_oTD19eyWt9KdCb6J.png)

계속해서 목록에서 프로필을 선택하고 `Enter`를 누릅니다.
 Amplify는 이제 백엔드 프레임 워크 배포를 시작합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/0_fX2wHxziZZil6sJ3.png)

새로운 Amplify 프로젝트를 초기화하면 몇 가지 일이 발생합니다.
 

- 백엔드 정의를 저장하는`amplify`라는 최상위 디렉토리를 생성합니다.
 자습서 중에 인증, GraphQL API, 저장소 및 API에 대한 권한 부여 규칙과 같은 기능을 추가합니다.
 기능을 추가하면`amplify` 폴더가 백엔드 스택을 정의하는 코드로서의 인프라 템플릿으로 확장됩니다.
 코드로서의 인프라는 복제 가능한 백엔드 스택을 생성하는 모범 사례 방법입니다.
 
- Amplify로 생성 한 서비스에 대한 모든 구성을 보유하는`src` 디렉토리에`aws-exports.js`라는 파일을 생성합니다.
 이것이 Amplify 클라이언트가 백엔드 서비스에 대한 필요한 정보를 얻을 수있는 방법입니다.
 
- `.gitignore` 파일을 수정하여 생성 된 파일을 무시 목록에 추가합니다.
 
- `amplify console`을 실행하여 액세스 할 수있는 AWS Amplify Console에서 클라우드 프로젝트가 생성됩니다.
 콘솔은 백엔드 환경 목록, Amplify 범주 별 프로비저닝 된 리소스에 대한 딥 링크, 최근 배포 상태 및 백엔드 리소스를 승격, 복제, 가져 오기 및 삭제하는 방법에 대한 지침을 제공합니다.
 

서비스를 배포하려면`push` 명령어를 실행하세요.
 

Vue 애플리케이션에 Amplify 종속성을 설치해야합니다.
 다음 명령으로 설치할 수 있습니다.
 

```undefined
npm install aws-amplify
```

Vue 애플리케이션에 Amplify를 추가해야합니다.
 `main.js` 파일을 열고 마지막 가져 오기 행 뒤에 다음을 추가합니다.
 

```undefined
import Amplify from 'aws-amplify';
import awsconfig from './aws-exports'; 
Amplify.configure(awsconfig);
```

위의 코드는 Amplify를 성공적으로 구성합니다.
 Amplify CLI를 사용하여 카테고리를 추가 또는 제거하고 백엔드 구성을 업데이트하면`aws-exports.js`의 구성이 자동으로 업데이트됩니다.
 

신규 사용자가 애플리케이션에 등록 할 수있는 페이지가 필요합니다.
 보기 폴더에서`Register.vue`라는 새 파일을 만듭니다.
 

이 새 페이지를 경로에 추가 한 다음 내비게이션에 표시해야합니다.
 `router` 폴더에서`index.js` 파일을 엽니 다.
 이것을 경로 배열에 추가하십시오.
 

```undefined
{
    path: '/register',
    name: 'Register',
    component: () =>
        import(/* webpackChunkName: "register" */ '../views/Register.vue'),
},
```

이제 이것을 탐색에 추가하십시오.
 `App.vue` 파일을 열고 탐색에`Register` 항목을 추가합니다.
 탐색은 다음과 같아야합니다.
 

```undefined
<div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> |
    <router-link to="/register">Register</router-link>
</div>
```

`Register.vue` 파일로 돌아갑니다.
 이 페이지에는 사용자가 새 사용자로 등록하기위한 이메일과 비밀번호를 입력 할 수있는 양식이 있습니다.
 템플릿 섹션에 입력해야하는 코드는 다음과 같습니다.
 

```undefined
<div class="container">
    <form @submit.prevent="register">
        <h2>Register</h2>
        <input
            type="email"
            v-model="email"
            placeholder="Email address..."
        />
        <input
            type="password"
            v-model="password"
            placeholder="password..."
        />
        <button>Register</button>
    </form>
</div>
```

양식을 보면 두 개의 입력 필드와 버튼이 바로 옆에 있습니다.
 

세 필드 사이에 간격을 추가 하시겠습니까?
 이 페이지에 CSS를 추가 할 수 있지만이 페이지에만 적용됩니다.
 다음에 만들 로그인 페이지에서이 양식을 다시 사용할 것입니다.
 

두 페이지 모두에서 작동하는 스타일을 얻으려면`App.vue` 파일에 다음 CSS를 넣으십시오.
 `App.vue` 파일을 열고 다음 스타일을 추가합니다.
 

```undefined
:input {   
  margin-right: 10px; 
}
```

`Register.vue` 파일로 돌아갑니다.
 사용자가 이메일 및 비밀번호에 입력하는 값을 캡처하고 있으므로 데이터 개체에 추가해야합니다.
 다음과 같이 보이도록 데이터 개체에 추가합니다.
 

```undefined
data() { 
  return { 
    email: '', 
    password: '', 
  }; 
},
```

사용자가 양식을 제출하면`register` 메소드를 호출합니다.
 해당 방법의 코드는 다음과 같습니다.
 

```undefined
async register() {
    try {
        await Auth.signUp({
            username: this.email,
            password: this.password,
        });
        alert('User successfully registered. Please login');
    } catch (error) {
        alert(error.message);
    }
},
```

이 방법은 우리가 설치 한`aws-amplify` 패키지의`Auth`를 사용합니다.
 스크립트 섹션의 시작 부분에이 가져 오기를 추가하십시오.
 

```undefined
import { Auth } from 'aws-amplify';
```

이제 애플리케이션을 열고 새 사용자를 등록하십시오.
 성공하면 사용자가 등록되었다는 알림이 표시됩니다.
 

사용자가 애플리케이션에 계정을 등록하면 로그인 할 수있는 페이지가 필요합니다.`views` 폴더에`Login.vue`라는 새 파일을 만듭니다.
 

이 새 페이지를 경로에 추가 한 다음 내비게이션에 표시해야합니다.
 `router` 폴더에서`index.js` 파일을 엽니 다.
 이것을 경로 배열에 추가하십시오.
 

```undefined
{
    path: '/login',
    name: 'Login',
    component: () =>
        import(/* webpackChunkName: "login" */ '../views/Login.vue'),
},
```

이제 이것을 탐색에 추가하십시오.
 `App.vue` 파일을 열고 탐색에`Register` 항목을 추가합니다.
 탐색은 다음과 같아야합니다.
 

```undefined
<div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> |
    <router-link to="/register">Register</router-link> |
    <router-link to="/login">Login</router-link> 
</div>
```

`Login.vue` 파일로 돌아갑니다.
 `Register.vue` 파일의 템플릿 섹션에있는 HTML 코드를 복사하여이 새 파일에 붙여 넣을 수 있습니다.
 `Register`의 모든 참조를`Login`으로 변경합니다.
 템플릿 섹션은 다음과 같아야합니다.
 

```undefined
<div class="container">
    <form @submit.prevent="login">
        <h2>Login</h2>
        <input type="email" v-model="email" placeholder="Email address..." />
        <input type="password" v-model="password" placeholder="password..." />
        <button>Login</button>
    </form>
</div>
```

스크립트 섹션에서 `Auth`에 대한 가져 오기와 이메일 및 비밀번호에 대한 데이터 개체를 추가합니다.
 스크립트 섹션은 다음과 같아야합니다.
 

```undefined
<script>
import { Auth } from 'aws-amplify';
export default {
  name: 'Login',
  data() {
    return {
      email: '',
      password: ''
    }
  },
}
</script>
```

마지막으로 구현해야 할 것은 로그인 방법입니다.
 코드는 다음과 같습니다.
 

```undefined
async login() {
    try {
        await Auth.signIn(this.email, this.password);
        alert('Successfully logged in');
    } catch (error) {
        alert(error.message);
    }
},
```

이제 애플리케이션을 열면 이전에 등록한 사용자로 로그인 할 수 있습니다.
 

사용자가 애플리케이션에서 로그 아웃 할 수 있도록 버튼을 추가해야합니다.
 `App.vue` 파일을 엽니 다.
 탐색에서 로그 아웃하는 버튼을 추가합니다.
 탐색은 다음과 같아야합니다.
 

```undefined
<div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> |
    <router-link to="/register">Register</router-link> |
    <router-link to="/login">Login</router-link> |
    <button @click="logout">Logout</button>
</div>
```

스크립트 섹션에서`methods` 객체를 추가하고`logout` 메서드를 포함합니다.
 다음과 같이 표시되어야합니다.
 

```undefined
methods: {
    async logout() {
        try {
            await Auth.signOut();
        } catch (error) {
            alert(error.message);
        }
    },
},
```

축하합니다. Vue 애플리케이션에 AWS Amplify 인증을 성공적으로 추가했습니다.
 

여기 내 GitHub 계정에 전체 코드가 있습니다.
 

다른 인증 방법을 사용하여 Vue 애플리케이션에 인증을 추가하는 방법에 대한 몇 가지 후속 기사를 작성했습니다.
 

- 인증에 Firebase 사용
 
- 인증에 Auth0 사용
 

AWS Amplify는 애플리케이션에 인증을 추가 할 수있는 훌륭한 도구입니다.
 

이 기사가 재미 있었기를 바랍니다.
 읽어 주셔서 감사합니다.
 

2020 년 12 월 31 일에 https://www.jenniferbland.com에 처음 게시되었습니다.
 