---
layout: post
title: "Mac에 AWS Elastic Beanstalk CLI를 설치하는 방법"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1523474253046-8cd2748b5fd2?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDF8fGFtYXpvbnxlbnwwfHx8&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


엘라스틱 빈스톡은 AWS 플랫폼의 사용자가 웹 애플리케이션을 쉽게 배포할 수 있는 오케스트레이션 서비스다. 클라우드에서 애플리케이션을 실행하는 데 필요한 모든 설정에 따라 달라집니다.

조정은 단순히 클라우드에서 서비스로서의 리소스를 제공하기 위해 발생하는 워크플로 프로세스를 자동화한다는 의미입니다.

이 튜토리얼에서는 Elastic Bean stalk를 로컬에서 설정하는 간단한 단계를 살펴보겠습니다. 로컬에서 설정하면 터미널에서 AWS와 직접 상호 작용하고 EB에서 제공하는 명령을 통해 배포된 애플리케이션을 클라우드로 푸시할 수 있습니다.

## 탄성콩나무의 장점

Elastic Beanstalk를 사용하면 Elastic Cloud Compute 인스턴스가 종료된 후에도 데이터를 유지할 수 있습니다. 볼륨에 저장된 데이터에 계속 액세스할 수 있습니다.

또한 고가용성 및 내구성을 제공하여 구성요소 장애를 방지할 수 있도록 지원합니다.

## Elastic Beanstalk CLI 설치 방법

Elastic Beanstalk CLI는 사용자가 Elastic Beanstalk에서 프로세스를 생성, 설정 및 관리할 수 있는 명령줄 인터페이스입니다.

우리 지역 환경에 EB를 설치하기 위해서는 오픈 소스 aws-elastic-bean-stalk-cli-setup 프로젝트를 확인해 봐야 합니다. 여기에서 프로세스를 도와주는 설치 안내서를 찾을 수 있습니다.

### 1단계:

리포지토리를 로컬 환경에 복제합니다. Github 계정이 없으시면 여기서 가입하시면 됩니다.

```undefined
git clone https://github.com/aws/aws-elastic-beanstalk-cli-setup.git
```

### 2단계:

이 섹션에서는 zlib를 다운로드하여 구성해야 합니다. Zlib는 압축 및 압축 해제에 사용되는 라이브러리이다. EB는 데이터(스트링, 구조화된 내장 메모리 콘텐츠 또는 파일)를 압축 및 압축 해제해야 할 때 이 기능을 활용합니다.

```undefined
brew install zlib openssl readline
CFLAGS="-I$(brew --prefix openssl)/include -I$(brew --prefix readline)/include -I$(xcrun --show-sdk-path)/usr/include" LDFLAGS="-L$(brew --prefix openssl)/lib -L$(brew --prefix readline)/lib -L$(brew --prefix zlib)/lib"
```

### 3단계:

설치가 완료되면 zlib에 대한 환경 변수의 경로를 내보내고 설정합니다. 명령줄에서 다음을 실행합니다.

```undefined
$ export LDFLAGS=$LDFLAGS:-L/usr/local/opt/zlib/lib
$ export CPPFLAGS=$CPPFLAGS:-I/usr/local/opt/zlib/include
$ export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:~/usr/local/opt/zlib/lib/pkgconfig
```

경로가 올바르게 설정되었는지 보려면 다음 명령을 실행하십시오.

```undefined
$ echo $LDFLAGS $CPPFLAGS $PKG_CONFIG_PATH
```

### 4단계:

저장소를 꺼낸 터미널로 돌아가서 아래 코드와 함께 번들 설치 관리자를 실행해야 합니다.

```undefined
$ ./aws-elastic-beanstalk-cli-setup/scripts/bundled_installer
```

프로세스가 완료되면 다음과 같은 결과를 볼 수 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screenshot-2021-01-09-at-14.33.22.png)

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screenshot-2021-01-09-at-14.33.34.png)

### 5단계:

설치 과정을 마치려면 환경경로에도 eb와 python을 추가해야 한다. 터미널에서 이 코드를 실행하면 다음과 같은 작업을 수행할 수 있습니다.

```undefined
$ echo 'export PATH="/Users/user/.ebcli-virtual-env/executables:$PATH"' >> ~/.bash_profile && source ~/.bash_profile
$ echo 'export PATH=/Users/user/.pyenv/versions/3.7.2/bin:$PATH' >> /Users/user/.bash_profile && source /Users/user/.bash_profile
```

경로 추가를 마치면 Elastic Beanstalk를 초기화하고 선택된 지역 목록이 표시되는지 확인할 수 있습니다. 터미널에서 실행:

```undefined
$ eb init
```

다음 사항을 확인해야 합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screenshot-2021-01-09-at-14.44.03.png)

Voil➡! 선택할 수 있는 지역 목록이 있으며 AWS의 S3 버킷에서 자격 증명을 추가할 수 있습니다. ebcreate, eb deploy 등 다른 eb 명령도 실행할 수 있다.

### 참고문헌

- AWS Elastic Beanstalk 개발자 가이드
- zlib를 사용한 압축