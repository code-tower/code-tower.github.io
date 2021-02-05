---
layout: post
title: "TypeScript를 사용하여 RocketChatBot을 구축하는 방법"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1495055154266-57bbdeada43e?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDE4fHxib3R8ZW58MHx8fA&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


오늘 저는 여러분만의 로켓을 만드는 방법을 보여드리겠습니다.봇을 채팅하고 로컬로 테스트합니다.

이것은 커뮤니티에서 자체 호스팅하는 채팅 서버를 위해 무료 CodeCamp의 중재 채팅 봇을 구축하는 데 사용한 것과 동일한 프로세스입니다. 이 코드는 현재 운영 중이며 많은 사람들이 사용하고 있습니다.

## 로켓을 설치하는 방법채팅 서버

당신의 첫 번째 단계는 로켓의 예를 얻는 것입니다.로컬에서 채팅 실행 – 봇의 기능을 테스트하려면 채팅이 필요합니다.

당신은 무료 CodeCamp의 도커 파일을 사용할 수 있으며, 이것은 두 로켓을 회전시킬 것이다.개발 환경을 위해 자동으로 채팅 및 MongoDB를 수행합니다. 이렇게 하면 많은 시간을 절약할 수 있습니다.

이 리포지토리를 복제하거나 구성에 따라 직접 도커 파일을 만들 수 있습니다. 이 튜토리얼에서는 기존 도커 파일을 사용하고 있다고 가정합니다.

> 참고: 도커가 설치되어 있지 않으면 도커를 설치해야 합니다. 설치 프로세스는 운영 체제마다 다릅니다. 개인적으로 Windows 10을 사용하기 때문에 Docker 데스크톱 클라이언트를 설치하고 BIOS에서 '하드웨어 가상화'를 사용하도록 설정해야 했습니다.

로켓 안에서요채팅 디렉토리에서 `.env` 파일을 작성한 후 다음 내용을 삽입합니다.

그런 다음 동일한 디렉토리를 가리키는 터미널을 열고 다음을 실행합니다.

터미널에 다음과 같은 세 가지 성공 메시지가 표시됩니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-180.png)

이제 브라우저를 열고 localhost:3000으로 이동하면 로컬 로켓을 볼 수 있습니다.채팅 인스턴스. 표시되는 첫 번째 화면은 설치 마법사가 되어 관리자 계정을 만드는 과정을 안내합니다.

대부분의 개발자는 대화를 구성하기 위해 루트 수준 액세스에 관리자 계정을 사용합니다. 이것은 로컬 인스턴스이기 때문에 인증서의 보안은 라이브 인스턴스보다 덜 중요합니다.

정보를 입력하여 관리자 계정을 만듭니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-181.png)

다음 화면은 조직 정보 화면입니다. 이 정보는 선택 사항입니다. 이 튜토리얼의 경우 이 정보는 공백으로 둡니다.

계속을 클릭하면 서버 정보 페이지가 나타납니다. 여기서는 채팅 서버 이름(`제목` 메타데이터에 표시됨), 기본 언어, 서버 유형 및 2FA 설정을 설정합니다.

로컬 인스턴스에 대한 자동 2FA 설정을 해제해야 합니다. 그렇지 않으면 자체 서버에서 잠길 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-182.png)

마지막 단계는 선택적으로 서버를 등록하고 로켓에 액세스하는 것입니다.푸시 알림과 같은 채팅의 서비스입니다. 이러한 서비스는 유료 서비스입니다.

이 튜토리얼을 위해 `독립 실행형 유지` 옵션을 선택할 수 있습니다. 그런 다음 나중에 유료 서비스를 원하는지 여부를 결정할 수 있습니다.

계속을 클릭하면 작업영역을 사용할 준비가 되었음을 나타내는 모달이 표시됩니다. 그럼 새로운 채팅방을 봐야겠네요. 설치 마법사가 생성한 기본 채널은 `일반`입니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-183.png)

이거 보시면 축하드려요. 반쯤 가서 이제 기능 채팅 서버를 사용할 수다를 떨 수 있습니다.

## 로켓에서 봇 계정을 설정하는 방법채팅

이제 코드를 연결할 로컬 채팅 서버에 봇 사용자를 만들어야 합니다.

사이드바 상단에 있는 점 세 개를 선택하고 `관리`를 선택합니다. 그런 다음 나타나는 새 사이드바에서 `사용자`를 선택하고 오른쪽 상단에 있는 `+새로 만들기` 버튼을 클릭합니다. 새 사용자 계정을 만들 수 있는 창이 열립니다.

봇 계정의 정보 및 자격 증명을 입력합니다.

몇 가지 중요한 사항:

- 비밀번호 변경 필요 및 임의 비밀번호 설정 및 이메일로 보내기 설정을 해제로 유지합니다.
- 환영 전자 메일 보내기 설정을 해제로 둡니다.
- `역할` 드롭다운 메뉴에서 `봇`을 선택합니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/image-185.png)

> Rocket.cat은 시스템 알림에 사용되는 기본 제공 계정입니다.채팅 업데이트).

변경 내용을 저장하면 이제 봇 계정이 생성됩니다! 사용자 이름과 암호를 기록해 두십시오. 코드에는 이러한 정보가 필요합니다.

## 로켓 코드 만드는 법채팅 챗봇

이제 코드를 만들 시간입니다. 프로젝트의 비어 있는 새 폴더로 시작하십시오.

### 이니셜 로켓.채팅 챗봇 프로젝트 설정

먼저 node.js 프로젝트를 초기화하겠습니다. `npm init`을 사용하여 `package`를 생성해도 좋습니다.json을 선택하거나 수동으로 생성할 수 있습니다.

어느 쪽이든 `scripts` 섹션에 특정 값을 추가해야 합니다.

다음으로 필요한 종속성을 설치합니다. 먼저 개발 종속성을 설치합니다.

그런 다음 기본 종속성을 설치합니다.

다음 단계는 TypeScript 구성을 설정하는 것입니다.

TypeScript를 전체적으로 설치한 경우 `tsc --init`를 호출하여 구성 파일을 자동으로 생성할 수 있습니다. 그렇지 않으면 프로젝트의 루트 디렉터리에 `tsconfig.json` 파일을 수동으로 생성해야 합니다.

어느 쪽이든 이 프로젝트에 필요한 설정은 다음과 같습니다.

```undefined
{
  "compilerOptions": {
    "target": "ES5",
    "module": "CommonJS",
    "rootDir": "./src",
    "outDir": "./prod",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "noImplicitAny": false,
  }
}
```

버전 제어에 `git`를 사용하는 경우 `.gitignore` 파일을 작성해야 합니다. 이 파일은 무시할 파일/폴더를 `git`에 알려줍니다. 이 경우 다음을 무시합니다.

- `prod`로 편집된 자바스크립트
- 노드 모듈
- 당신의 .env 비밀

`.gitignore`에 추가:

```undefined
/node_modules/
/prod/
.env
```

비밀 얘기가 나와서 말인데, 지금 당장 그걸 세워야 해. .env 파일을 생성하고 다음 값을 추가하십시오.

이 시점에서 코드를 봅니다.

### 1차 로켓 작성 방법채팅 챗봇 코드

이제 초기 봇 코드를 작성할 시간입니다. 프로젝트 디렉터리 내에 `src` 폴더를 생성하고, 해당 `src` 폴더 내에 `bot.ts` 파일을 생성합니다. 이제 파일 구조는 다음과 같습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-9.png)

> package-lock.json 파일은 install을 실행할 때마다 npm에 의해 생성/업데이트됩니다. 이 작업은 npmci 명령에도 필요하므로 리포지토리에도 커밋해야 합니다.

bot.ts 파일 내에 bot를 구동하는 기본 코드를 작성합니다. 필요한 가져오기 작업부터 시작합니다.

`노드`는 환경 변수를 자동으로 로드하지 않으므로 `.env` 값을 노드 프로세스로 가져오려면 `dotenv`의 `config()` 메서드를 호출해야 합니다.

이제 노드 환경에서 이러한 변수를 추출할 수 있습니다. 소멸을 사용하여 다음 값을 가져옵니다.

```undefined
const {
  ROCKETCHAT_URL,
  ROCKETCHAT_USER,
  ROCKETCHAT_PASSWORD,
  ROCKETCHAT_USE_SSL,
} = process.env;
```

ROCKETCT_USE_SSH 외에 이러한 환경 값이 필요합니다. 하나를 생략하면 쓰는 코드가 오류 발생하므로 이러한 값이 모두 존재하는지 확인하는 단계를 추가해야 합니다.

이제 로켓을 사용할 수 있습니다.SDK를 채팅하여 만든 계정에 봇을 연결합니다.

SDK의 메소드는 비동기적이므로 즉시 호출되는 익명 함수 표현식(IIFE)을 사용하여 `sync/wait` 기능을 사용하도록 설정합니다.

```undefined
(async () => {
  // Nothing here yet
})();
```

> 다음 단계는 이 기능 내부에 기록됩니다.

먼저 봇이 SSL을 사용하여 대화 서버에 연결할지 여부를 결정합니다. 채팅 서버가 `HTTPS://pit`를 사용하는 경우 이 설정을 `true`로 설정해야 합니다. 로컬에서 개발 중이기 때문에 localhost에는 HTTPS 프로토콜이 없으므로 false로 설정됩니다.

운영 환경에서도 코드가 작동하도록 하려면 환경 변수를 기준으로 이 값을 동적으로 설정할 수 있습니다.

다음으로 SDK `driver`를 사용하여 채팅 서버와 인터페이스합니다. `드라이버`를 서버에 연결합니다.

```undefined
await driver.connect({ host: ROCKETCHAT_URL, useSsl: ssl });
```

봇 계정으로 로그인:

봇이 아직 룸에 있지 않은 인스턴스를 처리하기 위해 봇을 `일반` 룸에 참여시킵니다. 또한 `subscribeToMessages()` 방법으로 메시지를 들으라고 봇에 지시합니다.

```undefined
  await driver.joinRooms(["general"]);
  await driver.subscribeToMessages();
```

마지막으로 온라인 상태가 되면 봇이 메시지를 보내도록 합니다(연결 상태를 확인할 수 있습니다.

```undefined
  await driver.sendToRoom("I am alive!", "general");
```

이제 코드를 작성하고 실행합니다. 터미널에서 필요한 스크립트를 호출합니다.

```undefined
npm run build
npm run start
```

SDK에서 일부 기본 제공 로깅 후 채팅 서버에서 봇이 온라인 메시지를 보내는 것을 볼 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-10.png)

이 시점에서 코드를 봅니다.

### 명령 처리기 쓰기 방법

이제 봇이 채팅 서버에 연결하여 메시지를 수신하지만 기능이 없습니다.

명령을 추가하려면 먼저 해당 명령을 처리할 인프라를 구축해야 합니다.

먼저, 그 봇에게 메시지를 처리하라고 말해라. `subscribeToMessages()` 호출 직후 메시지에 응답할 줄을 추가합니다.

```undefined
driver.reactToMessages();
```

`reactToMessages()` 메서드에서 콜백 기능이 필요하므로 Intellisense에 오류가 표시됩니다.

이 메서드에 직접 콜백 함수를 쓸 수 있지만 대신 코드를 모듈화하고 내보낸 처리기를 만듭니다. 이렇게 하면 코드가 더 깨끗하고 유지 관리 용이해집니다.

`src` 폴더에 `commands`라는 폴더를 만들고 `commandhandler.ts`와 `commandList.ts`의 두 파일을 추가합니다. CommandList.ts 파일 내에 한 줄을 추가할 예정입니다.

```undefined
export const CommandList = [];
```

명령을 작성할 때 이 배열에 명령을 추가하여 처리기에서 명령을 반복할 수 있습니다.

이제 `CommandHandler.ts` 파일에 처리기의 논리를 작성해야 합니다.

필요한 가져오기 작업부터 시작합니다.

명령 처리기 기능을 정의합니다.

오류 처리를 추가합니다.

```undefined
  if (err) {
    console.error(err);
    return;
  }
  const message = messages[0];
  if (!message.msg || !message.rid) {
    return;
  }
```

`err` 매개변수에 오류가 나타나면 `return`을 조기에 수행해야 합니다.

`messages` 매개 변수는 메시지 배열을 사용하지만 첫 번째 메시지에 응답하고자 하므로 해당 배열에서 `message`로 추출합니다.

그런 다음 TypeScript의 어설션 처리를 위해 특정 속성이 없거나 정의되지 않은 경우 일찍 종료해야 합니다. 이 경우 메시지.msg는 메시지의 텍스트 내용이고, message.rid는 메시지를 받은 룸의 ID입니다.

클리너/더 읽기 쉬운 코드의 경우 메시지 개체에서 일부 값을 분석할 수 있습니다. rid 값에서 룸 이름을 가져옵니다. SDK에는 이 방법을 사용하는 방법이 포함되어 있습니다. 접두사 및 호출되는 명령도 가져옵니다.

```undefined
  const roomName = await driver.getRoomName(message.rid);
  const [prefix, commandName] = message.msg.split(" ");
```

명령 배열을 통해 반복할 논리를 추가합니다. TypeScript는 구조 누락으로 인한 일부 오류를 식별하지만, 아직 명령을 작성하지 않았으므로 이러한 오류를 무시할 수 있습니다.

이 코드 블록은 명령이 작동하는 방식을 아직 설정하지 않았기 때문에 약간 혼란스러울 수 있습니다.

먼저, 봇은 메시지가 올바른 접두사로 시작되는지 여부를 결정합니다. 그렇지 않으면 봇이 메시지를 무시합니다.

그런 다음 보터는 명령 목록을 반복하여 `name` 값이 메시지에서 보낸 명령 이름과 일치하는 명령을 찾으면 해당 명령을 실행합니다.

일치하는 명령을 찾을 수 없는 경우 룸에서 명령이 유효하지 않다는 응답을 보냅니다.

명령으로 이동하기 전에 `bot.ts` 파일의 `reactToMessages()` 호출로 돌아가 콜백으로 새 처리기를 전달합니다.

```undefined
  driver.reactToMessages(CommandHandler);
```

수동으로 가져와야 할 수도 있습니다.

```undefined
import { CommandHandler } from "./commands/CommandHandler";
```

이 시점에서 코드를 봅니다.

### 명령 작성 방법

TypeScript는 객체 구조를 정의하는 데 사용할 수 있는 `인터페이스` 기능을 제공합니다.

`src` 폴더에서 `인터페이스` 폴더를 만들고 `CommandInt.ts` 파일을 만듭니다.

파일 내에서 명령 유형을 정의합니다. 먼저 메시지 유형을 다시 가져옵니다.

```undefined
import { IMessage } from "@rocket.chat/sdk/dist/config/messageInterfaces";
```

이제 명령 정의를 위해 내보낸 인터페이스를 빌드합니다.

축하합니다! 이제 ping 명령을 만들 준비가 되었습니다.

`src/commands` 폴더에 `ping.ts` 파일을 생성합니다. 필요한 수입품부터 시작하세요: 로켓.채팅 드라이버 및 새 명령 인터페이스.

```undefined
import { driver } from "@rocket.chat/sdk";
import { CommandInt } from "../interfaces/CommandInt";
```

명령 정의 및 내보내기:

이 명령이 호출되면 bot가 "퐁!"으로 응답하도록 하자. 기능 내에서 설명을 다음으로 교체합니다.

```undefined
await driver.sendToRoom("Pong!", room);
```

이제 이 명령을 명령 목록에 로드합니다. 새 명령을 가져와 어레이에 포함할 `CommandList.ts` 파일을 엽니다.

```undefined
import { ping } from "./ping";

export const CommandList = [ping];

```

TypeScript에서 `CommandList` 배열에 `CommandList`가 포함되어 있다고 추론하고 있으므로 `CommandHandler.ts` 파일의 오류도 사라집니다.Int `type`입니다.

추가 유형 안전을 위해 `명령 목록`에 적절한 `명령`이 아닌 값을 실수로 추가하지 않도록 하기 위해객체에 이 변수를 명시적으로 입력합니다.

빌드 및 시작 스크립트를 다시 실행하여 이 새 기능을 테스트합니다.

대화방에서 ping 명령을 호출합니다. 다음과 같은 응답을 볼 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-11.png)

pong 명령을 호출합니다. 봇이 유효한 명령이 아님을 식별하는지 확인해야 합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-12.png)

최종 코드를 봅니다.

## 추가 탐색

축하합니다! 이제 기본 로켓을 성공적으로 제작했습니다.채팅 챗봇.

추가 기능 및 명령 구현에 대해 알아보려면 언제든지 라이브 봇의 코드베이스를 탐색하십시오.