---
layout: post
title: "단 15분 만에 초보자를 위한 HTML 기초 배우기"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/Ep10_html.png
tags: undefined
---


웹 사이트를 구축하려면 가장 먼저 배워야 할 언어는 HTML입니다.

이 기사에서는 HTML의 기본에 대해 알아보려고 합니다. 마지막에는 HTML만을 이용한 기초 웹사이트를 만들 것입니다.

다음은 이 기사를 보완하려는 경우 볼 수 있는 비디오입니다.

## HTML이란 무엇인가?

하이퍼텍스트 마크업 언어를 의미하는 HTML은 꽤 간단한 언어이다. 그것은 우리가 웹페이지를 구성하기 위해 사용하는 다른 요소들로 구성되어 있다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-11-at-1.16.17-PM.png)

## HTML 요소란 무엇인가?

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-11-at-1.16.34-PM.png)

요소는 일반적으로 요소의 이름으로 구성된 여는 태그로 시작합니다. 이것은 여닫이 앵글 브래킷으로 포장되어 있습니다. 시작 태그는 요소가 시작되는 위치를 나타냅니다.

오프닝 태그와 마찬가지로, 클로징 태그도 오프닝 및 클로징 앵글 브래킷으로 포장됩니다. 그러나 요소 이름 앞에 슬래시를 포함하기도 합니다.

개폐 태그 안의 모든 것이 내용입니다.

하지만 모든 요소가 이 패턴을 따르는 것은 아닙니다. 우리는 그것들을 비우지 않는 요소라고 부릅니다. 이 태그는 내용을 포함할 수 없는 단일 태그 또는 열기 태그로만 구성됩니다. 이러한 요소는 일반적으로 문서에 무언가를 삽입하거나 포함시키는 데 사용됩니다.

예를 들어, 이미지 파일을 포함시킬 때 `img` 요소를 사용하거나, 페이지에 입력을 삽입할 때 `<input> 요소를 사용합니다.

```html
<img src="https://images.unsplash.com/photo-1610447847416-40bac442fbe6" width="50">
```

위의 예에서 `img` 요소는 내용이 없는 하나의 태그로만 구성됩니다. 이 요소는 문서의 [플래시 해제]에서 이미지 파일을 삽입하는 데 사용됩니다.

## HTML 요소를 중첩하는 방법

```html
<div class="my-list">
  <h4>My list:</h4>

  <ul>
     <li>Apple</li>
     <li>Orange</li>
     <li>Banana</li>
  </ul>
</div>

```

요소는 다른 요소 내부에 배치할 수 있습니다. 이것을 네스팅이라고 합니다. 위의 예에서 <div> 요소 내부에는 <h4> 요소와 <ul> 또는 무순 목록 요소가 있습니다. 그리고 <울> 요소 내부에도 마찬가지로 3개의 <li> 또는 목록 항목 요소가 있다.

기본적인 보금자리는 이해하기 매우 간단하다. 그러나 페이지가 커지면 중첩이 복잡해질 수 있습니다.

따라서 HTML로 작업하기 전에 원하는 레이아웃 구조를 생각해 보십시오. 여러분은 그것을 종이 한 장이나 마음속에 그릴 수 있습니다. 도움이 많이 될 거예요.

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-12-at-10.45.05-AM.png)

## HTML 속성이란 무엇입니까?

요소에는 내용에 나타나지 않을 요소에 대한 추가 정보가 들어 있는 특성도 있습니다.

```html
<img src="https://images.unsplash.com/photo" width="50">
```

위의 예에서 `img` 요소는 이미지의 경로를 지정하는 src 또는 원본과 이미지의 너비를 픽셀 단위로 지정하는 `width`의 두 가지 속성을 가집니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-12-at-10.45.17-AM.png)

이 예에서는 다음과 같은 특성의 특성을 확인할 수 있습니다.

- 특성과 요소 이름 사이에 공백이 있습니다.
- 특성이 시작 태그에 추가됩니다.
- 요소는 많은 속성을 가질 수 있습니다.
- 속성에는 일반적으로 이름과 값이 있습니다. name="value"

그러나 모든 속성이 같은 패턴을 가지는 것은 아닙니다. 일부는 값 없이 존재할 수 있으며, 이를 부울 속성이라고 합니다.

```html
<button onclick=“alert('Submit')" disabled>Button</button>
```

이 예에서 단추를 사용하지 않으려면 아무 값 없이 `사용 안 함` 속성만 전달하면 됩니다. 즉, 속성의 존재는 참 값을 나타내고, 그렇지 않으면 결측값이 거짓 값을 나타냅니다.

### 공통 HTML 요소

총 100개 이상의 요소가 있습니다. 하지만 90%의 경우 가장 일반적인 약 20개만 사용할 수 있습니다. 5개 그룹으로 나누었습니다.

```html
  <div>, <span>, <header>, <footer>, <nav>, <main>, <section> 

```

이러한 요소는 내용을 다른 섹션으로 구성하는 데 사용됩니다. 예를 들어, <은 소개 및 탐색 섹션의 그룹을 나타내고, <은 탐색 링크가 포함된 섹션을 나타내는 등 일반적으로 자기 설명적이다.

```html
  <h1> to <h6>, <p>, <div>, <span>, <ul>, <ol>, <li>

```

이러한 요소는 내용 또는 텍스트 블록을 구성하는 데 사용됩니다. 그것들은 접근성과 SEO에 중요하다. 브라우저에 내용의 목적이나 구조를 알려줍니다.

```html
  <form>, <input>, <button>, <label>, <textarea>

```

이러한 요소를 함께 사용하여 사용자가 작성하고 제출할 수 있는 양식을 작성할 수 있습니다. HTML에서 양식이 가장 까다로운 부분일 수 있습니다.

```html
  <img>, <a>

```

이러한 요소는 이미지를 삽입하거나 하이퍼링크를 만드는 데 사용됩니다.

```html
  <br>, <hr>

```

이러한 요소는 웹 페이지에 중단 시간을 추가하는 데 사용됩니다.

모든 요소는 developer.mozilla.org에서 확인할 수 있습니다. 하지만 초보자에게는 가장 일반적인 것만 알면 돼요.

## 블록 레벨 대 인라인 HTML 요소

기본적으로 요소는 블록 수준 또는 인라인 요소일 수 있습니다.

블록 레벨 요소는 항상 새로운 선에서 시작하여 사용 가능한 전체 너비를 차지하는 요소입니다.

인라인 요소는 새 라인에서 시작하지 않는 요소이며 필요한 만큼만 너비를 차지합니다.

![image](https://www.freecodecamp.org/news/content/images/2021/01/Screen-Shot-2021-01-11-at-1.17.22-PM.png)

블록 레벨 요소와 인라인 요소를 각각 나타내는 두 가지 요소는 <div>와 <span>이다. 이 예제에서는 ➡div 요소가 3개의 선을 사용하는 반면, ➡span 요소는 1개의 선만 차지한다는 것을 알 수 있습니다.

그러나 문제는, 어떤 요소가 블록 레벨 요소이고 어떤 요소가 인라인 요소인지 어떻게 알 수 있는가 하는 것입니다. 불행히도 당신은 그들을 기억할 필요가 있다. 가장 쉬운 방법은 인라인 요소이고 나머지는 블록 요소인 것을 기억하는 것입니다.

가장 일반적인 HTML 요소를 되돌아보면 인라인 요소에는 `<span>, `input`, `button`, `label`, `textarea`, `img`, `a`, `br` 등이 있습니다.

## HTML로 코멘트하는 방법

```html
<p>This is a paragraph.</p>

<!-- <p>I am not showing.</p> -->

```

코멘트의 목적은 코드에 노트를 포함시켜 로직을 설명하거나 코드를 구성하기 위한 것입니다.

HTML 설명은 특수 마커인 <!-> 및 -->로 싸여 있으며 브라우저에서 무시됩니다.

## HTML 엔티티 사용 방법

show 태그는 단락을 정의하지만 브라우저는 <을 새 요소에 대한 시작 태그로 해석한다는 텍스트를 표시하려면 어떻게 해야 합니까? 이 경우 다음과 같은 HTML 엔티티를 사용할 수 있습니다.

```html
<p>the <p> tag defines a paragraph.</p>

<p>the &lt;p&gt; define a paragraph.</p>

```

## HTML에서 이모지를 사용하는 방법

현대의 웹에서는 HTML로 이모지를 쉽게 표시할 수 있습니다. 👻

```html
<p>😀 Grinning Face.</p>

<p>🎂 Birthday</p>

```

## HTML의 일반적인 초기 오류

### 1. 태그/요소 이름

태그/요소 이름은 대/소문자를 구분합니다. 즉, 소문자나 대문자로 쓸 수 있지만 모든 것을 소문자로 쓰는 것이 좋습니다(<Button>이 아니라 <<button>>).

### 2.마감태그

닫는 태그를 포함하지 않는 것은 일반적인 초기 오류입니다. 따라서 열림 태그를 만들 때마다 닫힘 태그를 즉시 넣으십시오.

### 3. 보금자리

이는 잘못된 것입니다.

```html
<div>Div 1 <span> Span 2 </div></span>

```

태그는 서로 내부 또는 외부에 있는 방식으로 열고 닫아야 합니다.

### 4. 작은따옴표와 큰따옴표

이는 잘못된 것입니다.

```html
<img src="https://images.unsplash.com/'>

```

작은 따옴표와 큰 따옴표를 혼합할 수 없습니다. 항상 큰따옴표를 사용하고 필요한 경우 HTML 엔티티를 사용해야 합니다.

## HTML로 간단한 웹 사이트를 구축하는 방법

개별 HTML 요소만으로는 웹 사이트를 만들 수 없습니다. 이제 간단한 웹 사이트를 처음부터 구축하려면 무엇이 더 필요한지 알아보겠습니다.

### HTML 문서 작성 방법

먼저 Visual Studio Code(또는 좋아하는 코드 편집기)를 여십시오. 선택한 폴더에서 새 파일을 생성하고 이름을 index.html로 지정합니다.

index.html 파일에 !( 느낌표)를 입력하고 Enter 키를 누릅니다. 다음과 같은 것을 볼 수 있습니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>

```

HTML 문서가 웹 사이트를 구성하는 데 필요한 최소 코드입니다. 다음은 다음과 같습니다.

- <!DOWLPE html>: 먼저 Do-type이 있습니다. HTML에서 이상한 역사적 이유로 우리는 모든 것이 올바르게 작동하려면 doctype을 포함해야 한다.
- = en > ➡: < 요소는 루트 요소라고도 하는 페이지의 모든 내용을 래핑합니다. 그리고 페이지의 언어를 선언하기 위해 항상 lang 속성을 포함해야 한다.
- `<머리>: `<head>` 요소는 포함할 모든 것을 담는 컨테이너이지만 사용자에게 표시할 내용은 아닙니다.
- =의 문자표=UTF-8" />`: 첫 번째 메타 요소는 문자 집합을 UTF-8로 설정하는 데 사용됩니다. UTF-8은 문자 언어의 문자를 대부분 포함합니다.
- `=width name="viewport" content="width=device-width, initial-scale=1.0" />: 두 번째 메타 요소는 브라우저 뷰포트를 지정합니다. 이 설정은 모바일 최적화 사이트용입니다.
- `<title> 문서</title>: 이것이 `제목` 요소이다. 페이지 제목을 설정합니다.
- `<body>: `본문` 요소는 페이지의 모든 내용을 포함합니다.

### 팬케이크 만드는 법 페이지

좋아, 이제 시작 코드가 생겼으니 팬케이크 레시피 페이지를 만들어보자. 우리는 이 All Recipes 페이지의 콘텐츠를 사용할 것입니다.

먼저 팬케이크 레시피의 `제목` 요소 내용을 알려드리겠습니다. 웹 페이지 탭의 텍스트가 변경됩니다. <body> 요소에서, 3개의 영역을 대표하는 <header><main>과 <footer>의 3가지 요소를 만들어 보자.

헤더에는 로고와 네비게이션이 필요합니다. 따라서 로고 전용의 `ALL RECIPE`라는 콘텐츠로 div를 만들어보자.

탐색에 `nav` 요소를 사용해 보겠습니다. <nav> 요소 내에서 <ul>을 사용하여 정렬되지 않은 목록을 만들 수 있습니다. 3개의 링크에 대해 3개의 `<li> 요소를 갖기를 원합니다. 재료, 단계 및 구독. 헤더 코드는 다음과 같습니다.

```html
...
    <header>
      <div>ALL RECIPE</div>
      <nav>
        <ul>
          <li><a href="#ingredients">Ingredients</a></li>
          <li><a href="#steps">Steps</a></li>
          <li><a href="#subsribe">Subscribe</a></li>
        </ul>
      </nav>
    </header>
...

```

메인 부분에서는 우선 제목과 이미지를 가지고 싶습니다. 제목에는 h1을, 이미지에는 img를 사용할 수 있습니다(무료로 Unsplash의 이미지를 사용할 수 있습니다).

```html
...
    <main>
      <h1>Good Old Fashioned Pancakes</h1>
      <img
        src="https://images.unsplash.com/photo-1575853121743-60c24f0a7502"
        alt="pancake"
        width="250"
      />
    </main>
...

```

다음으로, 우리는 모든 재료를 나열하고 싶습니다. 순서 목록을 작성하기 위해 =를 사용하고 확인란을 작성하기 위해 = 입력 유형 = "filength" / >를 사용할 수 있습니다.

그러나 그 전에 <h2>를 사용하여 새로운 컨텐츠 블록을 시작할 수 있습니다. 또한 id 속성을 추가하여 내비게이션의 링크가 어디로 가야 하는지 알 수 있도록 합니다.

```html
...
    <main>
    ...
      <h2 id="ingredients">Ingredients</h2>
      <ol>
        <li><input type="checkbox" /> 1 ½ cups all-purpose flour</li>
        <li><input type="checkbox" /> 3 ½ teaspoons baking powder</li>
        <li><input type="checkbox" /> 1 teaspoon salt</li>
        <li><input type="checkbox" /> 1 tablespoon white sugar</li>
        <li><input type="checkbox" /> 1 ¼ cups milk</li>
        <li><input type="checkbox" /> 1 egg</li>
      </ol>
    </main>
...

```

재료가 끝나면 모든 단계를 나열하고 싶습니다. 단계 제목에는 【h4】를, 단계 내용에는 【p】를 사용할 수 있다.

```html
...
    <main>
    ...
      <h2 id="steps">Steps</h2>
      
      <h4>Step 1</h4>
      <p>
        In a large bowl, sift together the flour, baking powder, salt and sugar.
        Make a well in the center and pour in the milk, egg and melted butter;
        mix until smooth.
      </p>
      
      <h4>Step 2</h4>
      <p>
        Heat a lightly oiled griddle or frying pan over medium-high heat. Pour
        or scoop the batter onto the griddle, using approximately 1/4 cup for
        each pancake. Brown on both sides and serve hot.
      </p>
    </main>
...

```

네, 이제 메인 섹션이 끝났으니 바닥글 섹션으로 넘어갑시다.

바닥글에는 구독 양식과 저작권 텍스트가 있습니다.

구독 양식에는 <form> 요소를 사용할 수 있습니다. 그 안에 텍스트 입력에는 = 입력형="텍스트"를, 제출 버튼에는 =버튼을 넣을 수 있다.

저작권 텍스트의 경우 간단히 `<div>를 사용할 수 있습니다. 여기서 우리는 HTML 엔티티 `$copy;`를 저작권 기호에 사용할 수 있습니다.

"<br>"을 추가하여 구독 양식과 저작권 텍스트 사이에 공간을 추가할 수 있습니다.

```html
...
    <footer>
      <h6 id="subscribe">Subscribe</h6>
      <form onsubmit="alert('Subscribed')">
        <input type="text" placeholder="Enter Email Address" />
        <button>Submit</button>
      </form>
      <br />
      <div>&copy; dakota kelly at Allrecipe.com</div>
    </footer>
...

```

자, 이제 끝났습니다! 다음은 참조할 수 있는 전체 코드입니다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Pancake Recipe</title>
  </head>
  <body>
    <header>
      <div>ALL RECIPE</div>
      <nav>
        <ul>
          <li><a href="#ingredients">Ingredients</a></li>
          <li><a href="#steps">Steps</a></li>
          <li><a href="#subsribe">Subscribe</a></li>
        </ul>
      </nav>
    </header>
    <main>
      <h1>Good Old Fashioned Pancakes</h1>
      <img
        src="https://images.unsplash.com/photo-1575853121743-60c24f0a7502?ixid=MXwxMjA3fDB8MHxzZWFyY2h8MXx8cGFuY2FrZXxlbnwwfHwwfA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=700&q=60"
        alt="pancake"
        width="250"
      />
      <h2 id="ingredients">Ingredients</h2>
      <ol>
        <li><input type="checkbox" /> 1 ½ cups all-purpose flour</li>
        <li><input type="checkbox" /> 3 ½ teaspoons baking powder</li>
        <li><input type="checkbox" /> 1 teaspoon salt</li>
        <li><input type="checkbox" /> 1 tablespoon white sugar</li>
        <li><input type="checkbox" /> 1 ¼ cups milk</li>
        <li><input type="checkbox" /> 1 egg</li>
      </ol>
      <h2 id="steps">Steps</h2>
      <h4>Step 1</h4>
      <p>
        In a large bowl, sift together the flour, baking powder, salt and sugar.
        Make a well in the center and pour in the milk, egg and melted butter;
        mix until smooth.
      </p>
      <h4>Step 2</h4>
      <p>
        Heat a lightly oiled griddle or frying pan over medium-high heat. Pour
        or scoop the batter onto the griddle, using approximately 1/4 cup for
        each pancake. Brown on both sides and serve hot.
      </p>
    </main>
    <hr />
    <footer>
      <h6 id="subscribe">Subscribe</h6>
      <form onsubmit="alert('Subscribed')">
        <input type="text" placeholder="Enter Email Address" />
        <button>Submit</button>
      </form>
      <br />
      <div>&copy; dakota kelly at Allrecipe.com</div>
    </footer>
  </body>
</html>

```

## 결론

HTML만 있으면 간단한 웹사이트를 만들 수 있지만, 아름답고 기능적인 웹사이트를 만들기 위해서는 CSS와 JavaScript를 공부해야 한다.

소셜 미디어나 유튜브에서 저를 팔로우하여 향후 이 주제에 대한 최신 정보를 얻으실 수 있습니다. 그러나 한편, 당신은 무료 Code Camp Curriculum을 체크하여 작은 작업을 해결함으로써 HTML을 연습할 수 있습니다.

그렇지 않으면 행복한 코딩 상태를 유지하고 향후 게시물 👋에서 뵙겠습니다.

________ 🐣 나에 대해____________________________________

- 저는 Dev Challenges의 설립자입니다.
- 내 채널 구독
- 내 트위터 팔로우
- 불협화음 참여