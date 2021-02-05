---
layout: post
title: "JavaScript에서 시도/캐치 – JS에서 오류를 처리하는 방법"
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2020/12/neo-urban-1734495_1920-1.jpg
tags: undefined
---


프로그래밍에는 버그와 에러가 불가피하다. 내 친구는 그것들을 알 수 없는 특징이라고 부른다.

여러분이 원하는 대로 부르세요. 하지만 저는 솔직히 버그가 프로그래머로서 우리의 일을 흥미롭게 만드는 것 중 하나라고 믿습니다.

하룻밤 사이에 코드를 디버깅하려고 해도 문제가 간과한 단순한 쉼표나 그와 같은 것이었음을 알게 되면 여러분은 틀림없이 크게 웃을 것입니다. 비록, 고객이 보고한 실수는 미소보다 더 큰 인상을 줄 것이다.

그렇긴 하지만, 실수는 성가시고 뒤에서 정말 고통스러울 수 있습니다. 그래서 저는 이 글에서 자바스크립트에서 try/catch라는 것을 설명하고 싶습니다.

## JavaScript에서 try/catch 블록이란 무엇입니까?

시도/캐치 블록은 기본적으로 JavaScript에서 오류를 처리하는 데 사용됩니다. 스크립트에서 오류가 발생하지 않도록 하려면 이 코드를 사용하십시오.

이 방법은 if 문장으로 쉽게 수행할 수 있는 것처럼 보일 수 있지만 try/catch는 if/other 문장이 할 수 있는 것 이상의 많은 이점을 제공합니다. 그 중 일부는 아래에 나와 있습니다.

```undefined
try{
//...
}catch(e){
//...
}
```

시도 문을 사용하여 코드 블록의 오류를 테스트할 수 있습니다.

캐치 문으로 해당 오류를 처리할 수 있습니다. 예를 들어:

```undefined
try{ 
getData() // getData is not defined 
}catch(e){
alert(e)
}
```

이것이 기본적으로 시도/캐치 구성 방식입니다. 당신은 당신의 코드를 try block에 넣고, 오류가 발생하면, 자바스크립트는 당신이 말한대로 즉시 catch 문 제어를 합니다. 이 경우 오류를 알려줍니다.

모든 JavaScript 오류는 실제로 이름(예: 오류, 구문 오류 등)과 실제 오류 메시지의 두 가지 속성을 포함하는 개체입니다. 그렇기 때문에 경고를 할 때 참조 오류와 같은 것이 발생합니다. getData가 정의되지 않았습니다.

JavaScript의 다른 모든 개체와 마찬가지로 e.name(ReferenceError) 및 e.message(getData가 정의되지 않음)와 같이 값에 다르게 액세스하도록 결정할 수 있습니다.

그러나 솔직히 이것은 자바스크립트가 할 일과 실제로 다르지 않다. JavaScript는 콘솔에 오류를 기록할 수 있을 만큼 사용자를 존중하며 전 세계가 다음 정보를 볼 수 있도록 경고를 표시하지 않습니다.

그렇다면 try/catch 진술의 이점은 무엇입니까?

## 시도/캐치 문을 사용하는 방법

### 던지기 성명서

try/catch의 이점 중 하나는 사용자가 직접 생성한 오류를 표시할 수 있다는 것입니다. 이것을 `(던지기 오류)`라고 한다.

JavaScript에서 표시하는 이 추한 것을 원하지 않는 상황에서는 던지기 문을 사용하여 오류(예외)를 던질 수 있습니다. 이 오류는 문자열, 부울 또는 개체일 수 있습니다. 오류가 있을 경우 캐치 문에는 사용자가 던진 오류가 표시됩니다.

```undefined
let num =prompt("insert a number greater than 30 but less than 40")
try { 
if(isNaN(num)) throw "Not a number (☉｡☉)!" 
else if (num>40) throw "Did you even read the instructions ಠ︵ಠ, less than 40"
else if (num <= 30) throw "Greater than 30 (ب_ب)" 
}catch(e){
alert(e) 
}
```

이거 좋지? 하지만 우리는 자바스크립트 생성자 오류에 대한 오류를 발생시킴으로써 한 단계 더 나아갈 수 있습니다.

기본적으로 JavaScript는 오류를 6개 그룹으로 분류합니다.

- EvalError - Eval 함수에 오류가 발생했습니다.
- 범위 오류 - `1.toPrecision(500)과 같은 범위를 벗어난 숫자가 발생했습니다. To Precision은 기본적으로 숫자에 1.000과 같은 소수값을 부여하며, 숫자에는 그 중 500을 가질 수 없다.
- 참조 오류 - 선언되지 않은 변수 사용
- 구문 오류 - 구문 오류가 있는 코드를 평가할 때
- TypeError - `1.toUpperCase()`와 같은 예상 유형의 범위를 벗어나는 값을 사용하는 경우
- URI(Uniform Resource Identifier) 오류 - URI 함수에 잘못된 문자를 사용할 경우 URI 오류가 발생합니다.

그래서 이 모든 것을 가지고, 우리는 쉽게 "새로운 오류 던지기"와 같은 오류를 던질 수 있다. 이 경우 오류의 이름은 Error이고 Hi here 메시지가 됩니다. 사용자 정의 오류 생성자를 생성할 수도 있습니다. 예를 들어 다음과 같습니다.

```undefined
function CustomError(message){ 
this.value ="customError";
this.message=message;
}
```

또한 `새 사용자 정의 오류(데이터가 정의되지 않음)`를 통해 어디서나 쉽게 이 기능을 사용할 수 있습니다.

지금까지 우리는 시도/잡기 그리고 그것이 어떻게 우리의 대본이 죽는 것을 막는지에 대해 배웠지만, 그것은 실제로 달려있다. 다음 예를 살펴보겠습니다.

```undefined
try{ 
console.log({}) 
}catch(e){ 
alert(e.message) 
} 
console.log("This should run after the logged details")
```

하지만 시도 때도, 시도문을 사용해도, 여전히 작동하지 않습니다. 왜냐하면 자바스크립트에는 두 가지 주요 유형의 오류가 있기 때문이다(위에서 설명한 오류, syntaxError 등). 이러한 오류를 구문 분석 시간 오류 및 런타임 오류 또는 예외의 예라고 할 수 있습니다.

구문 분석 시간 오류는 기본적으로 엔진이 코드를 이해하지 못하기 때문에 코드 내에서 발생하는 오류입니다.

예를 들어 위에서 JavaScript는 {{}}}의 의미를 이해하지 못하므로 여기서 try/catch를 사용할 수 없습니다(작동하지 않음).

반면에 런타임 오류는 잘못된 코드에서 발생하는 오류이며, 시도/캐치가 반드시 찾아내는 오류이다.

```undefined
try{ 
y=x+7 
} catch(e){ 
alert("x is not defined")
} 
alert("No need to worry, try catch will handle this to prevent your code from breaking")
```

믿거나 말거나, 위의 코드는 유효하며 try/catch는 오류를 적절하게 처리할 것입니다.

### Finally(마지막) 성명

최종 문장은 중립 접지, 기준점 또는 시험/캐치 블록의 최종 접지와 같은 역할을 합니다. 마지막으로, 당신은 기본적으로 try/catch에서 어떤 일이 일어나든(오류 또는 오류 없음) 최종 문의 이 코드가 실행되어야 한다고 말하고 있습니다. 예를 들어:

```undefined
let data=prompt("name")
try{ 
if(data==="") throw new Error("data is empty") 
else alert(`Hi ${data} how do you do today`) 
} catch(e){ 
alert(e) 
} finally { 
alert("welcome to the try catch article")
}
```

### 중첩 시도 블록

블록을 중첩시킬 수도 있지만, 자바스크립트에 중첩되어 있는 다른 모든 것처럼(예: 예를 들어, 용도와 같은 경우) 블록은 서툴고 읽을 수 없는 경향이 있으므로 이에 반대합니다. 하지만 그건 나뿐이야.

중첩 시도 블록을 사용하면 여러 시도 문에 대해 하나의 캐치 문만 사용할 수 있습니다. 각 시도 블록에 대해 캐치 문항도 작성하기로 결정할 수 있지만 다음과 같습니다.

```undefined
try { 
try { 
throw new Error('oops');
} catch(e){
console.log(e) 
} finally { 
console.log('finally'); 
} 
} catch (ex) { 
console.log('outer '+ex); 
}
```

이 경우 외부 시도 블록에 이상이 없기 때문에 오류가 발생하지 않습니다. 오류는 내부 시도 블록에서 발생하며, 이미 자체적으로 처리 중입니다(자체 캐치 문항이 있습니다). 아래 사항을 고려하십시오.

```undefined
try { 
try { 
throw new Error('inner catch error'); 
} finally {
console.log('finally'); 
} 
} catch (ex) { 
console.log(ex);
}
```

위의 이 코드는 약간 다르게 작동합니다. 오류는 캐치 문이 없는 내부 시도 블록에서 대신 최종 문과 함께 발생합니다.

try/catch는 다음 세 가지 방법으로 작성할 수 있습니다. `노력...노력` `노력...노력`마침내 `노력해봐...`마지막으로) 그러나 오류는 이 내부 시도에서 발생합니다.

앞서 말씀드린 바와 같이, 시도/잡기에서 어떤 일이 일어나든 효과가 있기 때문에, 이 내면의 마지막 진술은 분명히 효과가 있을 것입니다. 그러나 외부 시도에는 오류가 없지만 오류를 기록할 수 있는 제어 기능이 여전히 캐치에 부여됩니다. 더 좋은 것은, 내부 시도 문에서 우리가 만든 오류를 사용한다는 것입니다. 왜냐하면 오류가 거기서 오기 때문입니다.

외부 시도에 대한 오류를 생성한다면 내부 시도에 자체 오류가 발생하는 것을 제외하고 작성된 내부 오류를 계속 표시합니다.

이너 캐치에 코멘트를 달면 아래의 코드를 가지고 놀 수 있습니다.

```undefined
try { 
try { 
throw new Error('inner catch error');
} catch(e){ //comment this catch out
console.log(e) 
} finally { 
console.log('finally'); 
} 
throw new Error("outer catch error") 
} catch (ex) { 
console.log(ex);
}
```

### 다시 던지기 오류

캐치프레이트는 실제로 오는 모든 오류를 포착합니다. 그리고 때때로 우리는 그것을 원하지 않을 수도 있습니다. 예를 들면,

```undefined
"use strict" 
let x=parseInt(prompt("input a number less than 5")) 
try{ 
y=x-10 
if(y>=5) throw new Error(" y is not less than 5") 
else alert(y) 
}catch(e){ 
alert(e) 
}
```

입력되는 숫자가 5보다 적다고 가정해 봅시다(`엄격한 사용`의 목적은 코드가 "엄격한 모드"에서 실행되어야 한다는 것을 나타내기 위함입니다). 예를 들어, 엄격한 모드에서는 선언되지 않은 변수(소스)를 사용할 수 없습니다.

나는 trystatement에서 y의 오류를 발생시키는 것을 원한다. y 값이 불가능에 가까운 5보다 클 때. 위의 오류는 y보다 작지 않아야 합니다... 그리고 noty는 정의되지 않았다.

이와 같은 경우 오류 이름을 확인하고, 오류 이름이 원하는 이름이 아닌 경우 다음 오류 이름을 다시 던질 수 있습니다.

```undefined
"use strict" 
let x = parseInt(prompt("input a number less than 5"))
try{
y=x-10 
if(y>=5) throw new Error(" y is not less than 5") 
else alert(y) 
}catch(e){ 
if(e instanceof ReferenceError){ 
throw e
}else alert(e) 
} 

```

그러면 여기서 스크립트를 가져오거나 끊기 위한 다른 시도 문의 오류가 다시 발생합니다. 이 기능은 특정 유형의 오류만 모니터링하려는 경우 유용하며 부주의로 인해 발생할 수 있는 기타 오류는 코드를 깨야 합니다.

## 결론

이 기사에서는 시도/획득과 관련된 다음 개념을 설명하려고 했습니다.

- 시도/잡기 문항 및 작동 시기
- 사용자 정의 오류 발생 방법
- 최종 진술이 무엇이며 어떻게 작동하는지
- 네스팅 시도/캐치 문의 작동 방식
- 오류를 다시 던지는 방법

읽어주셔서 감사합니다. 트위터 @fakoredeDami로 따라오세요.