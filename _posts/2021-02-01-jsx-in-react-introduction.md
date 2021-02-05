---
layout: post
title: "React의 JSX – 예제로 설명
 "
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/jsx.jpeg
tags: undefined
---


JSX는 React의 핵심 개념 중 하나입니다.
 따라서 잘 이해하면 더 나은 React 코드를 작성할 수 있습니다.
 

이 기사에서는 다음 내용을 살펴 봅니다.
 

- React에서 JSX는 무엇이며 어떻게 사용합니까?
 
- JSX가`React.createElement`로 변환되는 방법
 
- JSX 표현식이란 무엇이며 그 안에 쓸 수있는 것
 
- JSX의 일반적인 문제
 

그리고 훨씬 더.
 그럼 시작하겠습니다.
 

## JSX 란?
 

> JSX는 React에서 HTML과 JavaScript를 함께 쉽게 작성하는 데 사용되는 JavaScript Extension Syntax입니다.
 

아래 코드를 살펴보십시오.
 

```undefined
const jsx = <h1>This is JSX</h1>
```

이것은 React의 간단한 JSX 코드입니다.
 그러나 브라우저는이 JSX가 유효한 JavaScript 코드가 아니기 때문에 이해하지 못합니다.
 이는 문자열이 아니라 HTML 코드 만있는 변수에 HTML 태그를 할당하기 때문입니다.
 

따라서 브라우저에서 이해할 수있는 JavaScript 코드로 변환하기 위해 JavaScript 컴파일러 / 트랜스 파일러 인 Babel과 같은 도구를 사용합니다.
 

이 기사에서 보여준 것처럼 Webpack을 사용하여 자신의 바벨 구성을 설정할 수 있습니다.
 또는 JSX에서 JavaScript 로의 변환을 위해 내부적으로 Babel을 사용하는 create-react-app을 사용할 수 있습니다.
 

React 코드에서 위의 JSX를 다음과 같이 사용할 수 있습니다.
 

```undefined
class JSXDemo extends React.Component {
    render() {
        return <h1>This is JSX</h1>;
    }
}

ReactDOM.render(<JSXDemo />, document.getElementById('root'));
```

여기서는`JSXDemo` 컴포넌트에서 JSX를 반환하고`ReactDOM.render` 메소드를 사용하여 화면에 렌더링합니다.
 

다음은 코드 샌드 박스 데모입니다.
 

Babel이 위의 JSX를 실행할 때 다음 코드로 변환합니다.
 

```undefined
class JSXDemo extends React.Component {
    render() {
        return React.createElement("h1", null, "This is JSX");
    }
}
```

다음은 코드 샌드 박스 데모입니다.
 

위의 코드 샌드 박스에서 볼 수 있듯이 코드는 여전히`React.createElement`를 사용하여 콘텐츠를 화면에 올바르게 인쇄합니다.
 

이것은 React에서 코드를 작성하는 예전 방식 이었지만, 단순한 div를 추가하는 경우에도 매번`React.createElement`를 작성하는 것은 지루합니다.
 

그래서 React는 코드를 작성하고 이해하기 쉽게 만드는 JSX 코드 작성 방식을 도입했습니다.
 

> JSX를`React.createElement`로 변환하는 방법을 아는 것은 React 개발자로서 매우 중요합니다 (인기있는 인터뷰 질문이기도합니다).
 

## React.createElement 함수는 무엇입니까?
 

모든 JSX는 브라우저가 이해하는`React.createElement` 함수 호출로 변환됩니다.
 

`React.createElement`에는 다음 구문이 있습니다.
 

```undefined
React.createElement(type, [props], [...children])
```

`createElement` 함수의 매개 변수를 살펴 보겠습니다.
 

- type은 h1, div와 같은 HTML 태그이거나 React 컴포넌트 일 수 있습니다.
 
- props는 요소가 갖기를 원하는 속성입니다.
 
- 하위에는 다른 HTML 태그가 포함되어 있거나
 

`React.createElement` 호출도 다음과 같이 객체 표현으로 변환됩니다.
 

```undefined
{   
 type: 'h1',   
 props: {     
   children: 'This is JSX'   
 }
}

```

JSX를 일부 지역 변수에 할당하고 아래와 같이 기록하면이 객체 표현을 볼 수 있습니다.
 

```undefined
class JSXDemo extends React.Component {
    render() {
        const jsx = <h1>This is JSX</h1>;
        console.log(jsx);
        return jsx;
    }
}

ReactDOM.render(<JSXDemo />, document.getElementById('root'));
```

다음은 코드 샌드 박스 데모입니다.
 

아래와 같이 인쇄 된 로그를 볼 수 있습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/log.png)

이제 아래 코드를 살펴보십시오.
 

```undefined
class JSXDemo extends React.Component {
  render() {
    const jsx = <h1 id="jsx">This is JSX</h1>;
    console.log(jsx);
    return jsx;
  }
}

ReactDOM.render(<JSXDemo />, document.getElementById("root"));

```

여기에서는 다음과 같이 JSX를 사용했습니다.
 

```undefined
<h1 id="jsx">This is JSX</h1>
```

따라서 React는이 JSX를 아래 코드로 변환합니다.
 

```undefined
React.createElement("h1", { id: "jsx" }, "This is JSX");
```

우리의 경우와 같이 HTML 태그에 추가 된 속성이 있으면`React.createElement` 호출의 두 번째 매개 변수로 전달됩니다.
 객체 표현은 다음과 같습니다.
 

```undefined
{ 
  type: 'h1', 
  props: { 
   id: 'jsx',
   children: 'This is JSX'
  } 
}
```

다음은 코드 샌드 박스 데모입니다.
 

아래와 같이 인쇄 된 로그를 볼 수 있습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/create_element.png)

이제 JSX에 복잡성을 추가하여`React.createElement` 호출로 어떻게 변환되는지 살펴 보겠습니다.
 

```undefined
class JSXDemo extends React.Component {
  handleOnClick = () => {
    console.log("clicked");
  };
  render() {
    return (
      <button id="btn" onClick={this.handleOnClick}>
        Click Here
      </button>
    );
  }
}

ReactDOM.render(<JSXDemo />, document.getElementById("root"));
```

여기에서 버튼에 `onClick`핸들러를 추가했습니다.
 

위 코드의 경우`React.createElement` 호출은 다음과 같습니다.
 

```undefined
React.createElement("button", {
  id: "btn", 
  onClick: function() {}
}, "Click Here")
```

다음은 코드 샌드 박스 데모입니다.
 

객체 표현은 다음과 같습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/id_children.png)

따라서 위의 모든 예제에서 JSX가`React.createElement` 호출로 변환 된 다음 객체 표현으로 변환된다는 것이 분명합니다.
 

JSX에서`React.createElement` 로의 변환 코드를 보려면이 기사에서 만든이 애플리케이션으로 이동하면됩니다.
 왼쪽에 JSX 코드를 작성하고 아래와 같이 오른쪽에 변환 된 코드를 볼 수 있습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/conversion.png)

## 복잡한 JSX를 반환하는 방법
 

아래 코드를 살펴보십시오.
 

```undefined
import React from "react";
import ReactDOM from "react-dom";

const App = () => {
  return (
      <p>This is first JSX Element!</p>
      <p>This is another JSX Element</p>
  );
};

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

다음은 코드 샌드 박스 데모입니다.
 

여기에서는 App 구성 요소에서 두 개의 단락을 반환합니다.
 그러나 코드를 실행하면 다음 오류가 발생합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/adjacent_error.png)

React는 인접한 요소를 부모 태그로 감싸 야하기 때문에 오류가 발생합니다.
 

앞에서 살펴본 것처럼`<p> 이것이 첫 번째 JSX 요소입니다! </ p>`는`React.createElement ( "p", null, "This is first JSX Element!")`및`<p>로 변환됩니다.
 이것은 또 다른 JSX 요소입니다 </ p>`는`React.createElement ( "p", null, "This is another JSX Element")`로 변환됩니다.
 

이제 변환 된 코드는 다음과 같습니다.
 

```undefined
import React from "react";
import ReactDOM from "react-dom";

const App = () => {
  return (
            React.createElement("p", null, "This is first JSX Element!"); React.createElement("p", null, "This is another JSX Element");
        );
};

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

여기서는 둘 다 래핑 할 부모 요소가 없기 때문에 작동하지 않는`App` 구성 요소에서 두 가지를 반환합니다.
 

작동하도록하려면 분명한 해결책은 둘 다 부모 요소 (대부분 다음과 같은`div`)로 래핑하는 것입니다.
 

```undefined
import React from "react";
import ReactDOM from "react-dom";

const App = () => {
  return (
    <div>
      <p>This is first JSX Element!</p>
      <p>This is another JSX Element</p>
    </div>
  );
};

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

다음은 코드 샌드 박스 데모입니다.
 

그러나 그것을 작동시키는 다른 방법도 있습니다.
 

먼저 아래와 같이 배열로 반환 해 볼 수 있습니다.
 

```undefined
import React from "react";
import ReactDOM from "react-dom";

const App = () => {
  return (
    [<p>This is first JSX Element!</p>,<p>This is another JSX Element</p>]
  );
};

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

다음은 코드 샌드 박스 데모입니다.
 

이렇게하면 작업이 완료되지만 브라우저 콘솔에서 볼 수 있듯이 `경고 : 목록의 각 하위 항목에는 고유 한 "키"소품이 있어야합니다.`라는 경고가 표시됩니다.
 

> React에서는 배열의 모든 요소 (JSX를 사용하여 표시 될 때)에 고유 키가 추가되어야하기 때문입니다.
 

인접한 요소에 고유 키를 추가하여 수정할 수 있습니다.
 

```undefined
import React from "react";
import ReactDOM from "react-dom";

const App = () => {
  return (
    [<p key="first">This is first JSX Element!</p>,<p key="second">This is another JSX Element</p>]
  );
};

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

다음은 코드 샌드 박스 데모입니다.
 

다른 방법은`React.Fragment` 구성 요소를 사용하는 것입니다.
 

```undefined
import React from "react";
import ReactDOM from "react-dom";

const App = () => {
  return (
    <React.Fragment>
      <p>This is first JSX Element!</p>
      <p>This is another JSX Element</p>
    </React.Fragment>
  );
};

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

다음은 코드 샌드 박스 데모입니다.
 

`React.Fragment`는 React 버전 16.2에 추가되었습니다. 컴포넌트가 반환하는 모든 JSX 내부의 일부 태그 (예 : div)에서 여러 인접 요소를 항상 래핑해야하기 때문입니다.
 그러나 불필요한 div 태그가 추가됩니다.
 

이것은 대부분의 경우 괜찮지 만 좋지 않은 경우가 있습니다.
 

예를 들어 Flexbox를 사용하는 경우 Flexbox의 구조에 특별한 부모-자식 관계가 있습니다.
 그리고 중간에 div를 추가하면 원하는 레이아웃을 유지하기가 어렵습니다.
 

따라서`React.Fragment`를 사용하면이 문제가 해결됩니다.
 

> 프래그먼트를 사용하면 DOM에 추가 노드를 추가하지 않고도 자식 목록을 그룹화 할 수 있습니다.
 

## JSX 코드에 주석을 추가하는 방법
 

다음과 같은 코드가있는 경우 :
 

```undefined
<p>This is some text</p>
```

해당 코드에 대한 주석을 추가하려면 다음과 같이`/ *`및`* /`주석 기호 안에 JSX 표현 구문으로 해당 코드를 래핑해야합니다.
 

```undefined
{/* <p>This is some text</p> */}
```

팁 : 주석을 수동으로 입력하는 대신`Cmd + /`(Mac) 또는`Ctrl + /`단축키를 사용하여 주석을 추가하거나 제거 할 수 있습니다.
 

## JSX에서 JavaScript 코드를 추가하는 방법
 

지금까지 JSX의 일부로 HTML 태그 만 사용했습니다.
 그러나 JSX는 실제로 JavaScript 코드를 내부에 추가 할 때 더 유용합니다.
 

JSX 내부에 JavaScript 코드를 추가하려면 다음과 같이 중괄호 안에 작성해야합니다.
 

```undefined
const App = () => {
 const number = 10;
 return (
  <div>
   <p>Number: {number}</p>
  </div>
 );
};
```

다음은 코드 샌드 박스 데모입니다.
 

> 중괄호 안에는 어떤 값으로 평가되는 표현식 만 작성할 수 있습니다.
 

따라서 종종 중괄호를 사용하는이 구문을 JSX 표현식 구문이라고합니다.
 

다음은 JSX 표현식에서 사용할 수있는 유효한 것입니다.
 

- "hello"와 같은 문자열
 
- 10과 같은 숫자
 
- [1, 2, 4, 5]와 같은 배열
 
- 어떤 값으로 평가 될 객체 속성
 
- JSX 일 수있는 일부 값을 반환하는 함수 호출
 
- 항상 새 배열을 반환하는 맵 메서드
 
- JSX 자체
 

다음은 유효하지 않은 사항이며 JSX 표현식에서 사용할 수 없습니다.
 

- for 루프, while 루프 또는 기타 루프
 
- 변수 선언
 
- 함수 선언
 
- if 조건
 
- 객체
 verified_user

`<p> {[1, 2, 3, 4]} </ p>`가 마침내`<p> {1} {2} {3} {4} </으로 변환되기 때문에 JSX 표현식에서 배열을 작성할 수 있습니다.
 p>`를 렌더링 할 때 (문제없이 렌더링 할 수 있음).
 

개체의 경우 개체가 어떻게 표시되어야하는지 명확하지 않습니다.
 예를 들어 쉼표로 구분 된 키-값 쌍이어야합니까 아니면 JSON으로 표시해야합니까?
 따라서 JSX 표현식에서 객체를 표시하려고하면 오류가 발생합니다.
 하지만 대신 객체 속성을 사용할 수 있습니다.
 

> 또한 undefined, null 및 boolean은 JSX 내에서 사용될 때 UI에 표시되지 않습니다.
 

따라서 부울 값이 있고이를 UI에 표시하려면 다음과 같이 ES6 템플릿 리터럴 구문으로 래핑해야합니다.
 

```undefined
const App = () => {
  const isAdmin = true;
  return (
    <div>
      <p>isAdmin is {`${isAdmin}`} </p>
    </div>
  );
};
```

다음은 코드 샌드 박스 데모입니다.
 

### JSX 표현식의 조건부 연산자
 

문제로 생각할 수있는 JSX 표현식에는 if 조건을 작성할 수 없습니다.
 그러나 React를 사용하면 삼항 연산자와 같은 조건 연산자와 다음과 같은 논리 단락 && 연산자를 작성할 수 있습니다.
 

```undefined
<p>{a > b ? "Greater" : "Smaller"}</p>
<p>{shouldShow && "Shown"}</p>
```

다음은 JSX 표현식을 작성하는 다양한 방법을 설명하는 코드 샌드 박스 데모입니다.
 

## JSX 표현식을 중첩하는 방법
 

다음과 같이 JSX 표현식을 중첩 할 수도 있습니다.
 

```undefined
const App = () => {
  const number = 10;
  return (
    <div>
      {number > 0 ? (
        <p>Number {number} is positive</p>
      ) : (
        <p>Number {number} is Negative</p>
      )}
    </div>
  );
};
```

다음은 코드 샌드 박스 데모입니다.
 

## JSX에서 클래스를 추가하는 방법
 

HTML에서와 같이`id` 및`class`와 같은 속성을 JSX 요소에 추가 할 수 있습니다.
 

```undefined
import React from "react";
import ReactDOM from "react-dom";

const App = () => {
  const id = "some-id";
  return (
    <div>
      <h1 id={id}>This is a heading</h1>
      <h2 className="active">This is another heading</h2>
    </div>
  );
};

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

다음은 코드 샌드 박스 데모입니다.
 

React에서는`class` 대신`className`을 사용해야합니다.
 

왜냐하면`className` 대신`class`를 사용하면 아래와 같이 콘솔에 경고가 표시되기 때문입니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/class_warning.png)

다음은 코드 샌드 박스 데모입니다.
 

경고가 표시되는 이유를 이해하려면 경고의 개체 표현을 인쇄하면 다음이 표시됩니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/class_info-1.png)

다음은 코드 샌드 박스 데모입니다.
 

보시다시피 props 객체에는 값이 `active`인 `class`속성이 있습니다.
 하지만 자바 스크립트에서`class`는 예약 된 키워드이므로`props.class`에 액세스하면 오류가 발생합니다.
 

이것이 React가`class` 대신`className`을 사용하기로 결정한 이유입니다.
 

`class` 대신`className`을 사용하는 것은 React 인터뷰에서 자주 묻는 질문입니다.
 

> React에서 모든 속성 이름은 camelCase로 작성됩니다.
 

여기에서 변경되거나 변경되지 않은 모든 속성 목록을 찾을 수 있습니다.
 

## 결론
 

이 기사에서는 React에서 JSX를 사용하는 방법을 살펴 보았습니다.
 다음은 몇 가지 주요 사항입니다.
 

- 모든 JSX 태그는`React.createElement` 호출과 해당 객체 표현으로 변환됩니다.
 
- 중괄호 안에 쓰여진 JSX 표현식은 문자열, 숫자, 배열 맵 메소드 등과 같은 값으로 평가되는 것만 허용합니다.
 
- React에서는 HTML 요소에 클래스를 추가하기 위해 `class`대신 `className`을 사용해야합니다.
 
- React의 모든 속성 이름은 camelCase로 작성됩니다.
 
- `undefined`,`null` 및`boolean`은 JSX 내에서 사용될 때 UI에 표시되지 않습니다.
 

### 읽어 주셔서 감사합니다!
 verified_user

무료 React Router 소개 과정을 확인하십시오.
 

또한 Mastering Modern JavaScript 책을 확인하여 JavaScript 및 React에서 더 나은 사람이되기 위해 모든 최신 ES6 + 기능을 자세히 배우십시오.
 

내 주간 뉴스 레터를 구독하여 1000 명 이상의 다른 구독자와 함께 놀라운 팁, 요령, 기사 및 할인 거래를받은 편지함에서 직접 받아보세요.
 