---
layout: post
title: "한 컴퓨터에서 여러 Git 구성을 사용하는 방법"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/cover-1.jpg
tags: undefined
---


여러분은 많은 고양이들을 관리하는 데 어려움을 겪을 수 있지만, Git 프로필에 관한 한 여러분이 할 수 있는 일이 있습니다.

해결책으로 바로 가보자 – 답은 `.gitconfig` 파일에 있다. Git가 어떤 구성을 사용해야 하는지 식별하기 위한 시작 지점입니다.

이 방법은 원하는 프로필을 분리하여 컴퓨터의 리포지토리를 여러 디렉터리로 분리한 다음 프로필당 `.gitconfig` 파일을 정의하는 것입니다.

## 1단계 → 별도의 저장소 디렉토리 생성

작업 중인 프로젝트를 작업하려는 프로필을 기준으로 별도의 폴더로 구성합니다.

예를 들어 작업 중인 Git 프로필이 두 개 있다고 가정해 보겠습니다. 이는 우리 대부분이 흔히 사용하는 사례입니다.

- 업무 관련 프로젝트용 `WORK` →
- 오픈 소스 및 사이드 프로젝트용 `개인용` →

## 2단계 → 글로벌 Git 구성 생성

글로벌 `.gitconfig` 파일이 아직 없는 경우 홈 디렉토리에 파일을 작성합니다. 그런 다음 아래 예제와 같이 모든 프로파일 디렉토리를 항목으로 추가합니다.

Git 디렉토리를 생성한 디렉토리 경로가 inclide의 경로 중 하나와 일치할 경우 이 작동 방식은 매우 직관적입니다.IF`이면 Git은 특정 프로파일 구성 파일을 사용합니다. 그렇지 않으면 기본 구성을 사용합니다.

## 3단계 → 프로필을 위한 개별 Git 구성 생성

지금까지 몰랐다면 글로벌 .gitconfig 파일에 .gitconfig-personal과 .gitconfig-work 파일을 언급했을 뿐 아직 생성하지 않았다. 이러한 개별 파일에는 사용자 이름 및 전자 메일에서 커밋 후크에 이르기까지 필요한 모든 사용자 지정이 포함될 수 있습니다.

## 확인하자

준비 다 됐어요! 이제 홈 디렉토리에 Git 파일이 세 개 있습니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screenshot-2021-01-03-at-3.36.24-PM.png)

이제 작업 및 개인 디렉토리에 새로운 Gitrepo를 만들고 시작하고 구성을 확인합니다.

```undefined
$ cd ~/work
$ mkdir work-test-repo
$ cd work-test-repo
$ git init
  *Initialized empty Git repository in /Users/dbarochiya/work/work-test-repo/.git/*
$ git config -l   
  *credential.helper=osxkeychain
  includeif.gitdir:~/personal/.path=~/.gitconfig-personal
  includeif.gitdir:~/work/.path=~/.gitconfig-work
  **user.name=working_me
  user.email = work@work.com**
  core.repositoryformatversion=0
  core.filemode=true
  core.bare=false
  core.logallrefupdates=true
  core.ignorecase=true
  core.precomposeunicode=true*                                                                                                                   1 

```

```undefined
$ cd ~/personal
$ mkdir personal-test-repo
$ git init
 *Initialized empty Git repository in /Users/dbarochiya/personal/.git/*
$ git config -l
 *credential.helper=osxkeychain
 includeif.gitdir:~/personal/.path=~/.gitconfig-personal
 **user.name=me_personal
 user.email=personal@personal.com**
 includeif.gitdir:~/work/.path=~/.gitconfig-work
 core.repositoryformatversion=0
 core.filemode=true
 core.bare=false
 core.logallrefupdates=true
 core.ignorecase=true
 core.precomposeunicode=true*

```

Voil➡ – e-메일과 사용자 이름은 모두 다릅니다. Gitrepo의 경로에 따라 사용자 정의 `.gitconfig` 파일을 사용할 수 있습니다.