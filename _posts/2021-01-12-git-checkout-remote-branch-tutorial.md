---
layout: post
title: "Git Checkout 원격 분기 튜토리얼"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1501605623075-d5715e4637ab?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDE0fHxicmFuY2h8ZW58MHx8fA&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


Git은 다양한 버전의 응용 프로그램을 유지 관리하고 볼 수 있는 버전 제어 도구입니다. 새 업데이트로 인해 앱이 중단되면 Git를 통해 변경 내용을 이전 버전으로 되돌릴 수 있습니다.

Git를 사용하면 버전 관리 외에도 여러 환경에서 동시에 작업할 수 있습니다. 이 컨텍스트의 여러 환경은 분기를 의미합니다.

## 분기가 필요한 이유

Git을 사용하는 경우 마스터 환경(주 환경이라고도 함)이 생성됩니다. 이 분기는 앱이 프로덕션 준비가 되었을 때 배포되는 소스 코드를 보유합니다.

앱을 업데이트하려는 경우 이 분기에 커밋(변경사항)을 더 추가할 수도 있습니다. 사소한 변화에는 큰 문제가 되지 않을 수 있지만, 큰 변화에는 이상적이지 않습니다. 그래서 다른 지점들이 존재하는 것입니다.

새 분기를 만들고 사용하려면 프로젝트 디렉터리의 터미널에서 다음 명령을 사용합니다.

```undefined
# create a new branch
git branch branch-name
# change environment to the new branch
git checkout branch-name

```

이 새 분기에서 새 변경사항을 작성할 수 있습니다. 그런 다음 작업이 완료되면 마스터 분기와 병합할 수 있습니다.

지점의 또 다른 이점은 여러 개발자가 동일한 프로젝트를 동시에 작업할 수 있도록 허용한다는 것입니다. 여러 개발자가 동일한 마스터 분기에서 작업하는 경우 재해가 발생할 수 있습니다. 각 개발자의 코드 간에 너무 많은 변경 사항이 있으며, 일반적으로 병합 충돌로 끝납니다.

Git을 사용하면 다른 지점(다른 환경)에서 작업을 진행하는 동안 다른 지점(다른 환경)에서 작업을 변경할 수 있습니다.

## Git Checkout Remote Branch는 무엇을 의미합니까?

Git로 프로젝트를 시작하면 컴퓨터에 존재하는 로컬 마스터 분기 및 GitHub와 같은 Git 지원 플랫폼에 존재하는 원격 마스터 분기의 두 가지 환경이 나타납니다.

로컬 마스터 분기에서 원격 마스터 분기로 변경 내용을 푸시하고 원격 분기에서 변경 내용을 가져올 수도 있습니다.

분기를 로컬로 만들 때 분기가 원격 분기가 되는 GitHub로 푸시될 때까지 분기만 로컬로 존재합니다. 이는 다음 예에 나와 있습니다.

```undefined
# create a new branch
git branch new-branch
# change environment to the new branch
git checkout new-branch
# create a change
touch new-file.js
# commit the change
git add .
git commit -m "add new file"
# push to a new branch
git push --set-upstream origin new-branch

```

위의 예에서 `원래 새 지점`은 원격 분기가 됩니다. 이미 알고 계시겠지만, 저희는 새 분기를 만들고 새 원격 분기로 진행하기 전에 분기를 변경했습니다.

하지만 만약 원격지점이 이미 존재한다면, 그리고 우리가 그 지점과 그 모든 변화를 우리의 지역 환경에 끌어들이고 싶다면요?

여기가 바로 "Git Checkout Remote Branch"입니다.

## 체크아웃 원격 분기를 가져오는 방법

다른 개발자가 만든 원격 지점이 있는데 그 지점을 끌어당기고 싶다고 가정해 보겠습니다. 다음과 같은 방법으로 해결할 수 있습니다.

### 1. 모든 원격 지점 가져오기

```undefined
git fetch origin

```

리포지토리에서 모든 원격 분기를 가져옵니다. `➡`은 당신이 목표로 하는 원격 이름입니다. 따라서 "업스트림" 원격 이름을 가지고 있다면 "git fetch upstream"이라고 부를 수 있습니다.

### 2. 체크아웃할 수 있는 지점

체크아웃에 사용할 수 있는 분기를 보려면 다음을 실행하십시오.

```undefined
git branch -a

```

이 명령의 출력은 체크아웃에 사용할 수 있는 분기 목록입니다. 원격 분기의 경우 `원격/원본` 접두사를 사용합니다.

### 3. 원격 분기에서 변경 사항 가져오기

원격 분기에서 직접 변경할 수 없습니다. 따라서 해당 지점의 복사본이 필요합니다. 원격 지점 `고장 테스트`를 복사하고 싶다고 가정해 보겠습니다.

```undefined
git checkout -b fix-failing-tests origin/fix-failing-tests

```

이렇게 하면 다음과 같은 이점이 있습니다.

- `고정-고정-고정`이라는 새로운 지점을 만든다.
- 그 지점이다.
- `변형/고정-고정-고정`에서 해당 지점으로 이동

그리고 이제 당신은 그 외딴 지점의 복사본을 가지고 있습니다. 또한 원격 분기에 커밋을 푸시할 수도 있습니다. 예를 들어 다음과 같은 새 커밋을 수행할 수 있습니다.

```undefined
touch new-file.js
git add .
git commit -m "add new file"
git push

```

이를 통해 약속된 변경 사항을 `원점/고장-고장-고장-고장-고장-고장-고장-고장-고장-고장-고 만약 당신이 알아차렸다면, 우리는 어디에서 변경을 추진하고 있는지 명시할 필요가 없었다(예: "git push origin fix-failing-tests"). 이는 Git가 원격 분기를 추적하도록 로컬 분기를 자동으로 설정하기 때문입니다.

## 결론

Git 분기를 사용하면 애플리케이션 개발 중에 쉽게 협업할 수 있습니다.

분기를 사용하면 서로 다른 개발자가 애플리케이션의 여러 부분에서 동시에 쉽게 작업할 수 있습니다.

Checkout Remote Branch에서는 개발자가 시스템의 원격 분기를 로컬로 복사하고, 변경하고, 원격 분기에 푸시할 수 있기 때문에 공동 작업이 더욱 원활해집니다.