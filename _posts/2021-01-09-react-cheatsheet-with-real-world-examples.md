---
layout: post
title: "2021년 대응 부정 행위 시트(+실제 사례)"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/the-react-cheatsheet-for-2021-1.png
tags: undefined
---


리액트 라이브러리의 모든 주요 개념과 기능을 2021년에 마스터할 수 있도록 포괄적인 시각적 부정 행위 시트를 작성했습니다.

저는 여러분이 반응 학습을 최단 시간 내에 최적화할 수 있도록 돕기 위해 이 치트 시트를 만들었습니다.

여기에는 라이브러리에 대한 모든 기능과 프로젝트의 적용 패턴을 사용하여 라이브러리의 작동 방식을 설명하는 수많은 실제 예가 포함되어 있습니다.

각각의 코드 조각과 함께, 나는 많은 유용한 코멘트를 추가했다. 이러한 설명을 읽으면 각 코드 행이 무엇을 하는지, 서로 다른 개념들이 어떻게 관련되어 있는지, 그리고 리액션을 어떻게 사용할 수 있는지 더 완벽하게 이해할 수 있습니다.

반응 개발자로서 특히 유용한 키워드는 굵게 강조되어 있으므로 이러한 키워드를 주의 깊게 살펴보십시오.

### 당신만의 치트시트를 원하십니까?‬

여기에서 PDF 형식의 치트 시트를 다운로드하십시오(5초 소요).

다음은 다운로드 가능한 버전을 통해 얻을 수 있는 몇 가지 빠른 이점입니다.

- ■ 언제 어디서나 검토하기 위한 빠른 참조 가이드
- ■ 쉽게 재사용할 수 있는 수많은 복사 가능한 코드 조각
- ■ 가장 적합한 가이드를 읽어 보십시오. 기차에서, 책상에, 줄 서 있는... 아무데나

다뤄야 할 멋진 일들이 많으니까, 시작해보도록 하죠.

> 아래의 코드 조각 중 하나를 실행하시겠습니까? 새로운 대응 응용프로그램을 만들어 (무료) 온라인 도구 CodeSandbox를 사용하여 이러한 예제를 사용해 보십시오. act.new를 방문하면 즉시 그렇게 할 수 있다.

## 목차.

### 기본 사항 대응

- JSX 요소
- 구성 요소 및 소품
- 목록 및 키
- 이벤트 수신기 및 이벤트 처리

### 에센셜 리액트 후크

- 상태 및 사용 상태
- 부작용 및 사용 효과
- 참조 및 사용 참조

### 후크 및 성능

- 리렌더 및 리액션.메모 방지
- 콜백 기능 및 콜백 사용
- 메모화 및 메모 사용

### 고급 반응 후크

- 컨텍스트 및 사용 컨텍스트
- 리듀서 및 사용 리듀서
- 사용자 지정 후크 쓰기
- 후크 규칙

## 기본 사항 대응

### JSX 요소

반응 애플리케이션은 JSX라는 구문을 사용하여 구조화됩니다. 기본 JSX 요소의 구문입니다.

```undefined
/* 
  JSX allows us to write in a syntax almost identical to plain HTML.
  As a result, JSX is a powerful tool to structure our applications.
  JSX uses all valid HTML tags (i.e. div/span, h1-h6, form/input, img, etc).
*/

<div>Hello React!</div>

/* 
  Note: this JSX would not be visible because it needs to be rendered by our application using ReactDOM.render() 
*/
```

JSX는 React 애플리케이션을 구조화하는 가장 일반적인 방법이지만 React에는 필요하지 않습니다.

```undefined
/* JSX is a simpler way to use the function React.createElement()
In other words, the following two lines in React are the same: */

<div>Hello React!</div>  // JSX syntax

React.createElement('div', null, 'Hello React!'); // createElement syntax
```

JSX가 브라우저에서 이해되지 않습니다. 브라우저가 이해할 수 있는 일반 자바스크립트로 컴파일해야 한다.

JSX에서 가장 일반적으로 사용되는 컴파일러는 Babel이라고 불린다.

```undefined
/* 
  When our project is built to run in the browser, our JSX will be converted by Babel into simple React.createElement() function calls. 
  From this... 
*/
const greeting = <div>Hello React!</div>;

/* ...into this: */
"use strict";

const greeting = /*#__PURE__*/React.createElement("div", null, "Hello React!");
```

JSX는 몇 가지 중요한 면에서 HTML과 다르다.

```undefined
/* 
  We can write JSX like plain HTML, but it's actually made using JavaScript functions.
  Because JSX is JavaScript, not HTML, there are some differences:

  1) Some JSX attributes are named differently than HTML attributes. Why? Because some attribute words are reserved words in JavaScript, such as 'class'. Instead of class, JSX uses 'className'.

  Also, because JSX is JavaScript, attributes that consist of multiple words are written in camelcase:
*/

<div id="header">
  <h1 className="title">Hello React!</h1>
</div>

/* 
  2) JSX elements that consist of only a single tag (i.e. input, img, br elements) must be closed with a trailing forward slash to be valid (/): 
*/

<input type="email" /> // <input type="email"> is a syntax error

/* 
  3) JSX elements that consist of an opening and closing tag (i.e. div, span, button element), must have both or be closed with a trailing forward slash. Like 2), it is a syntax error to have an unterminated element. 
*/

<button>Click me</button> // <button> or </button> is a syntax error
<button /> // empty, but also valid
```

스타일 속성을 사용하여 JSX 요소에 인라인 스타일을 추가할 수 있습니다. HTML과 같이 큰따옴표의 집합이 아닌 객체 내에서 스타일이 업데이트됩니다.

스타일 속성 이름은 낙타 케이스에도 입력해야 합니다.

```undefined
/* 
  Properties that accept pixel values (like width, height, padding, margin, etc), can use integers instead of strings.
  For example: fontSize: 22. Instead of: fontSize: "22px"
*/
<h1 style={ color: 'blue', fontSize: 22, padding: '0.5em 1em' }>
  Hello React!
</h1>
```

JSX 요소는 JavaScript 식이며 이와 같이 사용할 수 있습니다. JSX는 사용자 인터페이스 내에서 직접 JavaScript의 모든 기능을 제공합니다.

```undefined
/* 
  JSX elements are expressions (resolve to a value) and therefore can be assigned to plain JavaScript variables... 
*/
const greeting = <div>Hello React!</div>;

const isNewToReact = true;

// ... or can be displayed conditionally
function sayGreeting() {
  if (isNewToReact) {
    // ... or returned from functions, etc.
    return greeting; // displays: Hello React!
  } else {
    return <div>Hi again, React</div>;
  }
}
```

JSX를 사용하면 다음과 같은 곱슬 브레이스 구문을 사용하여 간단한 JavaScript 식을 삽입(또는 포함)할 수 있습니다.

```undefined
const year = 2021;

/* We can insert primitive JS values (i.e. strings, numbers, booleans) in curly braces: {} */
const greeting = <div>Hello React in {year}</div>;

/* We can also insert expressions that resolve to a primitive value: */
const goodbye = <div>Goodbye previous year: {year - 1}</div>

/* Expressions can also be used for element attributes */
const className = 'title';
const title = <h1 className={className}>My title</h1>

/* Note: trying to insert object values (i.e. objects, arrays, maps) in curly braces will result in an error */
```

JSX는 HTML과 같은 요소들을 서로 중첩시킬 수 있게 해준다.

```undefined
/* 
  To write JSX on multiple lines, wrap in parentheses: ()
  JSX expressions that span multiple lines are called multiline expressions
*/

const greeting = (
  // div is the parent element
  <div>
    {/* h1 and p are child elements */}
    <h1>Hello!</h1>
    <p>Welcome to React</p>
  </div>
);
/* 'parents' and 'children' are how we describe JSX elements in relation
to one another, like we would talk about HTML elements */
```

JSX의 코멘트는 다음과 같이 곱슬곱슬한 브레이스 사이에 쓰여지는 다중 라인 JavaScript 코멘트로 작성된다.

```undefined
const greeting = (
  <div>
    {/* This is a single line comment */}
   <h1>Hello!</div>
 <p>Welcome to React</p>
    {/* This is a 
      multiline
      comment */} 
  </div>
);
```

All React 앱에는 다음 세 가지가 필요합니다.

- ReactDOM.render(): 앱을 HTML 요소에 마운트하여 렌더링(표시)하는 데 사용됩니다.
- JSX 요소: 애플리케이션의 루트이기 때문에 "루트 노드"라고 합니다. 즉, 렌더링하면 모든 하위 항목이 렌더링됩니다.
- HTML(DOM) 요소: HTML 페이지 내에 앱이 삽입되는 위치. 요소는 일반적으로 root의 ID를 가진 div이며 index.html 파일에 위치한다.

```undefined
// Packages can be installed locally or brought in through a CDN link (added to head of HTML document) 
import React from "react";
import ReactDOM from "react-dom";

// root node (usually a component) is most often called "App"
const App = <h1>Hello React!</h1>;

// ReactDOM.render(root node, HTML element)
ReactDOM.render(App, document.getElementById("root"));
```

### 구성 요소 및 소품

JSX는 컴포넌트라고 불리는 개별 함수 내에서 함께 그룹화될 수 있다.

반응에는 기능 구성 요소와 클래스 구성 요소의 두 가지 유형이 있습니다.

함수 또는 클래스 구성 요소의 구성 요소 이름은 JSX를 반환하지 않는 일반 JavaScript 기능과 구별하기 위해 대문자로 지정됩니다.

```undefined
import React from "react";

/*  
  Function component
  Note the capitalized function name: 'Header', not 'header'
*/
function Header() {
  return <h1>Hello React</h1>;
}

// Function components which use an arrow function syntax are also valid
const Header = () => <h1>Hello React</h1>;

/* 
  Class component
  Class components have more boilerplate (note the 'extends' keyword and 'render' method)
*/
class Header extends React.Component {
  render() {
    return <h1>Hello React</h1>;
  }
}
```

기능임에도 불구하고 컴포넌트는 일반적인 자바스크립트 함수처럼 불리지 않는다. 그들은 우리의 앱에서 JSX처럼 그들을 렌더링함으로써 실행된다.

```undefined
// Do we call this function component like a normal function?

// No, to execute them and display the JSX they return...
const Header = () => <h1>Hello React</h1>;

// ...we use them as 'custom' JSX elements
ReactDOM.render(<Header />, document.getElementById("root"));
// renders: <h1>Hello React</h1>
```

구성요소의 큰 이점은 필요할 때마다 응용프로그램 전반에 걸쳐 재사용할 수 있다는 점입니다.

구성 요소는 JavaScript 함수의 힘을 활용하므로, 우리는 하나 이상의 인수를 전달하여 논리적으로 데이터를 전달할 수 있다.

```undefined
/* 
  The Header and Footer components can be reused in any page in our app.
  Components remove the need to rewrite the same JSX multiple times.
*/

// IndexPage component, visible on '/' route of our app
function IndexPage() {
  return (
    <div>
      <Header />
      <Hero />
      <Footer />
    </div>
  );
}

// AboutPage component, visible on the '/about' route
function AboutPage() {
  return (
    <div>
      <Header />
      <About />
      <Testimonials />
      <Footer />
    </div>
  );
}
```

자바스크립트에서 구성요소에 전달된 데이터를 소품이라고 한다. 소품은 일반 JSX/HTML 요소의 속성과 동일해 보이지만 구성 요소 자체 내에서 해당 값에 액세스할 수 있습니다.

소품은 전달되는 구성 요소의 매개 변수에서 사용할 수 있습니다. 소품은 항상 개체의 속성으로 포함됩니다.

```undefined
/* 
  What if we want to pass custom data to our component from a parent component?
  For example, to display the user's name in our app header.
*/

const username = "John";

/* 
  To do so, we add custom 'attributes' to our component called props.
  We can add many of them as we like and we give them names that suit the data we pass in.
  To pass the user's name to the header, we use a prop we appropriately called 'username'
*/
ReactDOM.render(
  <Header username={username} />,
  document.getElementById("root")
);
// We called this prop 'username', but can use any valid identifier we would give, for example, a JavaScript variable

// props is the object that every component receives as an argument
function Header(props) {
  // the props we make on the component (username)
  // become properties on the props object
  return <h1>Hello {props.username}</h1>;
}
```

어린이 구성 요소 내에서 소품을 직접 교체해서는 안 됩니다.

또 다른 방법은 소품은 자바스크립트 객체이기 때문에 소품은 변이되어서는 안 된다는 것이다.

```undefined
/* 
  Components should operate as 'pure' functions.
  That is, for every input, we should be able to expect the same output.
  This means we cannot mutate the props object, only read from it.
*/

// We cannot modify the props object :
function Header(props) {
  props.username = "Doug";

  return <h1>Hello {props.username}</h1>;
}
/* 
  But what if we want to modify a prop value that is passed to our component?
  That's where we would use state (see the useState section).
*/
```

소품/구성 요소를 다른 구성 요소에 소품으로 전달하려는 경우 어린이 소품이 유용합니다.

```undefined
// Can we accept React elements (or components) as props?
// Yes, through a special property on the props object called 'children'

function Layout(props) {
  return <div className="container">{props.children}</div>;
}

// The children prop is very useful for when you want the same
// component (such as a Layout component) to wrap all other components:
function IndexPage() {
  return (
    <Layout>
      <Header />
      <Hero />
      <Footer />
    </Layout>
  );
}

// different page, but uses same Layout component (thanks to children prop)
function AboutPage() {
  return (
    <Layout>
      <About />
      <Footer />
    </Layout>
  );
}
```

다시 말하지만 구성 요소는 JavaScript 식이므로 if-else 문 및 스위치 문과 함께 사용하여 다음과 같은 내용을 조건부로 표시할 수 있습니다.

```undefined
function Header() {
  const isAuthenticated = checkAuth();
    
  /* if user is authenticated, show the authenticated app, otherwise, the unauthenticated app */
  if (isAuthenticated) {
    return <AuthenticatedApp />   
  } else {
    /* alternatively, we can drop the else section and provide a simple return, and the conditional will operate in the same way */
    return <UnAuthenticatedApp />   
  }
}
```

구성 요소의 반환된 JSX 내의 조건을 사용하려면 단측 연산자 또는 단락(단선)을 사용할 수 있습니다.

```undefined
function Header() {
  const isAuthenticated = checkAuth();

  return (
    <nav>
      {/* if isAuth is true, show nothing. If false, show Logo  */}
      {isAuthenticated || <Logo />}
      {/* if isAuth is true, show AuthenticatedApp. If false, show Login  */}
      {isAuthenticated ? <AuthenticatedApp /> : <LoginScreen />}
      {/* if isAuth is true, show Footer. If false, show nothing */}
      {isAuthenticated && <Footer />}
    </nav>
  );
}
```

조각은 DOM에 추가 요소를 추가하지 않고 여러 구성 요소를 표시하기 위한 특수 구성 요소입니다. 이들은 인접한 여러 요소 또는 요소를 포함하는 조건부 논리에 이상적입니다.

```undefined
/*
  We can improve the logic in the previous example.
  If isAuthenticated is true, how do we display both the AuthenticatedApp and Footer components?
*/
function Header() {
  const isAuthenticated = checkAuth();

  return (
    <nav>
      <Logo />
      {/* 
        We can render both components with a fragment. 
        Fragments are very concise: <> </>
      */}
      {isAuthenticated ? (
        <>
          <AuthenticatedApp />
          <Footer />
        </>
      ) : (
        <Login />
      )}
    </nav>
  );
}
/* 
  Note: An alternate syntax for fragments is React.Fragment:
  <React.Fragment>
     <AuthenticatedApp />
     <Footer />
  </React.Fragment>
*/
```

### 목록 및 키

.map() 함수를 사용하여 데이터(레이) 목록을 요소 목록으로 변환합니다.

```undefined
const people = ["John", "Bob", "Fred"];
const peopleList = people.map(person => <p>{person}</p>);

```

.map()은 구성 요소뿐만 아니라 일반 JSX 요소에도 사용할 수 있습니다.

```undefined
function App() {
  const people = ['John', 'Bob', 'Fred'];
  // can interpolate returned list of elements in {}
  return (
    <ul>
      {/* we're passing each array element as props to Person */}
      {people.map(person => <Person name={person} />}
    </ul>
  );
}

function Person({ name }) {
  // we access the 'name' prop directly using object destructuring
  return <p>This person's name is: {name}</p>;
}
```

요소 목록 내의 각 반응 요소에는 특수 키 소자가 필요합니다. 리액션이 `.map() 함수로 반복되고 있는 각 요소를 추적하기 위해서는 키가 필수적이다.

React는 전체 목록을 다시 렌더링하는 대신 키를 사용하여 데이터가 변경될 때 개별 요소를 업데이트합니다.

키에는 고유한 값이 있어야 키 값에 따라 각 값을 식별할 수 있습니다.

```undefined
function App() {
  const people = [
    { id: 'Ksy7py', name: 'John' },
    { id: '6eAdl9', name: 'Bob' },
    { id: '6eAdl9', name: 'Fred' },
  ];

  return (
    <ul>
      {/* keys need to be primitive values, ideally a unique string, such as an id */}
      {people.map(person =>
         <Person key={person.id} name={person.name} />
      )}
    </ul>
  );
}

// If you don't have some ids with your set of data that are unique // and primitive values, use the second parameter of .map() to get each // elements index

function App() {
  const people = ['John', 'Bob', 'Fred'];

  return (
    <ul>
      {/* use array element index for key */}
      {people.map((person, i) => <Person key={i} name={person} />)}
    </ul>
  );
}
```

### 이벤트 수신기 및 이벤트 처리

JSX 요소에 대한 이벤트 청취와 HTML 요소에 대한 청취는 몇 가지 중요한 면에서 다르다.

첫째, 반응 구성 요소에서만 이벤트를 청취할 수 없습니다. 예를 들어, React 구성 요소에 `onClick`이라는 소품을 추가하는 것은 소품 개체에 추가된 다른 속성일 뿐입니다.

```undefined
/* 
  The convention for most event handler functions is to prefix them with the word 'handle' and then the action they perform (i.e. handleToggleTheme)
*/
function handleToggleTheme() {
  // code to toggle app theme
}

/* In HTML, onclick is all lowercase, plus the event handler includes a set of parentheses after being referenced */
<button onclick="handleToggleTheme()">
  Toggle Theme
</button>

/* 
  In JSX, onClick is camelcase, like attributes / props.
  We also pass a reference to the function with curly braces.
*/
<button onClick={handleToggleTheme}>
  Toggle Theme
</button>
```

알아야 할 가장 중요한 리액트 이벤트는 온클릭, 온체인지, 온서밋이다.

- `onClick(클릭)`은 JSX 요소의 클릭 이벤트(버튼의 이름)를 처리합니다.
- `변경 시`는 키보드 이벤트(입력 또는 텍스트 영역에 입력하는 사용자)를 처리합니다.
- `제출 시`는 사용자의 양식 제출을 처리합니다.

```undefined
function App() {
  function handleInputChange(event) {
    /* When passing the function to an event handler, like onChange we get access to data about the event (an object) */
    const inputText = event.target.value; // text typed into the input
    const inputName = event.target.name; // 'email' from name attribute
  }

  function handleClick(event) {
    /* onClick doesn't usually need event data, but it receives event data as well that we can use */
    console.log('clicked!');
    const eventType = event.type; // "click"
    const eventTarget = event.target; // <button>Submit</button>
  }
    
  function handleSubmit(event) {
    /* 
     When we hit the return button, the form will be submitted, as well as when a button with type="submit" is clicked.
     We call event.preventDefault() to prevent the default form behavior from taking place, which is to send an HTTP request and reload the page.
    */
    event.preventDefault();
    const formElements = event.target.elements; // access all element within form
    const inputValue = event.target.elements.emailAddress.value; // access the value of the input element with the id "emailAddress"
  }

  return (
    <form onSubmit={handleSubmit}>
      <input id="emailAddress" type="email" name="email" onChange={handleInputChange} />
      <button onClick={handleClick}>Submit</button>
    </form>
  );
}

```

## 에센셜 리액트 후크

### 상태 및 사용 상태

useState 후크는 함수 구성요소의 상태를 제공한다. State를 사용하면 시간이 지남에 따라 구성요소의 특정 값에 액세스하고 업데이트할 수 있습니다.

로컬 구성요소 상태는 상태 변수를 제공하는 Reacthook `useState`에 의해 관리되며 이를 업데이트할 수 있는 함수를 제공합니다.

우리가 useState라고 부를 때 useState라고 부를 때 우리는 useState를 첫번째 주장으로 제공함으로써 우리의 state에 디폴트 값을 부여할 수 있다.

```undefined
import React from 'react';

/* 
  How do you create a state variable?
  Syntax: const [stateVariable] = React.useState(defaultValue);
*/
function App() {
  const [language] = React.useState('JavaScript');
  /* 
    We use array destructuring to declare state variable.
    Like any variable, we declare we can name it what we like (in this case, 'language').
  */

  return <div>I am learning {language}</div>;
}
```

참고: 이 섹션의 후크는 React core 라이브러리에서 가져온 것이며 개별적으로 가져올 수 있습니다.

```undefined
import React, { useState } from "react";

function App() {
  const [language] = useState("javascript");

  return <div>I am learning {language}</div>;
}
```

또한 `useState`는 생성 후 상태를 업데이트하는 `setter` 기능을 제공합니다.

```undefined
function App() {
  /* 
   The setter function is always the second destructured value.
   The naming convention for the setter function is to be prefixed with 'set'.
  */
  const [language, setLanguage] = React.useState("javascript");

  return (
    <div>
      <button onClick={() => setLanguage("python")}>
        Learn Python
      </button>
      {/*  
        Why use an inline arrow function here instead of immediately calling it like so: onClick={setterFn()}? 
        If so, setLanguage would be called immediately and not when the button was clicked by the user.
        */}
      <p>I am now learning {language}</p>
    </div>
  );
}

/* 
 Note: whenever the setter function is called, the state updates,
 and the App component re-renders to display the new state.
 Whenever state is updated, the component will be re-rendered
*/
```

useState는 단일 구성 요소 내에서 한 번 또는 여러 번 사용할 수 있습니다. 그리고 그것은 상태를 관리하기 위해 원시적 또는 객체적 가치를 받아들일 수 있다.

```undefined
function App() {
  const [language, setLanguage] = React.useState("python");
  const [yearsExperience, setYearsExperience] = React.useState(0);

  return (
    <div>
      <button onClick={() => setLanguage("javascript")}>
        Change language to JS
      </button>
      <input
        type="number"
        value={yearsExperience}
        onChange={event => setYearsExperience(event.target.value)}
      />
      <p>I am now learning {language}</p>
      <p>I have {yearsExperience} years of experience</p>
    </div>
  );
}
```

새 상태가 이전 상태에 따라 달라지는 경우 업데이트가 안정적으로 수행되도록 하기 위해 정확한 이전 상태를 제공하는 세터 함수 내에서 함수를 사용할 수 있습니다.

```undefined
/* We have the option to organize state using whatever is the most appropriate data type, according to the data we're managing */
function App() {
  const [developer, setDeveloper] = React.useState({
    language: "",
    yearsExperience: 0
  });

  function handleChangeYearsExperience(event) {
    const years = event.target.value;
    /* We must pass in the previous state object we had with the spread operator to spread out all of its properties */
    setDeveloper({ ...developer, yearsExperience: years });
  }

  return (
    <div>
      {/* No need to get previous state here; we are replacing the entire object */}
      <button
        onClick={() =>
          setDeveloper({
            language: "javascript",
            yearsExperience: 0
          })
        }
      >
        Change language to JS
      </button>
      {/* We can also pass a reference to the function */}
      <input
        type="number"
        value={developer.yearsExperience}
        onChange={handleChangeYearsExperience}
      />
      <p>I am now learning {developer.language}</p>
      <p>I have {developer.yearsExperience} years of experience</p>
    </div>
  );
}
```

여러 원시 값을 관리하는 경우 useState를 여러 번 사용하는 것이 개체와 함께 한 번 사용하는 것보다 더 좋은 경우가 많습니다. 옛 주와 새 주를 결합하는 것을 잊지 않아도 됩니다.

```undefined
function App() {
  const [developer, setDeveloper] = React.useState({
    language: "",
    yearsExperience: 0,
    isEmployed: false
  });

  function handleToggleEmployment(event) {
    /* We get the previous state variable's value in the parameters.
       We can name 'prevState' however we like.
    */
    setDeveloper(prevState => {
      return { ...prevState, isEmployed: !prevState.isEmployed };
      // It is essential to return the new state from this function
    });
  }

  return (
    <button onClick={handleToggleEmployment}>Toggle Employment Status</button>
  );
}

```

### 부작용 및 사용 효과

`use Effect`를 사용하면 함수 구성 요소에서 부작용을 수행할 수 있다. 그렇다면 부작용이란 무엇일까요?

부작용은 우리가 바깥세상으로 다가가야 할 부분이다. 예를 들어, API에서 데이터를 가져오거나 DOM으로 작업할 수 있습니다.

이러한 작업은 예측할 수 없는 방식으로 구성 요소 상태를 변경할 수 있는 작업입니다(`부작용`을 일으킴).

`use Effect`는 콜백 함수(`effect` 함수)를 수락하며, 이 함수는 리렌더가 있을 때마다 기본적으로 실행됩니다.

구성 요소가 마운트되면 실행됩니다. 구성 요소 라이프사이클에서 부작용을 수행할 적절한 시기입니다.

```undefined
/* What does our code do? Picks a color from the colors array and makes it the background color */
import React, { useState, useEffect } from 'react';

function App() {
  const [colorIndex, setColorIndex] = useState(0);
  const colors = ["blue", "green", "red", "orange"];

  /* 
    We are performing a 'side effect' since we are working with an API.
    We are working with the DOM, a browser API outside of React.
  */
  useEffect(() => {
    document.body.style.backgroundColor = colors[colorIndex];
  });
  /* Whenever state is updated, App re-renders and useEffect runs */

  function handleChangeColor() {
    /* This code may look complex, but all it does is go to the next color in the 'colors' array, and if it is on the last color, goes back to the beginning */
    const nextIndex = colorIndex + 1 === colors.length ? 0 : colorIndex + 1;
    setColorIndex(nextIndex);
  }

  return (
    <button onClick={handleChangeColor}>
      Change background color
    </button>
  );
}
```

각 렌더 뒤에 효과 콜백이 실행되지 않도록 두 번째 인수인 빈 배열을 제공합니다.

```undefined
function App() {
  ...
  /* 
    With an empty array, our button doesn't work no matter how many times we click it... 
    The background color is only set once, when the component first mounts.
  */
  useEffect(() => {
    document.body.style.backgroundColor = colors[colorIndex];
  }, []);

  /* 
    How do we not have the effect function run for every state update  but still have it work whenever the button is clicked? 
  */

  return (
    <button onClick={handleChangeIndex}>
      Change background color
    </button>
  );
}
```

use Effect를 사용하면 종속성 배열을 사용하여 조건부 효과를 수행할 수 있습니다.

종속성 배열은 두 번째 인수이며 배열의 값 중 하나가 변경되면 효과 함수가 다시 실행됩니다.

```undefined
function App() {
  const [colorIndex, setColorIndex] = React.useState(0);
  const colors = ["blue", "green", "red", "orange"];

  /* 
    Let's add colorIndex to our dependencies array
    When colorIndex changes, useEffect will execute the effect function again
  */
  useEffect(() => {
    document.body.style.backgroundColor = colors[colorIndex];
    /* 
      When we use useEffect, we must think about what state values
      we want our side effect to sync with
    */
  }, [colorIndex]);

  function handleChangeIndex() {
    const next = colorIndex + 1 === colors.length ? 0 : colorIndex + 1;
    setColorIndex(next);
  }

  return (
    <button onClick={handleChangeIndex}>
      Change background color
    </button>
  );
}
```

use Effect는 마지막에 함수를 반환하여 특정 효과의 가입을 취소할 수 있도록 합니다.

```undefined
function MouseTracker() {
  const [mousePosition, setMousePosition] = useState({ x: 0, y: 0 });

  React.useEffect(() => {
    // .addEventListener() sets up an active listener...
    window.addEventListener("mousemove", handleMouseMove);

    /* ...So when we navigate away from this page, it needs to be
       removed to stop listening. Otherwise, it will try to set
       state in a component that doesn't exist (causing an error)

     We unsubscribe any subscriptions / listeners w/ this 'cleanup function')
     */
    return () => {
      window.removeEventListener("mousemove", handleMouseMove);
    };
  }, []);

function handleMouseMove(event) {
   setMousePosition({
     x: event.pageX,
     y: event.pageY
   });
}

  return (
    <div>
      <h1>The current mouse position is:</h1>
      <p>
        X: {mousePosition.x}, Y: {mousePosition.y}
      </p>
    </div>
  );
}
```

`use Effect`는 HTTP 요청(구성 요소가 마운트될 때 GET 요청)을 할 때 사용할 후크입니다.

보다 간결한 비동기/대기 구문으로 약속을 처리하려면 별도의 함수를 만들어야 합니다. (이유는?효과 콜백 기능은 비동기식일 수 없습니다.)

```undefined
const endpoint = "https://api.github.com/users/reedbarger";

// Using .then() callback functions to resolve promise
function App() {
  const [user, setUser] = React.useState(null);

  React.useEffect(() => {
    fetch(endpoint)
      .then(response => response.json())
      .then(data => setUser(data));
  }, []);
}

// Using async / await syntax to resolve promise:
function App() {
  const [user, setUser] = React.useState(null);
  // cannot make useEffect callback function async
  React.useEffect(() => {
    getUser();
  }, []);

  // We must apply async keyword to a separate function
  async function getUser() {
    const response = await fetch(endpoint);
    const data = await response.json();
    setUser(data);
  }
}

```

### 참조 및 사용 참조

Refs는 모든 React 구성 요소에서 사용할 수 있는 특수 속성입니다. 구성 요소가 마운트될 때 지정된 요소/구성 요소에 대한 참조를 만들 수 있습니다.

useRef를 사용하면 Reactref를 쉽게 사용할 수 있습니다. 우리는 (성분의 맨 위에) useRef를 호출하고 반환된 값을 요소의 ref 속성에 첨부하여 참조한다.

참조를 만들고 나면 현재 속성을 사용하여 요소의 속성을 수정(변환)하거나 해당 요소에 사용 가능한 메서드(예: `.focus()`를 호출하여 입력을 포커싱할 수 있다.

```undefined
function App() {
  const [query, setQuery] = React.useState("react hooks");
  /* We can pass useRef a default value.
     We don't need it here, so we pass in null to reference an empty object
  */
  const searchInput = useRef(null);

  function handleClearSearch() {
    /* 
      .current references the input element upon mount
      useRef can store basically any value in its .current property
    */
    searchInput.current.value = "";
    searchInput.current.focus();
  }

  return (
    <form>
      <input
        type="text"
        onChange={event => setQuery(event.target.value)}
        ref={searchInput}
      />
      <button type="submit">Search</button>
      <button type="button" onClick={handleClearSearch}>
        Clear
      </button>
    </form>
  );
}

```

## 후크 및 성능

### 리렌더 및 리액션.메모 방지

React.memo는 구성 요소가 렌더링되는 방식을 최적화할 수 있는 기능입니다.

특히, 구성 요소가 필요 없을 때 다시 렌더링되지 않도록 하는 메모화라는 프로세스를 수행합니다(메모화에 대한 보다 완전한 정의는 React.useMemo 참조).

React.memo는 상위 구성요소가 다시 렌더링될 때 구성요소 목록이 다시 렌더링되는 것을 방지하는 데 가장 큰 도움이 된다.

```undefined
/* 
  In the following application, we are keeping track of our programming skills. We can create new skills using an input, and they are added to the list (shown in the SkillList component). If we click on a skill, it is deleted.
*/

function App() {
  const [skill, setSkill] = React.useState('')
  const [skills, setSkills] = React.useState([
    'HTML', 'CSS', 'JavaScript'
  ])

  function handleChangeInput(event) {
    setSkill(event.target.value);
  }

  function handleAddSkill() {
    setSkills(skills.concat(skill))
  }

  return (
    <>
      <input onChange={handleChangeInput} />
      <button onClick={handleAddSkill}>Add Skill</button>
      <SkillList skills={skills} />
    </>
  );
}

/* But the problem, if you run this code yourself, is that when we type into the input, because the parent component of SkillList (App) re-renders, due to the state being updated on every keystroke, the SkillList is rerendered constantly (as indicated by the console.log) */

/* However, once we wrap the SkillList component in React.memo (which is a higher-order function, meaning it accepts a function as an argument), it no longer re-renders unnecessarily when our parent component does. */
const SkillList = React.memo(({ skills }) => {
  console.log('rerendering');
  return (
    <ul>
    {skills.map((skill, i) => <li key={i}>{skill}</li>)}
    </ul>
  )
})

export default App
```

### 콜백 기능 및 콜백 사용

use Callback은 부품 성능 향상에 사용되는 후크이다. 콜백 함수는 상위 구성 요소 내에서 "다시 호출"되는 함수의 이름입니다.

가장 일반적인 용도는 상태 변수가 있는 상위 구성 요소를 사용하는 것이지만 하위 구성 요소에서 해당 상태를 업데이트하려고 합니다. 무슨 일을 하세요? 콜백 함수를 부모로부터 자식에게 전달합니다. 이를 통해 상위 구성요소의 상태를 업데이트할 수 있습니다.

콜백은 리액트메모와 비슷한 방식으로 기능한다. 콜백 기능을 메모하므로 모든 리렌더에 재생성되지 않습니다. 콜백 사용을 올바르게 사용하면 앱의 성능을 향상시킬 수 있습니다.

```undefined
/* Let's keep the exact same App as above with React.memo, but add one small feature. Let's make it possible to delete a skill when we click on it. To do that, we need to filter the skills array according to the skill we click on. For that, we create the handleRemoveSkill function in App */

function App() {
  const [skill, setSkill] = React.useState('')
  const [skills, setSkills] = React.useState([
    'HTML', 'CSS', 'JavaScript'
  ])

  function handleChangeInput(event) {
    setSkill(event.target.value);
  }

  function handleAddSkill() {
    setSkills(skills.concat(skill))
  }

  function handleRemoveSkill(skill) {
    setSkills(skills.filter(s => s !== skill))
  }
    
  /* Next, we pass handleRemoveSkill down as a prop, or since this is a function, as a callback function to be used within SkillList */
  return (
    <>
      <input onChange={handleChangeInput} />
      <button onClick={handleAddSkill}>Add Skill</button>
      <SkillList skills={skills} handleRemoveSkill={handleRemoveSkill} />
    </>
  );
}

/* When we try typing in the input again, we see rerendering in the console every time we type. Our memoization from React.memo is broken! 

What is happening is the handleRemoveSkill callback function is being recreated everytime App is rerendered, causing all children to be rerendered, too. We need to wrap handleRemoveSkill in useCallback and only have it be recreated when the skill value changes.

To fix our app, replace handleRemoveSkill with:

const handleRemoveSkill = React.useCallback((skill) => {
  setSkills(skills.filter(s => s !== skill))
}, [skills])

Try it yourself!
*/
const SkillList = React.memo(({ skills, handleRemoveSkill }) => {
  console.log('rerendering');
  return (
    <ul>
    {skills.map(skill => <li key={skill} onClick={() => handleRemoveSkill(skill)}>{skill}</li>)}
    </ul>
  )
})


export default App
```

### 메모화 및 메모 사용

use Memo는 use Callback과 매우 유사하며 성능 향상을 위한 것이다. 그러나 콜백 대신 고가의 계산 결과를 저장하기 위한 것입니다.

useMemo는 특정 입력에 대해 이미 만들어진 값비싼 계산 결과를 메모하거나 기억할 수 있게 해준다.

메모화는 지정된 입력으로 이전에 계산을 수행한 경우 해당 작업의 저장된 결과를 이미 가지고 있으므로 다시 계산할 필요가 없다는 의미입니다.

useMemo는 연산에서 값을 반환하고, 그 값을 변수에 저장합니다.

```undefined
/* Building upon our skills app, let's add a feature to search through our available skills through an additional search input. We can add this in a component called SearchSkills (shown above our SkillList).
*/

function App() {
  const [skill, setSkill] = React.useState('')
  const [skills, setSkills] = React.useState([
    'HTML', 'CSS', 'JavaScript', ...thousands more items
  ])

  function handleChangeInput(event) {
    setSkill(event.target.value);
  }

  function handleAddSkill() {
    setSkills(skills.concat(skill))
  }

  const handleRemoveSkill = React.useCallback((skill) => {
    setSkills(skills.filter(s => s !== skill))
  }, [skills])
   
  return (
    <>
      <SearchSkills skills={skills} />
      <input onChange={handleChangeInput} />
      <button onClick={handleAddSkill}>Add Skill</button>
      <SkillList skills={skills} handleRemoveSkill={handleRemoveSkill} />
    </>
  );
}

/* Let's imagine we have a list of thousands of skills that we want to search through. How do we performantly find and show the skills that match our search term as the user types into the input ? */
function SearchSkills() {
  const [searchTerm, setSearchTerm] = React.useState('');  
      
  /* We use React.useMemo to memoize (remember) the returned value from our search operation and only run when it the searchTerm changes */
  const searchResults = React.useMemo(() => {
    return skills.filter((s) => s.includes(searchTerm);
  }), [searchTerm]);
    
  function handleSearchInput(event) {
    setSearchTerm(event.target.value);
  }
    
  return (
    <>
    <input onChange={handleSearchInput} />
    <ul>
      {searchResults.map((result, i) => <li key={i}>{result}</li>
    </ul>
    </>
  );
}


export default App
```

## 고급 반응 후크

### 컨텍스트 및 사용 컨텍스트

반응에서 상위 구성 요소에서 두 개 이상의 수준으로 데이터를 전달하기 위해 여러 개의 소품을 만드는 다음과 같은 문제를 피하고자 한다.

```undefined
/* 
  React Context helps us avoid creating multiple duplicate props.
  This pattern is also called props drilling.
*/

/* In this app, we want to pass the user data down to the Header component, but it first needs to go through a Main component which doesn't use it */
function App() {
  const [user] = React.useState({ name: "Fred" });

  return (
    // First 'user' prop
    <Main user={user} />
  );
}

const Main = ({ user }) => (
  <>
    {/* Second 'user' prop */}
    <Header user={user} />
    <div>Main app content...</div>
  </>
);

const Header = ({ user }) => <header>Welcome, {user.name}!</header>;
```

컨텍스트는 상위 구성 요소에서 여러 수준의 하위 구성 요소를 전달하는 데 유용합니다.

```undefined
/* 
  Here is the previous example rewritten with Context.
  First we create context, where we can pass in default values
  We call this 'UserContext' because we're passing down user data
*/
const UserContext = React.createContext();

function App() {
  const [user] = React.useState({ name: "Fred" });

  return (
    {/* 
      We wrap the parent component with the Provider property 
      We pass data down the component tree on the value prop
     */}
    <UserContext.Provider value={user}>
      <Main />
    </UserContext.Provider>
  );
}

const Main = () => (
  <>
    <Header />
    <div>Main app content</div>
  </>
);

/* 
  We can't remove the two 'user' props. Instead, we can just use the Consumer property to consume the data where we need it
*/
const Header = () => (
    {/* We use a pattern called render props to get access to the data */}
    <UserContext.Consumer>
      {user => <header>Welcome, {user.name}!</header>}
    </UserContext.Consumer>
);
```

useContext 후크는 렌더 소품 패턴을 사용하는 대신 제공자의 자식인 함수 구성 요소의 컨텍스트를 사용할 수 있게 해준다.

```undefined
function Header() {
  /* We pass in the entire context object to consume it and we can remove the Consumer tags */
  const user = React.useContext(UserContext);
    
  return <header>Welcome, {user.name}!</header>;
};

```

### 리듀서 및 사용 리듀서

리듀서는 이전 상태 개체와 작업 개체를 가져와서 새 상태 개체를 반환하는 단순하고 예측 가능한(순수) 함수입니다.

```undefined
/* This reducer manages user state in our app: */

function userReducer(state, action) {
  /* Reducers often use a switch statement to update state in one way or another based on the action's type property */
    
  switch (action.type) {
    /* If action.type has the string 'LOGIN' on it, we get data from the payload object on action */
    case "LOGIN":
      return { 
        username: action.payload.username, 
        email: action.payload.email
        isAuth: true 
      };
    case "SIGNOUT":
      return { 
        username: "",
        email: "",
        isAuth: false 
      };
    default:
      /* If no case matches the action received, return the previous state */
      return state;
  }
}
```

리듀서는 널리 사용되는 상태 관리 라이브러리 Redux(일반적으로 React와 함께 사용됨)에서 사용되는 상태를 관리하기 위한 강력한 패턴입니다.

reducers는 useState(로컬 구성요소 상태용)와 비교하여 앱 전체의 상태를 관리하기 위해 react with the useReducer hook에서 사용할 수 있다.

useReductor를 useContext와 쌍으로 구성하여 데이터를 관리하고 구성 요소를 쉽게 전달할 수 있다.

따라서 앱의 경우 사용 감소기 + 사용 컨텍스트가 전체 상태 관리 시스템이 될 수 있습니다.

```undefined
const initialState = { username: "", isAuth: false };

function reducer(state, action) {
  switch (action.type) {
    case "LOGIN":
      return { username: action.payload.username, isAuth: true };
    case "SIGNOUT":
      // could also spread in initialState here
      return { username: "", isAuth: false };
    default:
      return state;
  }
}

function App() {
  // useReducer requires a reducer function to use and an initialState
  const [state, dispatch] = useReducer(reducer, initialState);
  // we get the current result of the reducer on 'state'

  // we use dispatch to 'dispatch' actions, to run our reducer
  // with the data it needs (the action object)
  function handleLogin() {
    dispatch({ type: "LOGIN", payload: { username: "Ted" } });
  }

  function handleSignout() {
    dispatch({ type: "SIGNOUT" });
  }

  return (
    <>
      Current user: {state.username}, isAuthenticated: {state.isAuth}
      <button onClick={handleLogin}>Login</button>
      <button onClick={handleSignout}>Signout</button>
    </>
  );
}
```

### 사용자 지정 후크 쓰기

후크는 애플리케이션 전체의 구조를 재사용하기 위해 구성 요소를 생성하는 방법과 유사하게 구성 요소 간의 동작을 쉽게 재사용하기 위해 만들어졌습니다.

후크를 사용하면 필요에 따라 사용자 지정 기능을 앱에 추가할 수 있으며 기존 후크와 모두 결합할 수 있습니다.

모든 React 개발자를 위해 타사 라이브러리에 후크를 포함할 수도 있습니다. @apolo/client, react-query, swr 등 맞춤형 후크를 제공하는 훌륭한 리액트 라이브러리가 많이 있다.

```undefined
/* Here is a custom React hook called useWindowSize that I wrote in order to calculate the window size (width and height) of any component it is used in */

import React from "react";

export default function useWindowSize() {
  const isSSR = typeof window !== "undefined";
  const [windowSize, setWindowSize] = React.useState({
    width: isSSR ? 1200 : window.innerWidth,
    height: isSSR ? 800 : window.innerHeight,
  });

  function changeWindowSize() {
    setWindowSize({ width: window.innerWidth, height: window.innerHeight });
  }

  React.useEffect(() => {
    window.addEventListener("resize", changeWindowSize);

    return () => {
      window.removeEventListener("resize", changeWindowSize);
    };
  }, []);

  return windowSize;
}

/* To use the hook, we just need to import it where we need, call it, and use the width wherever we want to hide or show certain elements, such as in a Header component. */

// components/Header.js

import React from "react";
import useWindowSize from "../utils/useWindowSize";

function Header() {
  const { width } = useWindowSize();

  return (
    <div>
      {/* visible only when window greater than 500px */}
      {width > 500 && (
        <>
         Greater than 500px!
        </>
      )}
      {/* visible at any window size */}
   <p>I'm always visible</p>
    </div>
  );
}
```

### 후크 규칙

React 훅을 사용하는 데는 두 가지 필수 규칙이 있으며, 이러한 규칙이 제대로 작동하기 위해서는 위반할 수 없습니다.

- 후크는 함수 구성 요소 내에서만 사용할 수 있습니다(일반 JavaScript 기능 또는 클래스 구성 요소가 아님).
- 후크는 구성요소 상단에서만 호출할 수 있습니다(조건, 루프 또는 중첩 함수에는 사용할 수 없음).

## 결론

배울 수 있는 다른 가치 있는 개념들이 있습니다. 하지만 만약 여러분이 이 부정행위 시트에 포함된 개념을 배운다면, 여러분은 리액트 라이브러리의 가장 중요하고 강력한 부분을 잘 이해할 수 있을 것입니다.

나중에 참조할 수 있도록 이 가이드를 보관하시겠습니까?

여기에서 이 치트시트의 전체 PDF 버전을 다운로드하십시오.