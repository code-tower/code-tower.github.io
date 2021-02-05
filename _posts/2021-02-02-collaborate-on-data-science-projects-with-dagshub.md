---
layout: post
title: "DAGsHub를 사용하여 데이터 과학 프로젝트에서 공동 작업하는 방법
 "
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/02/dagshub-storage.png
tags: undefined
---


소프트웨어 엔지니어링 팀의 경우 Git과 같은 도구와 GitHub, GitLab 및 BitBucket과 같은 원격 Git 클라이언트를 통해 공동 작업이 쉽고 복잡해졌습니다.
 

서로 다른 위치에있는 여러 개발자가 동일한 프로젝트를 원활하게 수행하고 기여할 수 있습니다.
 프로젝트에서 쉽게 협업 할 수있는 이러한 능력은 대규모 오픈 소스 소프트웨어 / 라이브러리 생태계의 개발을 촉진했습니다.
 

안타깝게도 데이터 사이언스 팀도 마찬가지입니다.
 가장 능숙한 데이터 과학 팀조차도 프로젝트를 구성하고 효과적으로 협업하기위한 모범 사례가 부족합니다.
 

데이터 과학 분야는 소프트웨어 엔지니어링과 연구, 즉 코드 + 데이터 세트, 훈련 된 모델 및 레이블 인코딩의 조합입니다.
 버전 기록을 제어하고 몇 가지 git 명령을 사용하여 원격으로 코드 공동 작업을 수행하는 것이 기초적인 것처럼 데이터 과학자는 데이터 및 모델을 쉽게 찾아보고, 미리보고, 공유하고, 분기하고, 병합 할 수 있어야합니다.
 

원격 공동 작업을 지원하려면 버전 제어와 원격 중앙 저장소의 두 가지가 있어야합니다.
 

Git을 사용하여 소프트웨어 엔지니어가 서로 다른 버전의 코드간에 안전하게 앞뒤로 이동할 수있는 것처럼 데이터 과학자는 서로 다른 버전의 코드뿐만 아니라 서로 다른 버전의 데이터도 제어해야합니다.
 

또한 특정 버전에 대해 특정 상태를 달성하기 위해 수행 한 작업을 추적 할 수 있어야하며 필요할 때 동일한 상태를 재현 할 수 있어야합니다.
 

그렇다면 가능한 해결책은 무엇입니까?
 

## 옵션 1 : 데이터 과학 프로젝트에서 버전 제어를 위해 Git 사용
 

여러분은 이미 질문하고 계실 것입니다. 그냥 Git을 사용할 수 없습니까?
 문제는 Git의 파일 크기 제한이 100MB라는 것입니다.
 때때로 기가 바이트 단위로 실행되는 데이터 파일이있는 심각한 데이터 과학 프로젝트에는 충분하지 않습니다.
 

해결책은 Git LFS (Large File Storage)를 믹스에 추가하는 것입니다.
 

Git LFS는 Git에서 파일 크기 제한을 처리하기위한 git 확장입니다.
 대용량 데이터 파일에 대한 참조를 저장하는 포인터 파일을 생성하여이를 수행합니다.
 이러한 대용량 파일은 로컬 Git LFS 캐시 또는 GitHub 또는 Gitlab과 같은 원격 서버에 저장됩니다.
 

그래도 이것만으로는 충분하지 않습니다.
 Git LFS는 여전히 파일 크기 (약 2GB)를 제한하며 완전한 데이터 과학 솔루션이 아닙니다.
 대용량 파일 버전에서 변경된 사항에 대한 유용한 정보를 제공하지 않습니다 (포인터 파일의 텍스트 기반 변경 사항 만 해당).
 또한 시각화 또는 그래프 전후에 액세스 할 수 없습니다.
 

Git LFS는 또한 기본적으로 diff를 지원하지 않으므로 파일의 후속 버전 간의 차이점을 조사하는 것은 매우 어렵습니다.
 

## 옵션 2 : 데이터 과학 프로젝트에서 버전 제어를 위해 DVC 사용
 

더 나은 옵션은 DVC를 사용하는 것입니다.
 데이터 버전 제어를 의미하는 DVC는 본질적으로 Git과 비슷하지만 특히 데이터를 위해 만들어졌습니다.
 

그리고 DVC의 구문은 Git과 유사합니다!
 따라서 이미 Git을 알고 있다면 DVC를 배우는 것이 어렵지 않을 것입니다.
 DVC는 대용량 파일을 쉽게 추적하므로 재사용 성과 재현성이 케이크 조각입니다.
 

DVC를 사용하면 다음을 수행 할 수 있습니다.
 

- 코드를 캡처하는 것과 동일한 방식으로 데이터 및 기계 학습 모델을 추적하고 저장합니다.
 
- 데이터 버전과 ML 모델을 쉽게 생성하고 전환
 
- 데이터 세트 및 ML 아티팩트가 처음에 어떻게 구축되었는지 이해
 
- 실험 간 모델 측정 항목 비교
 
- 데이터 과학 프로젝트에서 엔지니어링 도구 및 모범 사례 채택
 

그러나 여전히 DVC는 로컬 버전 제어 만 지원합니다.
 원격 협업을 위해 설정하려면 원격 스토리지에 연결해야합니다.
 문제는이 클라우드 스토리지를 설정하는 것이 너무 번거 롭다는 것입니다.
 

예를 들어 Amazon S3를 살펴 보겠습니다.
 신용 카드를 제공하고, AWS CLI 도구를 설치하고, IAM 사용자를 생성하고, 올바른 권한을 할당해야합니다 (대부분의 사람들은 일반적으로 첫 번째 시도에서 제대로되지 않음).
 

너무 복잡합니다.
 이러한 수준의 마찰은 사람들이 원격 협업의 전체 목적인 프로젝트에 기여하지 못하게 할 수 있습니다.
 

계정 생성 및 Git 푸시만큼 간단해야합니다.
 액세스 제어도 자동으로 처리되어야합니다.
 

그리고 이것이 DagsHub Storage가 들어오는 곳입니다.
 

## 옵션 3 : 버전 제어 및 원격 공동 작업을 위해 DVC + DAGsHub 저장소 사용
 

DAGsHub Storage는 구성이 필요없는 대체 (그리고 무료로 사용할 수있는) DVC 원격입니다.
 데이터 과학자 및 기계 학습 엔지니어를위한 데이터 버전 제어 및 협업을위한 웹 플랫폼 인 DAGsHub 제작자의 새로운 도구입니다 (DAGsHub는 Github와 Git에 대한 DVC).
 

DAGsHub 스토리지를 사용하면 어떤 것도 설정해야하는 스트레스를 겪을 필요가 없습니다.
 Git 리모컨을 추가하는 것과 동일한 방식으로 작동합니다.
 

DagsHub에 리포지토리를 생성하면 자동으로 DVC 원격 URL이 제공됩니다.
 이 URL을 사용하면 기존 DAGsHub 자격 증명 (HTTPS 기본 인증을 통해)을 사용하여 데이터를 빠르게 푸시하고 가져올 수 있습니다.
 

이것은 또한 비 DVC 사용자와 작업을 공유하는 것이 훨씬 쉽다는 것을 의미합니다. 클라우드 설정이 필요하지 않기 때문입니다.
 훨씬 나아지지 않나요?
 

DAGsHub Storage를 원격 저장소로 연결하려면 DAGsHub에서 계정을 만들고 프로젝트를 만들어야합니다.
 처음부터 새로 만들거나 Github 또는 Bitbucket과 같은 다른 플랫폼의 기존 프로젝트에 연결하고 로컬 데이터 버전 관리를 위해 DVC를 설정하여이를 수행 할 수 있습니다.
 

![image](https://lh5.googleusercontent.com/pptgXgKjG8tKKl1edmThDD-fsvmckeNcOTo5lBlT3bnexEr_JgQWvaHd6z0OkLdvBF9EG5fHDnnvsRuCBppijm4QbkEJFalBGdCs-QdRnaPQFa7buMwmI6r5ez70px1yec3isZhx)

DAGsHub에서 리포지토리를 만들면 Git 및 DVC의 두 가지 원격이 제공됩니다.
 

![image](https://lh4.googleusercontent.com/HzmNRfDG774q_7TeuwytoXTk2qmbEwxlrzofsYBu0rosNI_oHfp8nZK0O_hc0w7v2vxrTTONyHrJmusQe2BXMkljb699aN2dYolx_Xgf9gbLcepxChanbTn4bghIKH6jiivdnDFu)

DAGsHub 저장소 사용을 시작하려면 DVC 링크 (저장소 홈페이지에서 찾을 수 있음)를 복사하고 로컬 프로젝트의 원격으로 추가합니다.
 

터미널에서 프로젝트를 열고 DVC 리모컨을 추가하십시오.
 

```undefined
dvc remote add <--dvc remote link-->

```

다음은 GitHub에서와 마찬가지로 로컬 머신에 DAGsHub 자격 증명을 설정하는 것입니다.
 

```undefined
dvc remote modify origin --local auth basic
dvc remote modify origin --local user Linda-Ikechukwu
dvc remote modify origin --local ask_password true
```

그리고 voilà!
 이제`dvc push -r origin` 또는`dvc pull -r origin`을 사용하여 데이터 세트와 모델을 원활하게 푸시하거나 가져올 수 있습니다.
 

git checkout처럼 데이터의 다른 버전으로 전환하려면 다음을 실행하면됩니다.
 

```undefined
git checkout <..branch or commit..>
dvc checkout

```

또 뭔데?
 DAGsHub 풀 요청을 사용하여 프로젝트에 대한 풀 요청을 수신하고 병합 할 수도 있습니다.
 

## 결론
 

DAGsHub Storage를 사용하면 데이터와 모델을 링크를 공유하는 것만 큼 쉽게 공유 할 수 있으므로 공동 작업자에게 프로젝트 데이터, 모델, 코드, 실험 및 파이프 라인에 대한 개요를 쉽게 제공 할 수 있습니다.
 

이 모든 것이 데이터 과학 팀에 더 나은 협업 경험을 제공하며 OSDS (Open Source Data Science) 프로젝트의 대규모 개발 및 수용에 도움이되기를 바랍니다.
 

이와 같은 기사를 더 찾고 계십니까?
 

제 이름은 Linda이고 Frontend 개발자입니다.
 저는 성장하는 프런트 엔드 개발자를 대상으로하는 codewithlinda 블로그를 운영합니다. 여기서는 첫 번째 기술 작업을 얻고 생존하는 방법과 레벨 업에 도움이되는 기술 팁에 대해 작성합니다.
 Twitter에서 @MsLinda를 찾을 수도 있습니다.
 