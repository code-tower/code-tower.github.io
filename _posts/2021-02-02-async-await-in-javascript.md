---
layout: post
title: "예제 JS 코드로 JavaScript에서 Async / Await를 사용하는 방법
 "
author: 'Code Tower'
thumbnail: https://www.freecodecamp.org/news/content/images/size/w600/2021/01/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--12-.png
tags: undefined
---


이 튜토리얼에서는 JavaScript에서 Async / Await를 사용하는 방법을 배웁니다.
 

하지만 거기에 가기 전에 다음과 같은 몇 가지 주제를 이해해야합니다.
 

- 이벤트 루프
 
- 콜백
 
- 약속
 

## JavaScript의 이벤트 루프는 무엇입니까?
 

이벤트 루프는 JavaScript의 가장 중요한 측면 중 하나입니다.
 

JavaScript는 한 번에 하나의 작업 만 실행할 수있는 단일 스레드 프로그래밍 언어입니다.
 호출 스택이 있고 모든 코드가이 호출 스택 내에서 실행됩니다.
 예를 들어 이해합시다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--8-.png)

위의 예에서 콘솔에 두 개의 값을 기록하고 있음을 알 수 있습니다.
 

`First ()`가 실행을 마치면 호출 스택에서 튀어 나오고 이벤트 루프가 다음 줄로 이동합니다.
 다음 줄은 호출 스택에 저장되고 실행 플래그가 지정됩니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/01/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--9-.png)

콘솔은 다음 결과를 인쇄합니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--18-.png)

더 잘 이해하기 위해 다른 예를 살펴 보겠습니다.
 

```js
console.log('First!');

setTimeout(function second(){
    console.log('Timed Out!')
}, 0000)

console.log('Final!');
```

평소와 같이 코드는 호출 스택으로 이동하고 이벤트 루프는 한 줄씩 반복됩니다.
 

우리는 "First!"를 얻을 것입니다.
 콘솔에서 호출 스택 밖으로 이동됩니다.
 

이제 이벤트 루프가 두 번째 줄로 이동하여 호출 스택으로 푸시합니다.
 매크로 태스크 인`setTimeout` 함수를 만나고 다음 이벤트 루프에서 실행됩니다.
 

이제 매크로 작업이 무엇인지 궁금 할 것입니다.
 글쎄, 그것은 이벤트 루프의 모든 작업 후에 실행되는 작업입니다. 또는 다른 이벤트 루프에서 말할 수 있습니다.
 `SetTimeout` 및`SetInterval` 함수는 다른 모든 작업이 완료된 후 실행되는 매크로 작업의 예가 될 수 있습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--19-.png)

마지막으로 코드의 마지막 줄이 실행됩니다.
 콘솔에서 First, Final, Timed Out 순으로 표시됩니다.
 

## 콜백 함수는 JavaScript에서 어떻게 작동합니까?
 

콜백 함수는 다른 함수에 인수로 전달 된 함수입니다.
 

예를 살펴 보겠습니다.
 

```js
const movies = [
{ title: `A New Hope`, body:`After Princess Leia, the leader of the Rebel Alliance, is held hostage by Darth Vader, Luke and Han Solo must free her and destroy the powerful weapon created by the Galactic Empire.`},
{ title: `The Empire Strikes Back`, body: `Darth Vader is adamant about turning Luke Skywalker to the dark side. Master Yoda trains Luke to become a Jedi Knight while his friends try to fend off the Imperial fleet.` }]

function getMovies(){
    setTimeout(() => {
        movies.forEach((movie, index) => {
            console.log(movie.title)
        })
    }, 1000);
}

getMovies();
```

Star Wars 영화 목록과 목록을 가져 오는 함수`getMovies ()`를 포함하는 배열이 있습니다.
 

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--20-.png)

`createMovie ()`라는 또 다른 함수를 만들어 보겠습니다.
 새 영화를 추가하는 데 사용됩니다.
 

```js
const movies = [
        { title: `A New Hope`, body:`After Princess Leia, the leader of the Rebel Alliance, is held hostage by Darth Vader, Luke and Han Solo must free her and destroy the powerful weapon created by the Galactic Empire.`},
        { title: `The Empire Strikes Back`, body: `Darth Vader is adamant about turning Luke Skywalker to the dark side. Master Yoda trains Luke to become a Jedi Knight while his friends try to fend off the Imperial fleet.` }
    ]

function getMovies(){
    setTimeout(() => {
        movies.forEach((movie, index) => {
            console.log(movie.title)
        })
    }, 1000);
}

function createMovies(movie){
    setTimeout(() => {
        movies.push(movie)
    }, 2000);
}

getMovies();


createMovies({ title: `Return of the Jedi`, body:`Luke Skywalker attempts to bring his father back to the light side of the Force. At the same time, the rebels hatch a plan to destroy the second Death Star.` });
```

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--20--1.png)

하지만 여기서 문제는 우리가 콘솔에서 세 번째 영화를 얻지 못한다는 것입니다.
 `createMovie ()`가`getMovies ()`보다 오래 걸리기 때문입니다.
 `createMovie ()`함수는 2 초가 걸렸지 만`getMovies ()`는 1 초 밖에 걸리지 않았습니다.
 

즉,`getMovies ()`가`createMovies ()`보다 먼저 실행되고 영화 목록이 이미 표시됩니다.
 

이를 해결하기 위해 콜백을 사용할 수 있습니다.
 

`createPost ()`에서 함수 콜백을 전달하고 새 영화가 푸시 된 직후에 함수를 호출합니다 (2 초 동안 기다리지 않음).
 

```js
const movies = [
        { title: `A New Hope`, body:`After Princess Leia, the leader of the Rebel Alliance, is held hostage by Darth Vader, Luke and Han Solo must free her and destroy the powerful weapon created by the Galactic Empire.`},
        { title: `The Empire Strikes Back`, body: `Darth Vader is adamant about turning Luke Skywalker to the dark side. Master Yoda trains Luke to become a Jedi Knight while his friends try to fend off the Imperial fleet.` }
    ]

function getMovies(){
    setTimeout(() => {
        movies.forEach((movie, index) => {
            console.log(movie.title)
        })
    }, 1000);
}

function createMovies(movie, callback){
    setTimeout(() => {
        movies.push(movie);
        callback();
    }, 2000);
}


createMovies({ title: `Return of the Jedi`, 
                body:`Luke Skywalker attempts to bring his father back to the light side of the Force. 
                At the same time, the rebels hatch a plan to destroy the second Death Star.` }, getMovies);
```

![image](https://www.freecodecamp.org/news/content/images/2021/02/Pink-Cute-Chic-Vintage-90s-Virtual-Trivia-Quiz-Presentations--21--2.png)

이제 업데이트 된 영화 목록을 얻습니다.
 

## 프라 미스는 JavaScript에서 어떻게 작동합니까?
 

약속은 미래에 가치를 창출 할 수있는 가치입니다.
 이 값은 해결되거나 해결되지 않을 수 있습니다 (네트워크 장애와 같은 일부 오류의 경우).
 실제 약속처럼 작동합니다.
 

처리됨, 거부 됨 또는 보류 중이라는 세 가지 상태가 있습니다.
 

- Fulfilled :`onFulfilled ()`가 호출됩니다 (예 :`resolve ()`가 호출 됨).
 
- 거부 됨 :`onRejected ()`가 호출됩니다 (예 :`reject ()`가 호출 됨).
 
- 보류 중 : 아직 이행 또는 거부되지 않았습니다.
 

예를 살펴 보겠습니다.
 

Promise는 해결과 거부라는 두 가지 매개 변수를 사용합니다.
 무언가 잘못되면 reject가 호출되거나 resolve가 호출됩니다.
 

```js
const movies = [
        { title: `A New Hope`, body:`After Princess Leia, the leader of the Rebel Alliance, is held hostage by Darth Vader, Luke and Han Solo must free her and destroy the powerful weapon created by the Galactic Empire.`},
        { title: `The Empire Strikes Back`, body: `Darth Vader is adamant about turning Luke Skywalker to the dark side. Master Yoda trains Luke to become a Jedi Knight while his friends try to fend off the Imperial fleet.` }
    ]

function getMovies(){
    setTimeout(() => {
        movies.forEach((movie, index) => {
            console.log(movie.title)
        })
    }, 1000);
}

function createMovies(movie){
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            movies.push(movie);

            const error = false;

            if(!error){
                resolve();
            }
            else{
                reject('Error: Something went wrong!')
            }
        }, 2000);
    })
}

createMovies({ title: `Return of the Jedi`, body:`Luke Skywalker attempts to bring his father back to the light side of the Force. At the same time, the rebels hatch a plan to destroy the second Death Star.`})
.then(getMovies);
```

오류가 발생하면 `오류 : 문제가 발생했습니다!`와 같은 오류가 발생하고 그렇지 않으면 약속이 해결됩니다.
 

프라 미스가 해결되면`.then ()`키워드와`getMovies ()`를 호출합니다.
 

## 마지막으로 JavaScript에서 Async / Await는 어떻게 작동합니까?
 

비동기는 비동기를 의미합니다.
 프로그램이 전체 프로그램을 동결하지 않고 기능을 실행할 수 있습니다.
 이것은 Async / Await 키워드를 사용하여 수행됩니다.
 

Async / Await를 사용하면 promise를 더 쉽게 작성할 수 있습니다.
 함수 앞에 키워드 `async`는 함수가 항상 약속을 반환하도록합니다.
 그리고 키워드 await는 비동기 함수 내에서 사용되어 Promise가 해결 될 때까지 프로그램을 대기시킵니다.
 

```js
async function example() {

  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("done!"), 2000)
  });

  let result = await promise; // wait until the promise resolves (*)

  alert(result); // "done!"
}

example();
```

함수 실행은`(*)`줄에서 "일시 중지"되고 프라 미스가 충족되면 다시 시작되며`result`가 결과가됩니다.
 따라서 위의 코드는 "완료!"를 보여줍니다.
 2 초 안에.
 

실습 예제를 살펴 보겠습니다.
 

```js
const movies = [
        { title: `A New Hope`, body:`After Princess Leia, the leader of the Rebel Alliance, is held hostage by Darth Vader, Luke and Han Solo must free her and destroy the powerful weapon created by the Galactic Empire.`},
        { title: `The Empire Strikes Back`, body: `Darth Vader is adamant about turning Luke Skywalker to the dark side. Master Yoda trains Luke to become a Jedi Knight while his friends try to fend off the Imperial fleet.` }
    ]

function getMovies(){
    setTimeout(() => {
        movies.forEach((movie, index) => {
            console.log(movie.title)
        })
    }, 1000);
}

function createMovies(movie){
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            movies.push(movie);

            const error = false;

            if(!error){
                resolve();
            }
            else{
                reject('Error: Something went wrong!')
            }
        }, 2000);
    })
}

async function init(){
    await createMovies({ title: `Return of the Jedi`, body:`Luke Skywalker attempts to bring his father back to the light side of the Force. At the same time, the rebels hatch a plan to destroy the second Death Star.`});
    
    getMovies(); (*)
}

init();
```

위의 예에서 (*) 줄의`getMovies ()`는 비동기 함수에서`createMovies ()`가 실행되기를 기다리고 있습니다.
 

즉,`createMovies ()`는 비동기식이므로`getMovies ()`는`createMovies ()`가 완료된 후에 만 실행됩니다.
 

이제 Event Loops, Callbacks, Promise 및 Async / Await의 모든 기본 사항을 알았습니다.
 이러한 기능은 ECMAScript 2017에서 도입되었으며 JS 코드를 훨씬 쉽고 효과적으로 읽고 쓸 수있게되었습니다.
 

> 그게 다야!
 즐거운 학습과 실험,
 