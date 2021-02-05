---
layout: post
title: "오픈 소스 TypeScript Repo 인 DefinitelyTyped에 처음으로 기여한 방법
 "
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/02/definitelytyped.png
tags: undefined
---


TypeScript는 굉장합니다.
 즉시 코드를 더 안전하고 디버깅하기 쉬우 며 더 잘 문서화 할 수 있습니다.
 

얼마 동안 저는 모든 프로젝트에서 TypeScript를 독점적으로 사용하고 있습니다.
 그리고 여기에 문제가 있습니다. 유형 정의가 누락 된 패키지를 본 적이 없습니다.
 지금까지...
 

나는이 점에서 약간 버릇이 없다는 것을 인정합니다.
 하지만 우리가 사용하던 작지만 유용한 Gatsby 플러그인 인 gatsby-plugin-breakpoints가 아직 유형 정의를 갖고 있지 않다는 사실에 놀랐습니다.
 생각하게 했어요.
 

나의 초기 반응은 프로젝트에서 플러그인을 완전히 제거하는 것이 었습니다.
 쉽게 복제 할 수있는 간단한 기능을 제공했습니다.
 그리고 일반적으로 외부 의존성이 적을수록 좋습니다.
 

그러나 플러그인은 이미 프로젝트 전체에서 꽤 광범위하게 사용되었습니다.
 따라서 리팩토링을 피하려면 API를 정확히 복제해야했습니다.
 이것은 종속성을 제거하기 위해 이미 존재하는 (그리고 작동하는) 코드를 다시 작성해야 함을 의미합니다.
 이것은 좋은 접근 방식이 아닌 것 같습니다.
 

대신 프로젝트에 필요한 유형 만 추가하기로 결정했습니다.
 이것은 충분히 간단했습니다.
 내가 그것을 알기도 전에 모든 것이 끝났고 잘되었습니다.
 

그러나 나는 무언가를 깨달았다.
 React 프로젝트에서 매일 사용하는 수십 개의 라이브러리 및 플러그인에 대해이 작업을 수행 한 것은 이번이 처음이었습니다.
 그것은 처음에 저를 너무 많이 망친 커뮤니티에 뛰어 들고 작은 공헌을 할 수있는 독특한 기회를 제공했습니다.
 

그래서 했어요.
 

DefinitelyTyped는 TypeScript 유형 정의를위한 커뮤니티 주도 오픈 소스 저장소입니다.
 제가하고자했던 종류의 공헌을위한 장소입니다.
 

아래에서 설명하는 내용은 React 중심이지만 더 일반적인 가이드 역할을 할 수 있기를 바랍니다.
 

## Contribute 설정하기
 

시작은 간단합니다.
 첫 번째 단계는 DefinitelyTyped 저장소를 포크하고 다음을 사용하여 스캐 폴딩을 생성하는 것입니다.
 

```undefined
npx dts-gen --dt --name gatsby-plugin-breakpoints --template module

```

이렇게하면 DefinitelyTyped 프로젝트에 4 개의 파일이있는 폴더가 생성됩니다.
 

```undefined
gatsby-plugin-breakpoints-test.ts
index.d.ts
tsconfig.json
tslint.json
```

모든 타입 정의는`index.d.ts`에 있으며`gatsby-plugin-breakpoints-test.ts`는 모든 것이 예상대로 작동하는지 확인하는 데 도움이됩니다.
 

시작하기 전에 React로 작업하고 있으므로`tsconfig.json`에서 약간의 조정이 필요합니다.
 compilerOptions에` "jsx": "react"`를 추가하고 테스트 파일 이름을`gatsby-plugin-breakpoints-tests.tsx`로 변경해야합니다.
 또한 실제 테스트 파일의 이름을 바꾸는 것을 잊지 마십시오.
 

최종`tsconfig.json`은 다음과 같아야합니다.
 

```undefined
{
    "compilerOptions": {
        "module": "commonjs",
        "lib": [
            "es6",
            "DOM"
        ],
        "noImplicitAny": true,
        "noImplicitThis": true,
        "strictFunctionTypes": true,
        "strictNullChecks": true,
        "baseUrl": "../",
        "typeRoots": [
            "../"
        ],
        "types": [],
        "noEmit": true,
        "forceConsistentCasingInFileNames": true,
        "jsx": "react",
        "esModuleInterop": true
    },
    "files": [
        "index.d.ts",
        "gatsby-plugin-breakpoints-tests.tsx"
    ]
}

```

여태까지는 그런대로 잘됐다!
 verified_user

## 유형을 만들고 테스트하는 방법
 

`gatsby-plugin-breakpoints` 문서와 소스 코드를 살펴보면 생성해야하는 유형을 식별 할 수 있습니다.
 빠른 목록을 만들어 보겠습니다.
 

- 플러그인 구성
 
- useBreakpoint React 후크
 
- withBreakpoints React HOC (상위 구성 요소)
 
- BreakpointProvider
 
- BreakpointContext
 

### 플러그인 구성
 

먼저 구성을 다루겠습니다.
 

```undefined
// index.d.ts

// Type definitions for gatsby-plugin-breakpoints 1.3
// Project: https://github.com/JimmyBeldone/gatsby-plugin-breakpoints
// Definitions by: Iva Kop <https://github.com/IvaKop>
// Definitions: https://github.com/DefinitelyTyped/DefinitelyTyped

/**
 * @see https://www.gatsbyjs.com/plugins/gatsby-plugin-breakpoints/
 */


export type QueriesObject = Record<string, string>;

export interface BreakpointOptions {
    queries?: QueriesObject;
}

export interface BreakpointConfig {
    resolve: 'gatsby-plugin-breakpoints';
    options?: BreakpointOptions;
}
```

멋있는!
 이제 테스트 파일로 이동하여 모든 작업을 올바르게 수행했는지 확인합니다.
 

```undefined
// gatsby-plugin-breakpoints-tests.tsx

import React from 'react';
import {
    BreakpointConfig,
} from 'gatsby-plugin-breakpoints';

const defaultQueries = {
    xs: '(max-width: 320px)',
    sm: '(max-width: 720px)',
    md: '(max-width: 1024px)',
    l: '(max-width: 1536px)',
};

const plugins: BreakpointConfig = {
    resolve: `gatsby-plugin-breakpoints`,
    options: {
        queries: defaultQueries,
    },
};

```

### useBreakpoints
 

다음으로 useBreakpoints 후크를 입력 해 보겠습니다.
 

```undefined
// index.d.ts
// ...

export type BreakpointsObject = Record<string, boolean>;

export function useBreakpoint(): BreakpointsObject;
```

그리고 그것을 테스트하십시오.
 

```undefined
// gatsby-plugin-breakpoints-tests.tsx

import React from 'react';
import {
    // ...
    useBreakpoint
} from 'gatsby-plugin-breakpoints';

function HookComponent() {
    const breakpoints = useBreakpoint();
    return <div>{breakpoints.xs ? <div /> : null}</div>;
}



```

### withBreakpoints
 

플러그인은 우리가 사용할 수있는 HOC (고차 구성 요소)도 제공합니다.
 입력 해 보겠습니다.
 

```undefined
// index.d.ts
// ...

export interface BreakpointProps {
    breakpoints: BreakpointsObject;
}

export function withBreakpoints<P extends BreakpointProps>(Component: React.ComponentType<P>): React.ComponentType<P>;

```

... 그리고 그것을 테스트하십시오.
 

```undefined
// gatsby-plugin-breakpoints-tests.tsx

import React from 'react';
import {
    // ...
    withBreakpoints,
    BreakpointProps,
} from 'gatsby-plugin-breakpoints';

const EnhancedFunctionalComponent = withBreakpoints(function Component({ breakpoints }) {
    return breakpoints.xs ? <div /> : <div>Content hidden only on mobile</div>;
});

class Component extends React.Component<BreakpointProps> {
    render() {
        const { breakpoints } = this.props;
        return breakpoints.xs ? <div /> : <div>Content hidden only on mobile</div>;
    }
}

const EnhancedClassComponent = withBreakpoints(Component);

```

### BreakpointContext 및 BreakpointProvider
 

마지막으로 `BreakpointContext`와 `BreakpointProvider`라는 두 가지 더 처리해야 할 사항이 있습니다.
 

```undefined
// index.d.ts
// ...

export type QueriesObject = Record<string, string>;

export const BreakpointContext: React.Context<QueriesObject>;

export const BreakpointProvider: React.Provider<QueriesObject>;
```

마지막 테스트 :
 

```undefined
// gatsby-plugin-breakpoints-tests.tsx

import React from 'react';
import {
    // ...
    BreakpointProvider,
    BreakpointContext,
} from 'gatsby-plugin-breakpoints';

// BreakpointContext
function useContext() {
    const context = React.useContext(BreakpointContext);
    return context;
}

// BreakpointProvider
const ProviderComponent: React.FC = ({ children }) => {
    return <BreakpointProvider value={defaultQueries}>{children}</BreakpointProvider>;
};

```

## 마지막 단계
 

어려운 부분은 이제 끝났습니다.
 남은 것은 풀 요청을 만들기 전에 DefinitelyTyped lint 및 테스트 스크립트를 실행하는 것입니다.
 

```undefined
npm run lint gatsby-plugin-breakpoints
```

모두 좋아 보인다!
 

```undefined
npm run test gatsby-plugin-breakpoints
```

오, 안돼!
 오류가있는 것 같습니다.
 

```undefined
Cannot find module 'csstype' or its corresponding type declarations.
```

고맙게도 우리는 처음으로 그것을 접한 사람이 아닙니다.
 DefinitelyTyped 저장소에 이미 공개 된 문제가 있으며 수정은 상당히 간단 해 보입니다.`types / react`에 노드 모듈을 설치해야합니다.
 그것을 위해 가자!
 

```undefined
cd types/react && npm install && cd ../../ && npm run test gatsby-plugin-breakpoints
```

휴, 작동했습니다!
 

이 단계에서 PR을 열고 모든 CI 검사가 통과되었는지 확인하고 승인을 기다릴 준비가되었습니다.
 내 제한된 경험으로 볼 때 프로세스는 상당히 빠른 것 같습니다.
 이 특정 PR은 하루 조금 넘게 승인, 합병 및 게시되었습니다.
 

확인하려면 여기에 링크가 있습니다.
 

제가 여기서 설명한 것은 작은 기여입니다.
 (우리가 작성하는 모든 코드의 경우처럼) 개선 될 수 있습니다.
 그러나 커뮤니티와 공유하면 작은 기여가 쌓입니다.
 

제가 TypeScript를 1 년 넘게 독점적으로 사용했고 제가 직접 타이핑 할 수있는 프로젝트를 처음 접했다는 사실은 오픈 소스의 굉장함을 증명합니다.
 다음 사람이 프로젝트에서 TypeScript를 사용하는 것을 조금 더 쉽게 만들 수있게되어 기쁩니다.
 

따라서 다음에 해당 유형 (또는 다른 모든 것)을 찾고있는 프로젝트를 찾을 때 가능하면 참여하여 기여하십시오.
 그것은 모든 차이를 만듭니다!
 

이것이 유용하다고 생각되면 연결합시다.
 더 자세한 React 관련 기사는 내 블로그를 확인하세요.
 