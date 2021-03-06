---
layout: post
title: "실리콘 밸리의 Buzziest 앱인 Clubhouse를 재 설계 한 방법
 "
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/02/clubhouse-product-image-work.jpg
tags: undefined
---


소셜 미디어 씬에서 가장 인기있는 새로운 오디오 대화 앱인 Clubhouse의 사용자 경험을 개선하여 젊은 디자이너로서 제 한계를 시험하고 싶었습니다.
 

앱에서 파워 유저와 초보자 모두와 이야기를 나눈 후 앱에서 길 찾기 및 검색 가능성과 관련된 몇 가지 특정 문제점을 발견했습니다.
 이것이이 프로젝트 전반에 걸쳐 내 작업을 안내하는 주요 설계 과제가되었습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/onboarding-mockups.jpg)

면책 조항 : 저는 Clubhouse에서 일하지 않으며이 사례 연구의 견해는 엄격히 저의 것입니다.
 

신진 디자이너로서 저는이 프로젝트에 대한 저의 비전이 지나치게 야심적이고 때로는 비즈니스 목표와 사용자 데이터에 대한 가정에 의존 할 수 있음을 인정합니다.
 

완벽한 세상에서 저는 이러한 리소스에 직접 액세스하여 제 작업을 안내하는 클럽 하우스 팀과 함께 일할 것입니다.
 그때까지이 사례 연구는 제가 깊이 존경하는 제품에 대한 탐색 적 학습 경험을 의미했습니다.
 

## 브리핑
 verified_user

회원들이 문화에서 정치에 이르기까지 다양한 주제에 대해 토론 할 수있는 가상 방을 돌아 다닐 수있는 오디오 채팅 앱인 Clubhouse에 대한 흥분을 과소 평가하는 것은 어렵습니다.
 

이 앱은 베타 출시 후 한 달에 단 1,500 명의 사용자로 첫 1 억 달러를 모금했습니다.
 그리고이 글을 쓰는 시점에서 실리콘 밸리의 가장 인기있는 앱은 출시 후 9 개월 만에 대중에게 공개되기 전인 10 억 달러에 불과했습니다.
 

투자자들과의 성공 외에도 Clubhouse는 충성도가 높은 사용자 기반을 확보했으며, 창의력은 신규 사용자 온 보딩을위한 24 시간 연속 방에서 The Lion King의 라이브 프로덕션에 이르기까지 다양합니다.
 

초대 전용 플랫폼의 초기 베타 사용자로서 저는 실시간으로 제품 업데이트 (및 기하 급수적 성공)를 따르는 독특한 관점을 가졌습니다.
 그리고 저는 지금까지 가장 야심 찬 프로젝트 인 실리콘 밸리의 가장 흥미로운 앱을 최근 기억에 다시 디자인하는 것에 도전하려고했습니다.
 부담없이.
 

이 프로젝트의 높은 수준의 목표는 다음과 같습니다.
 

- Clubhouse 내에서 검색 가능성을 개선하여 사용자가 참여할 새 방, 사람 및 클럽을 더 쉽게 찾을 수 있습니다.
 
- 사용자가 가장 관련성이 높은 회의실을 필터링하고 찾을 수있는보다 원활한 복도 환경 만들기
 

## UX 과제 : 복잡한 정보 계층 구조 단순화
 

내가 고려해야 할 주요 고려 사항 중 하나는 사용자가 앱 내에서 상호 작용할 수있는 주요 구성 요소의 계층 구조였습니다.
 

- 사람 (앱의 다른 사용자)
 
- 회의실 (오디오 대화를위한 가상 회의 장소) 및
 
- 클럽 (룸을 호스팅 할 수있는 관심사 기반 그룹).
 

그 외에도 이러한 각 구성 요소가 대인 관계와 시간을 통해 연결되는 방식을 고려해야했습니다.
 

현재 Clubhouse 사용자의 복도 (홈 화면)에는 팔로우하는 사람 및 클럽에 연결된 라이브 룸이 표시됩니다 (이 사례 연구에서는 "네트워크 내"라고 함).
 이로 인해 사용자가 네트워크에서 예정된 회의실을 쉽게 추적하고 새로운 네트워크 외부 회의실에 참여하기가 어렵습니다.
 

이것은 내 작업 전반에 걸쳐 주요 이분법이되었습니다. Clubhouse의 이러한 개별 부분을 쉽게 발견 할 수 있도록하는 동시에 이들을 하나로 묶는 웹을 유지하고 단순화하는 것 사이의 균형을 찾아야했습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/ch-task-flow.jpg)

![image](https://www.freecodecamp.org/news/content/images/2021/02/ch-sketch.jpg)

## 연구 + 계획 : UX 연구원의 꿈
 

이 프로젝트의 또 다른 독특한 측면은 베타 사용자가 Clubhouse 창립자 인 Paul Davison과 Rohan Seth에 직접 액세스 할 수 있다는 점입니다.
 매주 일요일에는 두 사람이 매주 최신 제품 업데이트, 향후 로드맵, 비즈니스 목표, 최우선 순위를 공유하고 사용자가 제출 한 Q & A 공간을 공유하는 공개 포럼 인 Clubhouse Townhall을 개최합니다.
 

또한 Clubhouse의 열성적인 사용자 기반 덕분에 공식 Townhalls 다음에는 정기적으로 Townhall 요약 실 (커뮤니티 클럽에 외침)이 이어집니다. 여기에서 파워 사용자는 이번주의 업데이트와 가장 기대하는 기능에 대해 자세히 알아볼 수 있습니다.
 

클럽 하우스 타운 홀, 요약 실, 공식 및 커뮤니티가 운영하는 신규 회원 온 보딩 룸 (FAQ, Q & A 및 토론 포함) 사이에서 저는 가능한 한 많은 비즈니스 통찰력과 목표를 얻기 위해 6 주 동안 주당 평균 5 시간을 보냈습니다.
 내 제한된 유리한 지점에서.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/clubhouse-research-screenshots.jpg)

이러한 논의에서 클럽 하우스 팀의 가장 중요한 목표는 다음과 같습니다.
 

- 모든 사람이 클럽 하우스를 이용할 수 있도록 만들기 : Paul은 항상 팀의 최우선 과제가 품질을 희생하지 않으면 서 가능한 한 빨리 클럽 하우스를 확장하는 것임을 분명히했습니다.
 
- 제작자 우선 : Paul이 결코 과소 평가하지 않은 또 다른 점은 제작자 수익을 창출 할 수있는 도구를 구축하는 플랫폼 제작자에 대한 팀의 우선 순위였습니다.
 
- 검색 가능성 및 제안 된 콘텐츠 개선 :이 프로젝트 당시 Clubhouse는 관련 방을 점진적으로 쉽게 찾을 수 있도록 주제 디렉토리와 알고리즘을 적극적으로 구축했습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/clubhouse-sketches.jpg)

## 고급 사용자부터 초보자까지 사용자 인터뷰
 

저는 고급 사용자와 일반 커뮤니티 회원 모두와 같은 Clubhouse 사용자와 대화하여 현재 앱의 검색 경험과 관련하여 겪었던 문제를 파악했습니다.
 이 인터뷰를 통해 다음과 같은 통찰력을 얻었습니다.
 

- 경량 유지 : 대부분의 사용자는 개인 캘린더에서 예정된 회의실을 예약하는 것을 원하지 않는 자연스러운 경험을 위해 회의실 검색을 선호했습니다.
 
- 어수선한 복도 : 대부분의 사용자는 복도가 현재 큐레이팅 된 방식과 팔로우 한 사람들 중 주어진 방에있는 사람이 누구인지 혼란스러워했습니다.
 
- 발견의 원천으로서의 복도 : 복잡한 복도 환경에도 불구하고 대부분의 사용자는 기존 (아직 강력하지는 않음) "탐색"탭이 있음에도 불구하고 여전히 복도에 의존하여 새 방을 찾았습니다.
 
- 친구 우선 : 복도에 들어갈 방을 결정할 때 사용자는 만장일치로 특정 방에있는 친구를보고 싶어했습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/affinity-map--1-.jpg)

그렇다면 가벼운 네트워크 외부 발견을 용이하게하는 동시에 복도를 자발적인 상호 작용을위한 명확하고 간결한 장소로 만드는 방법은 무엇일까요?
 

## UX 솔루션 : Discovery-to-Hallway 파이프 라인 간소화
 

복도와 방에서 길을 더 쉽게 찾을 수 있도록 간단하면서도 강력한 UI를 개발했습니다.
 또한 발견 페이지를 통해 찾은 방을 복도로 쉽게 가져올 수 있습니다.
 

이 솔루션이 응집력 있고 사일로 화되지 않은 느낌을 받으려면 5 가지 주요 경험으로 나눠진 Clubhouse의 거의 완전한 재 설계를 구현해야했습니다.
 

여기에서 최종 프로토 타입으로 플레이하세요.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/clubhouse-wireframes.jpg)

## 경험 1 : 복도
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/ch-hallway-before-after.jpg)

사용자는 복도 경험이 더 의도적이고 통제 할 수 있기를 원했습니다.
 이를 위해 다음과 같은 최상위 계층 구조를 설정했습니다.
 

- 사용자가 활성 회의실을 볼 수있을뿐만 아니라 네트워크 내에서 예약 된 회의실에 대한 빠른 개요를 볼 수 있도록 진행 중 vs. 예정
 
- 온 보딩 중에 사용자가 선택한 관심 주제별로 필터링
 
- 복도의 방을 사람과 팔로우하는 클럽별로 정렬
 

추가 UI 결정은 복도의 방 내에서 팔로우하는 사람들 만 표시하는 것이 었습니다.
 이것은 현재 복도의 방 카드에서 사용자가 보는 이름을 둘러싼 모호성의 현재 문제를 완화합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/hallway-recording-1-.gif)

## 경험 2 : 방 미리보기
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/room-preview-recording-2-.gif)

현재 Clubhouse에서 복도의 방을 클릭하면 즉시 해당 방의 대화로 이동합니다.
 

어떤 방에서든 친구를 식별하는 것은 방에 참여하는 사용자에게 중요한 결정 요소이므로 사용자가 참여하기 전에 내부에서 아는 사람을 볼 수있는 방법을 설계하고 싶었습니다.
 

## 경험 3 : 발견
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/ch-explore-page-before-and-after--1-.jpg)

현재 Clubhouse의 검색은 숨겨져 있습니다. 사용자는 탐색 탭으로 이동하여 카테고리 및 키워드별로 사람과 클럽을 검색하고 캘린더 탭으로 이동하여 모든 Clubhouse에서 활성화 된 회의실과 예정된 회의실을 모두 검색합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/ch-save-room-page-after.jpg)

실제로 대부분의 참가자는 발견이라는 기본 목표를 달성하기 위해이 탭을 사용하지 않았습니다.
 대신 그들은 사용자 프로필을 통해 클럽을 발견하고, 방을 통해 사람을 발견하고, 주로 복도를 통해 방을 발견하는 등의 해결 방법을 채택하여 노출되는 콘텐츠의 범위를 제한했습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/discovery-filter-recording-1-.gif)

이러한 해결 방법을 더 원활하게 만들기 위해 UI 솔루션을 설계했지만 검색 페이지가 이러한 모든 사용 사례를 수용 할 수있는 목적지가되기를 원했습니다. 그러면 사용자가 Clubhouse의 증가하는 주제 디렉토리에서 사람, 클럽 및 회의실을 검색 할 수 있습니다.
 키워드에 추가.
 

또한 검색을 더욱 용이하게하기 위해 추가 정렬 기능을 통합했습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/discovery-recording-1-.gif)

또한 사용자는 네트워크 외부 회의실을 검색하고 액세스 할 수있는 쉽고 가벼운 솔루션을 원했습니다.
 

방의 중재자, 해당 클럽을 따르거나 개인 캘린더의 일정을 따르지 않고 탐색 피드에서 복도로 방을 보내는 기능은 직관적 인 느낌을주기 위해 여러 번 반복하는이 프로젝트의 가장 큰 도전이었습니다.
 

## 경험 4 : 활성 사용자
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/ch-active-users-before-after.jpg)

복도에 가까운 사촌 인 활성 사용자 화면은 현재 온라인 상태 인 모든 클럽 하우스 사람과 클럽이있는 곳입니다.
 인터뷰에 응한 사용자의 83 %는이 화면을 스캔하여 친구들이 어떤 방에 있는지 빠르게 식별한다고 언급했습니다.
 

친구 찾기를 더욱 용이하게하기 위해 많은 요청을받은 검색 창과 정렬 드롭 다운 메뉴를 추가하여 훨씬 더 중요한 구분 (방에 적극적으로 참여하는 사람과 그냥 듣는 사람)에 도달했습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/active-users-recording-1-.gif)

## 경험 5 : 사용자 및 클럽 프로필
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/club-prof-before-after.jpg)

87 %의 사용자가 사용자 프로필을 통해 직접 팔로우하기에 적합한 클럽을 찾습니다.
 클럽에는 팔로워 (알림을 받고 복도에서 클럽 브랜드 룸을 보는 사람)와 회원 (위에 추가하여 클럽 브랜드 룸을 시작할 수있는 사람)과 같은 추가 계층이 있습니다.
 

Clubhouse의 현재 디자인에서 사용자가 팔로우하는 클럽과 사용자가 회원 인 클럽은 서로 다른 위치에 있습니다. 사용자의 다음 목록과 사용자 프로필 하단에 각각 있습니다.
 이것은 특정 사람과 관련된 모든 클럽을 스캔하려는 사용자에게 혼란 스러웠습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/user-club-profile-recording-1-.gif)

사용자와 연결된 클럽을 통합 메트릭으로 만들면 해당 프로필을 방문하는 사용자는 자신이 속한 클럽을보다 쉽게 확인하고 새 화면을 방문하지 않고도 즉시 팔로우 할 수 있습니다.
 

클럽 수준에서 이전에 개최 한 회의실, 예정된 회의실 및 클럽 관리자와 같은 메타 데이터에 액세스 할 수 있으면 사용자가 클럽에 대한보다 효과적인 개요를 얻을 수 있습니다.
 

## UI 및 브랜딩 : 다크 UI 사례
 

이 경험의 모든 부분을 하나로 모으는 과정에서 시각적 요소를 너무 많이 추가하면 앱을 쉽게 이동하는 데 필요한 시각적 계층 구조가 손상된다는 것이 분명해졌습니다.
 

또한 Clubhouse의 일반적인 사용자 경험은 이미 너무나 몰입감이 넘치고 감성적이며 종종 밤 내내 지속됩니다. 저는이 사용 사례를 활용하고 Clubhouse의 몇 가지 콘텐츠 유형을 조화롭게 강조하는 우아한 UI를 구현하고 싶었습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/CH-style-tile.jpg)

## 사용성 테스트 : 앱 전체에서 검색 가능성과 검색 가능성이 얼마나 효율적입니까?
 

사용성 테스트를 수행 한 후 테스트 중에 통찰력, 동작 및 결과가 포함 된 선호도 맵을 만들었습니다.
 

대부분의 사용자는 실수가 거의 또는 전혀없이 앱을 통해 이동했지만 많은 참가자에게이 재 설계의 핵심 요소를 방해하는 주요 마찰 지점이있었습니다.
 

발견 페이지에서 복도로 저장 한 방에 액세스하는 방법이 아직 명확하지 않았습니다.
 

## 사용성 테스트 통찰력 및 우선 순위 변경
 

처음에는 발견 탭에있는 네트워크 외부 회의실이 방에 출연 한 사용자가 복도에 표시하도록 설계했습니다.
 그러면 복도에 알고리즘 방식으로 표시되며 "정렬 기준"드롭 다운 메뉴를 통해 추가로 검색 할 수 있습니다.
 이것에 몇 가지 문제가있었습니다.
 

- 원래 디자인은 기본적으로 이러한 방을 저장된 항목으로 취급하여 복도에있는 다른 방보다이 방의 우선 순위를 우연히 (그리고 잘못) 지정했습니다.
 
- 이 치료는 자발적인 방 생성을 방해하거나 일반적으로 네트워크 외부 방의 우선 순위를 부당하게 지정하는 데 더 큰 영향을 미칠 수 있습니다.
 
- 그 외에도 정렬 드롭 다운에 저장된 항목을 포함하는 것은 직관적이지 않았거나 이러한 유형의 콘텐츠를 찾을 수있는 장소가 아니 었습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/set-notifications-flow-recording-2-.gif)

## 결론 : 교훈 및 여기서 우리가가는 곳
 

이 프로젝트에 참여하면서 저는 이것이 젊은 디자이너에게 야심 찬 도전이 될 것이라는 것을 알았습니다.
 제가 몰랐던 것은 그 도전이 얼마나 복잡하고 포괄적 인 것인지였습니다.
 

널리 알려져 있고 사랑받는 제품을 작업하는 데는 (겉보기에) 모든 사람이 올바르게해야하는 많은 외부 압력과 내부 감정이 수반된다는 것을 배웠습니다.
 

기존 구조에 대한 애착이 강한 고급 사용자와 정적 프로토 타입으로 오디오 앱의 뉘앙스를 충분히 경험할 수없는 신규 사용자가 있습니다.
 

그런 다음, 작지만 강력한 Clubhouse 팀이 있습니다.이 팀은 매주 제품을 적극적으로 반복하여 제가 작업중인 동일한 과제에 대해 스스로 상상력이 풍부한 솔루션을 출시 할 수 있습니다.
 그리고 아직 상상하지 못한 다른 사람들 도요
 

거의 미묘하게 느껴지는 흥미 진진한 제품에 대한 공개적인 대화의 끊임없는 흐름에 대해, 나는이 압력이 저에게 가장 좋은 때가 있었고 그녀가 씹을 수있는 것보다 훨씬 더 많은 것을 깨달은 총 사기꾼처럼 느꼈다는 것을 겸손하게 인정할 것입니다.
 .
 

이 프로젝트가 저에게 가르쳐 준 가장 큰 교훈은 복잡한 도전에 직면했을 때의 인내, 실패를인지 한 후의 은혜, "충분히 좋은"(물론이 반복을 위해) 괜찮을 때 사이의 섬세한 균형이었습니다.
 

결국 저는 제 디자인 여정의이 단계에서이 프로젝트를 통해 이룰 수 있었던 것을 매우 자랑스럽게 생각합니다.
 그리고 나는 처음에 제품 디자인으로 이끈 내가 가장 좋아하는 만트라를 자주 떠 올렸다.
 

> "내가 원했던 건 책 같은 일이어서 평생 끝낼 수있을 정도였다."
 

제품 디자인은 저에게있어 그 일입니다.이 프로젝트 (및 다른 모든 프로젝트)가 완전히 완료되지는 않을 것이지만 가능한 한 많은 생명을 불어 넣었다는 것을 자랑스럽게 생각합니다. 즐겁게 즐기 셨기를 바랍니다.
 