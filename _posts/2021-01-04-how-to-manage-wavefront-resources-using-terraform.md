---
layout: post
title: "Terraform을 사용하여 Wavefront 리소스를 관리하는 방법"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/wavefront-terraform.png
tags: undefined
---


이전 기사에서는 메트릭과 메트릭스가 하드웨어 및 소프트웨어 시스템의 운영 상태를 파악하는 데 어떤 도움이 되는지에 대해 썼습니다.

Wavefront는 3D 관찰성(측정지표, 히스토그램, 추적/스팬)을 지원하는 고성능 스트리밍 분석 플랫폼입니다.

매우 높은 데이터 수집 속도와 쿼리 부하로 확장할 수 있습니다. 전체 애플리케이션 스택에서 여러 서비스 및 소스에서 데이터를 수집할 수 있으며, Wavefront에서 수집된 이전 데이터에 대한 세부 정보를 확인할 수 있습니다.

테라폼(Terraform)은 HashiCorp에서 개발한 오픈 소스 "Infrastructure as Code" 툴이다.

선언적 코딩 도구이며 개발자가 HCL(HashiCorp Configuration Language)이라는 고급 구성 언어를 사용하여 인프라에 대해 원하는 "종료 상태"를 설명할 수 있도록 한다.

이 인프라는 클라우드 또는 사내에 있을 수 있습니다. 그런 다음 해당 최종 상태에 도달하기 위한 계획을 생성하고 인프라 생성 계획을 실행합니다.

이 기사에서는 Terraform을 사용하여 Wavefront에서 대시보드와 경보를 자동으로 작성하는 코드를 작성하는 방법에 대해 알아보겠습니다. 이는 모든 모니터링 인프라가 코드로 유지되고 GitHub와 같은 버전 제어 시스템에 체크인되는 DevOps 문화 유지에 매우 유용합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/image-21.png)

## 테라폼 설치 방법

OS에 따라 Terraform의 설치 지침은 달라집니다. 이 자료에서는 macOS에 설치하는 방법에 대해 설명합니다.

MacOS에 설치할 때 권장되는 방법은 홈브루 패키지 관리자를 사용하는 것입니다.

### 테라폼 설치

다음과 같이 홈브루가 설치되어 있는지 확인합니다.

```undefined
$ brew --version

Homebrew/homebrew-core (git revision fe68a; last commit 2020-10-15)
Homebrew/homebrew-cask (git revision 4a2c25; last commit 2020-10-15)
```

그렇지 않은 경우 다음 명령을 사용하여 홈브루를 설치할 수 있습니다.

```undefined
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

그런 다음 다음 명령을 사용하여 Terraform을 설치합니다.

```undefined
$ brew tap hashicorp/tap
$ brew install hashicorp/tap/terraform
```

### Terraform 설치 확인

Terraform이 제대로 설치되었는지 확인하려면 다른 터미널 세션을 열고 Terraform 명령을 사용해 보십시오.

```undefined
$ terraform --help

Usage: terraform [global options] <subcommand> [args]

The available commands for execution are listed below.The primary workflow commands are given first, followed byless common or more advanced commands.
```

## API 토큰을 가져오는 방법

Terraform이 Wavefront 설치에 액세스할 수 있도록 하려면 액세스 토큰을 제공해야 합니다. 이 토큰은 계정의 API 토큰 섹션에서 찾을 수 있습니다.

기어 아이콘 > 계정 이름 > API 액세스로 이동

![image](https://www.freecodecamp.org/news/content/images/2020/12/Screenshot-2020-12-26-at-12.49.23-PM.png)

## Terraform 프로젝트 설정 방법

먼저 Terraform 프로젝트의 새 폴더를 생성합니다.

```undefined
$ mkdir wavefront-terraform
```

일반적인 Terraform 프로젝트에는 세 가지 주요 파일이 포함되어 있습니다.

- versions.tf — 사용할 플러그인 버전을 지정하는 Terraform 제공자 선언을 포함합니다.
- 변수tf — 기본 Terraform 코드에서 참조할 수 있는 변수를 포함합니다.
- main.tf — 이름에서 알 수 있듯이 여기에는 리소스를 구축하는 데 필요한 실제 코드가 포함됩니다.

프로젝트 폴더에 versions.tf 파일을 생성하고 다음 코드를 추가합니다.

다음으로, `terraform init` 명령을 실행하여 Wavefront 제공자를 초기화합니다.

```undefined
$ terraform init
```

그러면 terraform-wavefront-provider-<version> 파일이 다운로드되어 현재 프로젝트 폴더의 a.terraform 폴더에 저장됩니다.

그런 다음 프로젝트 폴더에 main.tf 파일을 생성하고 다음 코드를 추가합니다.

설치가 완료되었으므로 이제 몇 가지 대시보드와 경고를 만들 준비가 되었습니다.

## Wavefront 대시보드 작성 방법

대시보드를 만들기 전에 먼저 Wavefront 대시보드의 구조를 이해하겠습니다.

![image](https://www.freecodecamp.org/news/content/images/2020/12/Wavefront_Dashboard.png)

Wavefront의 대시보드는 5가지 엔티티로 구성됩니다.

- 대시보드 — 기본 대시보드이며 다른 모든 엔티티가 포함되어 있습니다.
- 섹션 — 대시보드에 하나 이상의 섹션이 포함될 수 있습니다. 섹션은 차트의 논리적 그룹입니다. 예를 들어 하드웨어 사용률과 관련된 차트를 표시하는 섹션과 API 호출과 관련된 차트를 표시하는 섹션이 각각 하나씩 있을 수 있습니다.
- 행 - 행은 차트의 집합입니다. 행에 표시할 차트 수를 정의할 수 있습니다. 제가 개인적으로 추천하는 것은 3개의 차트를 연속해서 만드는 것입니다. 그 이상이면 대시보드가 복잡해집니다.
- 차트 — 이 차트는 대시보드에 메트릭을 표시하는 최종 차트입니다. 차트 작성에는 선 차트, 막대 차트, 원형 차트 등과 같은 다양한 옵션이 있습니다.
- 원본 - 관리도에 하나 이상의 원본을 포함할 수 있습니다. 각 소스에는 기본 메트릭에서 작동하여 차트에 시각적 표현을 만드는 쿼리가 있습니다.

이제 대시보드를 만들기 위한 몇 가지 코드를 작성할 준비가 되었습니다. 다음 코드를 main.tf 파일에 추가합니다.

이렇게 하면 EC2 메트릭에 대한 섹션 하나가 포함된 대시보드가 생성됩니다. 이 절에는 두 개의 차트가 있는 행이 하나 있습니다. 한 차트는 CPU Utilization을 표시하고 다른 차트는 메모리 Utilization을 표시합니다. 둘 다 선 차트이며 사용률을 나타냅니다.

## 알림 생성 방법

우리가 만든 대시보드는 EC2 인스턴스의 CPU 및 메모리 활용도를 살펴보기 매우 좋습니다. 그러나 CPU 또는 메모리 사용량이 특정 임계값을 초과할 때 알림을 받으려면 몇 가지 알림을 설정해야 합니다.

CPU Utilization에 대한 경고를 생성하려면 다음 코드를 main.tf 파일에 추가하십시오.

이렇게 하면 두 가지 리소스가 생성됩니다.

- 알림을 열거나 확인할 때마다 지정된 주소로 이메일을 보내는 알림 대상입니다.
- CPU 사용률이 지정된 임계값을 초과할 때 발생하는 CPU 사용률 경고(60%를 초과할 경우 경고, 80%를 초과할 경우 심각 경고)

Wavefront는 CPU 사용률을 지속적으로 모니터링하여 임계값 위반 시 이메일 주소로 알림을 보냅니다. 마찬가지로, 사용률이 정상으로 되면 상황이 복구되었음을 나타내는 다른 알림을 보냅니다.

## Wavefront에서 리소스를 생성하는 방법

리소스 생성 코드가 준비되었습니다. 이제 이를 적용하여 실제 자원이 웨이브프론트에 생성되도록 해야 합니다.

당사의 코드를 통해 Wavefront에 어떤 변경 사항이 적용되는지 보려면 다음 명령을 실행하십시오.

```undefined
$ terraform plan
```

그러면 당사의 코드가 확인되고 Wavefront의 현재 설정과 귀하의 코드로 인해 발생하는 변경 사항 간의 차이가 표시됩니다.

마지막으로 Wavefront에서 리소스를 생성하려면 다음 명령을 실행합니다.

```undefined
$ terraform apply -auto-approve
```

그러면 구성이 Wavefront에 업로드되고 실제 대시보드 및 경고가 생성됩니다. 이제 Wavefront로 이동하여 이러한 리소스를 확인할 수 있습니다.

## 결론

축하합니다! 방금 새로운 Wavefront 대시보드를 만들고 코드를 통해 경고했습니다.

이제 코드를 수정하고 `테라폼 적용 - 자동 승인`을 실행하여 변경 내용을 Wavefront에 적용할 수 있습니다.

Terraform은 버전 제어 시스템에 체크인할 수 있는 코드 형태로 리소스를 유지하는 좋은 방법입니다. 이를 통해 여러 개발자가 리소스 작업을 수행하는 동시에 변경 사항을 추적할 수 있습니다.

이 튜토리얼의 전체 소스 코드는 여기에서 찾을 수 있습니다.

지금까지 나와 함께 있어줘서 고마워. 그 기사가 마음에 들었길 바라. 기술과 생활에 대해 정기적으로 논의하는 LinkedIn에서 저와 연결할 수 있습니다. 제 다른 기사들도 좀 보세요. 즐거운 독서. 🙂