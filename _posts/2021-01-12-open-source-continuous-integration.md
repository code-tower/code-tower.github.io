---
layout: post
title: "코드를 작성하지 않고 주요 오픈 소스 프로젝트에 기여하는 방법"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/Screen-Shot-2021-01-12-at-9.56.22-AM.png
tags: undefined
---


최근에 인기 있는 피닉스 프레임워크에 합병된 풀 요청을 받았는데, 엘릭서 코드를 작성하지 않고 했습니다. 나도 서류를 작성하지 않았어. 제가 한 일은 빌드 프로세스를 개선하는 데 도움이 되었습니다.

이 게시물에서 저는 그들의 빌드 프로세스에 대해 개선한 내용을 공유하고자 합니다. 이러한 개선 사항은 Phoenix Framework에만 국한되지 않으며 지속적인 통합 방식에 변화를 줄 수 있습니다.

하지만 먼저, 배경입니다.

## 피닉스 프레임워크란 무엇인가?

Phoenix는 매우 흥미로운 특성을 가진 웹 프레임워크입니다. Phoenix를 사용하면 클라이언트측 코드를 작성하지 않고도 풍부한 대화형 웹 애플리케이션을 구축할 수 있습니다.

이 작업은 서버에서 실시간 업데이트를 전송하여 클라이언트 브라우저의 HTML을 업데이트하는 LiveView라는 기능을 사용하여 수행할 수 있습니다.

우리는 주제에 대한 최신 트윗을 실시간으로 아주 쉽게 보여주는 페이지를 만들 수 있습니다.

다음은 예입니다.

![image](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FCorecursive%2FDUy3Kzmdsn.png?alt=media&token=edf6aee0-7744-435e-9e3f-0557e000214e)

프레임워크는 프로그래밍 언어 Elixir로 작성되었다.

호세 발림에 의해 만들어졌다. 루비와 많이 닮았지만 의미론도 많이 달라요. Ellixir는 Erlang VM에서 실행되며 Discord와 같은 프로젝트에 전원을 공급하며 Herku와 같은 회사에서 사용됩니다.

## 빌드 재현 방법

Phoenix 프레임워크는 빌드 파이프라인에 GitHub Actions를 사용합니다. 많은 훌륭한 프로젝트와 마찬가지로, 그들은 모든 사용자 기여에 대해 실행해야 하는 일련의 유닛 테스트를 가지고 있습니다.

하지만 그들의 테스트 노력은 여기서 그치지 않는다. 또한 통합 테스트도 실시합니다. Phoenix는 ORM을 사용하여 다양한 데이터베이스와 대화하고 통합 테스트를 통해 지원되는 3개 데이터베이스와의 통합을 중단하는 변경 사항이 없는지 확인합니다.

이것은 일반적인 패턴입니다. 실행하기도 쉽고 속도가 느리지만 좀 더 포괄적인 통합 테스트와 함께 많은 수의 유닛 테스트를 수행하는 것이 프로젝트에 버그가 유입되는 것을 방지하는 좋은 방법입니다.

그러나 Phoenix Framework는 Elixir 언어의 여러 버전과 Open Telecom Platform(OTP)의 몇 가지 버전도 지원해야 하기 때문에 이를 더욱 발전시킨다.

이건 복잡해지기 시작했어 우리는 다음의 모든 조합으로 각 변경 사항을 테스트해야 합니다.

- 데이터베이스(Postgres, MySQL MSSQL)
- Elixir(현재 및 이전 버전)
- OTP(현재 및 이전 버전)

GitHub Actions에서 이 설정을 하는 것은 비교적 쉽습니다. 하지만 이 테스트를 로컬에서 어떻게 실행하시겠습니까?

이러한 모든 것을 설치하는 것은 매우 어려운 일이므로 기여자들은 이러한 조합을 테스트하기 위해 GitHubActions에 의존하는 경향이 있습니다. 하지만, 만약 모든 사람들이 GitHub에 물건들을 밀어넣는 것에 의존해야 한다면, 시험이 통과되는지 보는 것은 개발 속도가 느려진다.

이걸 어떻게 고치죠?

## 테스트 실행을 통합하는 방법

여기가 내가 관여하게 된 곳이야. 나는 오픈소스 개발자 옹호자로서 Earth Technologies에서 일한다. 우리는 꽤 멋진 오픈 소스 빌드 도구를 가지고 있습니다. 제가 가끔 프로젝트에 직접 기여하지만, 제 일은 도구를 사용하는 커뮤니티와 그 도구를 사용하는 팀 간의 접점이 되는 것입니다.

나는 피닉스 팀이 겪고 있는 재현성 문제에 대해 들은 적이 있다. GitHub Actions와 로컬 개발 워크플로우에서 모두 사용할 수 있는 빌드 스크립트를 작성할 수 있다고 생각했습니다. 그래서 저는 홍보에 착수했습니다.

### 로컬에서 테스트 실행

제가 만들어 낸 것은, 약간 단순화된 것입니다:

```undefined
setup:
   ARG ELIXIR=1.10.4
   ARG OTP=23.0.3
   # Pull a Docker Image to Run Build Inside Of
   FROM hexpm/elixir:$ELIXIR-erlang-$OTP-alpine-3.12.0
   ...
 
integration-test:
    FROM +setup
    COPY . .
    # Pull In Dependencies
    RUN mix deps.get 
    # Start Up Service Dependencies
    WITH DOCKER --compose docker-compose.yml 
        # Run Tests
        RUN mix test --include database 
    # Stop Service Dependencies
    END


```

이것은 어스 파일입니다. 그것은 설정, 통합 테스트 등 여러 가지 대상으로 구성되었다. 대상 사이에 종속성이 있을 수 있습니다. 명령줄 도구를 `접지`로 사용하여 모든 대상을 실행할 수 있으며 각 대상은 도커 컨테이너에서 실행됩니다. 컨테이너화를 통해 원하는 곳에서 빌드를 실행할 수 있습니다.

이 예에서는 지정된 버전의 elixir 및 OTP가 설치된 hexpm/elixir 도커 컨테이너 내부에서 `통합 테스트`를 실행합니다.

`mix test --include database`로 테스트를 실행하기 전에 Docker composite를 사용하여 필요한 모든 종속성을 시작합니다.

```undefined
 WITH DOCKER --compose docker-compose.yml
        RUN mix test --include database
 END 

```

도커 작성 파일은 다음과 같습니다.

```yaml
version: '3'
services:
  postgres:
    image: postgres
    ports:
      - "5432:5432"
    environment:
      POSTGRES_PASSWORD: postgres
  mysql:
    image: mysql
    ports:
      - "3306:3306"
    environment:
      MYSQL_ALLOW_EMPTY_PASSWORD: "yes"
  mssql:
    image: mcr.microsoft.com/mssql/server:2019-latest
    environment:
      ACCEPT_EULA: Y
      SA_PASSWORD: some!Password
    ports:
      - "1433:1433" 

```

피닉스를 테스트하는 데 필요한 데이터베이스입니다.

이제 다음과 같이 명령줄에서 통합 테스트를 실행할 수 있습니다.

```undefined
>  earthly -P +integration-test

```

그리고 다른 버전의 Elixir를 테스트하려면 버전을 빌드 인수로 지정할 수 있습니다.

```undefined
 > earthly -P --build-arg ELIXIR=1.11.0 --build-arg OTP=23.1.1 +integration-test

```

이것을 성취하는 다른 방법들이 있다. 메이크 파일과 도커 파일의 조합도 작동했을 것이다. 핵심은 빌드 로직을 GHA의 특정 형식에서 벗어나 어디서나 실행할 수 있는 형식으로 만드는 것입니다.

## GitHub 동작에서 실행하는 방법

GitHub Actions에서 이와 동일한 프로세스를 사용하려면, 우리가 해야 할 일은 GitHub Actions yaml을 빌드 파이프라인에 사용할 수 있도록 조정하기만 하면 됩니다. 그리고 우리는 모두 준비되었습니다.

```js
  integration-test-elixir:
    runs-on: ubuntu-latest
    env:
      FORCE_COLOR: 1
    
    strategy:
      fail-fast: false
      matrix:
        include:
          - elixir: 1.11.1
            otp: 21.3.8.18
          - elixir: 1.11.1
            otp: 23.1.1
    steps:
      - uses: actions/checkout@v2
      - name: Download released earth
        run: "sudo /bin/sh -c 'wget https://github.com/earthly/earthly/releases/download/v0.4.1/earthly-linux-amd64 -O /usr/local/bin/earthly && chmod +x /usr/local/bin/earthly'"
      - name: Execute tests
        run: earthly -P --build-arg ELIXIR=${ matrix.elixir }  --build-arg OTP=${ matrix.otp } +integration-test

```

이제 복잡한 환경 설정 없이 빌드 파이프라인을 로컬로 실행할 수 있습니다. 또한, 우리는 Developer 컴퓨터에서 동일한 빌드 프로세스를 실행할 수 있습니다. 이 프로세스는 Dearte를 제외한 다른 제품은 설치할 필요가 없습니다. 이를 통해 새로운 기여자가 프로젝트에 더 쉽게 접근할 수 있습니다.

## 최종 결과

결국, 피닉스 팀의 도움으로 저는 이 변경을 승인받았고, 피닉스 프로젝트는 이제 그들의 제조 파이프라인에서 테스트하고 반복할 수 있는 쉬운 방법을 갖게 되었습니다. 난 엘릭서 코드도 안 썼어! 자세한 내용은 PR에서 확인할 수 있습니다.

이 기사를 읽어주셔서 감사합니다. 만약 당신이 지구인에 대해 더 알고 싶다면, 당신은 여기서 많은 것을 알 수 있습니다. 그리고 오픈 소스 프로젝트의 빌드에 대한 제 도움이 필요하시면 제게 알려 주십시오.