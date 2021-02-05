---
layout: post
title: "Pro와 같은 Android에서 모델-뷰-뷰 모델을 사용하는 방법"
author: 'Code Tower'
thumbnail: https://images.unsplash.com/photo-1503387762-592deb58ef4e?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MXwxMTc3M3wwfDF8c2VhcmNofDV8fGNvbnN0cnVjdGlvbnxlbnwwfHx8&ixlib=rb-1.2.1&q=80&w=2000
tags: undefined
---


이 기사에서 나의 목표는 모델-뷰-뷰 모델 아키텍처 패턴이 GUI 아키텍처의 프레젠테이션 논리와 관련하여 일부 상황에서 매우 어색한 우려 분리를 제공하는 이유를 설명하는 것이다.

프로젝트 요구 사항에 따라 MVVM의 두 가지 변형(한 가지 방법만 있는 것은 아님)과 한 변형을 다른 변형보다 선호하는 이유에 대해 알아보겠습니다.

## MVP/MVC와 MVP 비교?

내가 생방송 일요일 Q 동안 가장 많이 받는 질문일 가능성이 높다.

> MVP/MVC와 MVP 비교?

이 질문을 받을 때마다 단일 GUI 아키텍처가 모든 상황에서 잘 작동하는 것은 아니라는 생각을 재빨리 강조합니다.

왜, 물어봐도 돼? 주어진 응용 프로그램에 대한 최상의 아키텍처(또는 적어도 좋은 선택)는 당면한 요구 사항에 따라 크게 좌우됩니다.

이 단어 요구 사항이 실제로 무엇을 의미하는지 간략하게 살펴보겠습니다.

- UI가 얼마나 복잡합니까? 단순 UI는 일반적으로 이를 조정하는 데 복잡한 논리가 필요하지 않은 반면, 복잡한 UI는 원활한 작동을 위해 광범위한 논리와 세분화된 제어가 필요할 수 있다.
- 당신은 시험에 얼마나 신경을 쓰십니까? 일반적으로, 프레임워크와 OS(특히 사용자 인터페이스)에 긴밀하게 결합되는 클래스는 테스트하기 위해 추가 작업이 필요하다.
- 얼마나 많은 재사용과 추상화를 장려하고 싶으십니까? 애플리케이션의 백엔드, 도메인 및 프레젠테이션 로직을 서로 다른 플랫폼에서 공유하려면 어떻게 해야 합니까?
- 당신은 천성적으로 실용적인가, 완벽주의적인가, 게으른가, 또는 다른 상황에서 위의 모든 것을 다른 시간에 하는가?

위에 열거된 요구 사항과 우려 사항에 대해 MVVM이 어떻게 작동하는지 자세히 논의하는 기사를 쓰고 싶습니다. 불행하게도, 여러분 중 일부는 MVVM을 할 수 있는 한 가지 방법밖에 없다고 잘못 생각했을 것이다.

대신, 매우 뚜렷한 장점과 단점을 제시하는 MVVM의 일반적인 아이디어에 대한 두 가지 접근 방식에 대해 토론할 것이다. 하지만 먼저, 일반적인 아이디어부터 시작하겠습니다.

## 뷰 클래스를 참조하지 않아야 합니다.

오래된 영어를 읽지 못하는 내 친구들을 위해: "당신은 보기 수업을 참조하지 않을 수 있습니다."

ViewModel(클래스가 로직으로 가득 찬 경우 그 자체가 혼란스러운 경우)이라는 이름을 사용하는 것 외에도 MVVM 아키텍처의 철칙 중 하나는 ViewModel에서 View를 참조할 수 없다는 것입니다.

자, 첫 번째 혼동의 영역은 이 단어 "참조"에서 발생할 수 있습니다. 이 단어는 여러 가지 다른 수준의 전문 용어를 사용하여 다시 설명하겠습니다.

- View Model에는 뷰에 대한 참조(멤버 변수, 속성, 돌연변이/불가변 필드)가 없을 수 있습니다.
- 뷰 모델은 뷰에 의존하지 않을 수 있습니다.
- View Model이 View와 직접 통화할 수 없습니다.

자, 안드로이드 플랫폼에서, 이 규칙을 어기는 이유는 단순히 소프트웨어 아키텍처에 대해 아는 것처럼 보이는 사람이 나쁘다고 해서 나쁜 것이 아니기 때문입니다.

아키텍처 구성 요소의 View Model 클래스(해당되는 경우 인스턴스가 조각/활동 수명 주기보다 오래 지속되도록 설계됨)를 사용할 때 보기를 참조하면 심각한 메모리 누수가 요구됩니다.

MVVM이 일반적으로 이러한 참조를 허용하지 않는 이유에 대해, 목표는 가정적으로 View 및 View Model을 테스트하고 쓰기 쉽게 만드는 것이다.

다른 사람들도 그것이 View Model의 재사용을 촉진한다고 지적할 수 있지만, 이것이 바로 이러한 패턴으로 인해 문제가 되는 부분입니다.

코드를 살펴보기 전에 개인적으로 라이브 데이터를 생산 코드에서 사용하지 않는다는 점에 유의하십시오. 요즘은 나만의 Publisher-Subscriber 패턴을 쓰는 것을 선호하지만, 아래에서는 View Model에서 View로 PubSub/Observer Pattern 링크를 허용하는 모든 라이브러리에 적용됩니다.

이 자료에는 다음과 같은 여러 가지 아이디어를 다루는 비디오 튜토리얼이 첨부되어 있습니다.

## ViewLogic + View모델 또는 보기 + 보기모델 컨트롤러?

앞부분에서 `파단`이라고 했을 때, 말 그대로 패턴이 깨진다는 뜻은 아닙니다. 내 말은, 그것은 (적어도) 매우 뚜렷한 외양, 이점, 그리고 결과를 가진 두 가지 다른 접근법으로 구분된다는 것이다.

이 두 가지 접근 방식을 고려해보도록 하겠습니다. 다른 접근 방식보다 하나를 더 선호할 수 있을 때 말이죠.

![image](https://www.freecodecamp.org/news/content/images/2020/12/1_TfbPt5-CcYCjDu2hapFXNg.png)

### 첫 번째 접근 방식: 재사용 가능한 뷰 모델의 우선 순위 지정

내가 알 수 있는 한, MVVM을 구현하는 대부분의 사람들은 View Models의 재사용을 촉진하는 것을 목표로 하여 n개의 다른 보기(다대일 비율)에 재사용될 수 있다.

간단히 말해서, 이러한 재사용을 달성할 수 있는 두 가지 방법은 다음과 같습니다.

- 특정 보기를 참조하지 않음. 이 시점에서 이것은 당신에게 새로운 것이 아니기를 바랍니다.
- 일반적으로 UI의 세부 정보를 최대한 적게 파악함

두 번째 요점은 모호하거나 직관적이지 않은 것으로 들릴 수 있으므로(어떻게 하면 참조하지 않는 것에 대해 무엇을 알 수 있는가?) 몇 가지 코드를 살펴봐야 할 때입니다.

```undefined
class NoteViewModel(val repo: NoteRepo): ViewModel(){
    //Note: you may also publish data to the View via Databinding, RxJava Observables, and other approaches. Although I do not like to use LiveData in back end classes, it works great with Android front end with AAC
    val noteState: MutableLiveData<Note>()
    //...
    fun handleEvent(event: NoteEvent) {
        when (event) {
            is NoteEvent.OnStart -> getNote(event.noteId)
            //...
        }
    }
    private fun getNote(noteId: String){
        noteState.value = repo.getNote(noteId)
    }
}
```

이것은 매우 간단한 예이지만, 요점은 이 특정 View Model이 handleEvent 기능을 제외하고 공개적으로 노출하는 유일한 것은 간단한 Note 객체라는 것입니다.

```undefined
data class Note(val creationDate:String,
                val contents:String,
                val imageUrl: String,
                val creator: User?)
```

이러한 특별한 접근 방식을 통해, View 모델은 특정 View뿐만 아니라 세부 정보, 나아가 특정 View의 프레젠테이션 로직에서 완전히 분리됩니다.

만약 내가 말하는 것이 여전히 모호해 보인다면, 다른 접근 방식을 묘사한 후에 분명해질 것이라고 약속할게.

이전 제목인 "ViewLogic + View"에도 불구하고모델…"은 사용되거나 심각하게 고려되지 않습니다. 즉, 매우 분리되고 재사용 가능한 View Model을 사용함으로써 이제 화면에서 이 노트 개체를 렌더링/바인딩하는 방법을 찾는 작업을 View 자체에 의존하게 됩니다.

우리들 중 일부는 Logic으로 View 클래스를 채우는 것을 좋아하지 않는다.

이것이 바로 상황이 매우 혼탁해지고 프로젝트 요구 사항에 따라 달라지는 이유입니다. View 클래스를 다음과 같은 논리로 채운다는 것은 아닙니다.

```undefined
private fun observeViewModel() {
    viewModel.notes.observe(
        viewLifecycleOwner,
        Observer { notes: List<Note> ->
            if (notes.isEmpty()) showEmptyState()
            else showNoteList(notes)
        }
    )
   //..
}
```

…은 항상 나쁜 것이지만, (예: 단편) 플랫폼에 단단히 연결된 클래스는 테스트하기 어렵고, 논리가 포함된 클래스는 테스트하는 데 가장 중요한 클래스입니다!

한 마디로 말해서, 제가 생각하는 어떤 좋은 아키텍처의 황금 원칙도 적용하는데 실패하는 것입니다. 문제의 분리.

내 개인적인 의견은 우려의 분리를 매우 높은 수준으로 적용하는 것이 가치가 있다는 것이다. 하지만 그것이 무엇을 의미하는지 전혀 알지 못하는 사람들에 의해 많은 금전적 지원서가 작성되었다는 것을 실수하지 마세요.

어떤 경우든, 우리가 다음에 논의할 접근 방식은 자체적인 부작용을 가지면서도 다시 한 번 View에서 프레젠테이션 논리를 제거합니다.

어쨌든 대부분은요.

### 두 번째 접근 방식: 겸손한 보기, 제어-기묘한 보기 모델

View 모델의 재사용 우선 순위를 매기는 결과로써, 때로는 보기를 세부적으로 제어하지 못하는 경우도 있습니다. 실제로 좀 짜증나는 경우가 있습니다.

이전 접근 방식을 무차별적으로 적용하는 데 대한 열정이 훨씬 덜해지도록 하기 위해 View Model을 재사용할 필요가 없는 경우가 많습니다.

> 아이러니하게도, "너무 추상화"는 MVP를 MVP에 대한 일반적인 비평이다.

따라서 단순히 뷰 모델에 참조를 다시 추가하여 뷰에 대한 세분화된 제어 권한을 되찾을 수는 없습니다. 이는 기본적으로 MVP + 메모리 누수일 뿐입니다(AAC의 View Model을 여전히 사용 중인 경우).

또한 주어진 보기의 거의 모든 동작, 상태 및 프레젠테이션 논리를 포함할 수 있도록 View Model을 구축할 수도 있습니다. View는 여전히 View Model에 바인딩되어야 하지만 View 모델에 대한 충분한 세부 정보가 있으므로 View의 기능이 하나의 라인으로 축소됩니다(작은 예외).

Martin Fowler의 명명 규칙에서 이를 Passive View/Screen이라고 합니다. 이 접근법에 더 일반적으로 적용할 수 있는 이름은 겸손한 개체 패턴입니다.

이를 위해서는 View 모델에 다음과 같은 모든 컨트롤 또는 위젯에 대해 관찰 가능한 필드(데이터 바인딩, Rx, Live Data 등)가 있어야 합니다.

```undefined
class UserViewModel(
    val repo: IUserRepository,
){

    //The actual data model is kept private to avoid unwanted tampering
    private val userState = MutableLiveData<User>()

    //Control Logic
    internal val authAttemptState = MutableLiveData<Unit>()
    internal val startAnimation = MutableLiveData<Unit>()

    //UI Binding
    internal val signInStatusText = MutableLiveData<String>()
    internal val authButtonText = MutableLiveData<String>()
    internal val satelliteDrawable = MutableLiveData<String>()

    private fun showErrorState() {
        signInStatusText.value = LOGIN_ERROR
        authButtonText.value = SIGN_IN
        satelliteDrawable.value = ANTENNA_EMPTY
    }
    //...
}
```

그 후에는 View가 View Model에 직접 연결해야 하지만, View에 필요한 기능은 다음과 같이 쓰기가 매우 간단해집니다.

```undefined
class LoginView : Fragment() {

    private lateinit var viewModel: UserViewModel
    //...
    
    //Create and bind to ViewModel
    override fun onStart() {
        super.onStart()
        viewModel = ViewModelProviders.of(
        //...   
        ).get(UserViewModel::class.java)

        //start background anim
        (root_fragment_login.background as AnimationDrawable).startWithFade()

        setUpClickListeners()
        observeViewModel()

        viewModel.handleEvent(LoginEvent.OnStart)
    }

    private fun setUpClickListeners() {
      //...
    }

    private fun observeViewModel() {
        viewModel.signInStatusText.observe(
            viewLifecycleOwner,
            Observer {
                //"it" is the value of the MutableLiveData object, which is inferred to be a String automatically
                lbl_login_status_display.text = it
            }
        )

        viewModel.authButtonText.observe(
            viewLifecycleOwner,
            Observer {
                btn_auth_attempt.text = it
            }
        )

        viewModel.startAnimation.observe(
            viewLifecycleOwner,
            Observer {
                imv_antenna_animation.setImageResource(
                    resources.getIdentifier(ANTENNA_LOOP, "drawable", activity?.packageName)
                )
                (imv_antenna_animation.drawable as AnimationDrawable).start()
            }
        )

        viewModel.authAttemptState.observe(
            viewLifecycleOwner,
            Observer { startSignInFlow() }
        )

        viewModel.satelliteDrawable.observe(
            viewLifecycleOwner,
            Observer {
                imv_antenna_animation.setImageResource(
                    resources.getIdentifier(it, "drawable", activity?.packageName)
                )
            }
        )
    }
```

이 예제의 전체 코드는 여기에서 찾을 수 있습니다.

아마 아시겠지만, 우리는 이 View 모델을 다른 곳에서는 다시 사용하지 않을 것입니다. 또한 View는 충분히 겸손해졌으며(코드 적용 범위에 대한 표준 및 선호도에 따라), 매우 쉽게 작성되었습니다.

때로는 보기와 보기 모델 간의 프레젠테이션 로직 분포 간에 어떤 종류의 절반의 측정값을 찾아야 하는 상황에 직면할 수 있습니다. 이 경우 이러한 접근 방식 중 하나를 엄격하게 따르지 않습니다.

저는 한 가지 접근 방식을 다른 접근 방식에 대해 옹호하는 것이 아니라, 당면한 요구 사항에 따라 접근 방식에 유연성을 갖도록 권장하고 있습니다.

## 선호도와 요구 사항에 따라 아키텍처 선택

이 기사의 요점은 개발자가 안드로이드 플랫폼에서 MVVM 스타일 GUI 아키텍처를 구축하는 측면에서 취할 수 있는 두 가지 접근 방식을 살펴보는 것이다.

사실, 우리는 이 두 가지 접근법 내에서조차 작은 차이점에 대해 더 구체적일 수 있습니다.

- View는 보유하고 있는 모든 개별 위젯/컨트롤에 대해 필드를 관찰해야 하는가, 아니면 매번 전체 보기를 새로 렌더링하기 위해 단일 모델을 게시하는 필드를 관찰해야 하는가?
- 발표자 또는 컨트롤러 같은 것을 혼합물에 추가하는 것만으로 View 모델을 일대일로 만드는 것을 피할 수 있을까요?

대화는 싸고, 이런 것들을 코드로 배워볼 것을 강력히 권하고 싶습니다. 그래야 저 같은 사람에게 의지해서 어떻게 해야 할지 알 필요가 없습니다.

궁극적으로, 훌륭한 아키텍처를 만드는 두 가지 요소는 다음과 같은 고려 사항으로 귀결된다고 생각합니다.

우선, 여러분이 원하는 것을 찾을 때까지 몇 가지 접근 방식을 가지고 놀아라. 이는 각 스타일의 애플리케이션을 실제로 구축하고(간단할 수 있음) 무엇이 옳은지 확인하는 것이 가장 좋습니다.

둘째로, 선호도는 차치하고, 다른 스타일은 다른 결손에 대한 대가로 다른 이익을 강조하는 경향이 있다는 것을 이해하라. 결국, 여러분은 맹목적인 믿음보다는 프로젝트 요구 사항에 대한 이해에 따라 좋은 선택을 할 수 있을 것입니다.

### 소프트웨어 아키텍처에 대해 자세히 알아보기:

https://www.instagram.com/rkay301/
https://www.facebook.com/wiseassblog/
https://twitter.com/wiseass301
http://wiseassblog.com/