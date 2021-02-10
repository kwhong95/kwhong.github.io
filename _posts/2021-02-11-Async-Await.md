---
title: "JS - Async(3) - Async-Await"
categories: 
  - JavaScript
tags:
  - js
  - async
  - await
toc: true
toc_sticky: true
toc_label: "주요 목차"
---

# {{ page.title }}
> 드디어 비동기의 꽃 Async & Await API에 대해서 배워보겠습니다.

## 1. Why use Async?

### 1. Just Function
```js
function fetchUser () {
    // do network request in 10 sec...
    return 'kwHong';
}

const user = fetchUser();
console.log(user);
// ... 
```
다음은 User를 가져오는 함수입니다. 예를 들어 이 함수를 실행할때 10초의 시간이 걸린다고 가정하면, `fetchUser()`를 실행하는 부분에서 10초동안 뒤의 로직들을 수행히지 못하게 됩니다. 뒤의 로직에 UI를 호출하는 것이 존재한다고 가정하면 어떨까요? 사용자는 User를 가져오는 10초동안 뒤에 있는 UI를 보지 못하게 됩니다. 

### 2. Using Promise
```js
function fetchUser () {
    return new Promise((resolve, reject) => {
        resolve('kwHong');
    })
}

const user = fetchUser()
.then(console.log);
```
이러한 로직은 **Promise**를 사용하는 것 또한 나쁘지 않습니다.  
하지만 보다 간편하게 작성할 수 있는 **가독성**이 좋은 Async API를 사용해보죠.

### 3. Using Async
```js
async function fetchUser () {
    return 'kwHong';
}

const user = fetchUser();
console.log(user); // Promise { 'kwHong' }
```
어떤가요? 훨씬 간결하죠? 심지어 함수 앞에 async만 사용했을 뿐인데 Promise 객체로 반환되는 것을 볼 수 있습니다. 😆

## 2. Async - Await
### 1. Using Promise
```js
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
    await delay(3000);
    return '🍎';
}

async function getBanana() {
    await delay(3000);
    return '🍌';
}

function getFruits() {
  return getApple().then(apple => {
    return getBanana().then(banana => `${apple} + ${banana}`);
  });
}

getFruits().then(console.log); // 🍎 + 🍌 (6sec...)
```
Delay 함수를 Promise와 setTimeout을 이용해서 만들고 async를 이용해 과일을 Delay와 함께 반환하는 함수를 만들었습니다.  
과일을 가져오는 함수를 생성한 뒤 Promise의 **then**을 활용해 생성했습니다.  
어떤가요? **then 체이닝** 2번 했을 뿐인데 가독성이 떨어지는 느낌이 들지 않나요?  

### 2. Using Await 
```js
async  function getBanana() {
    await delay(3000);
    return '🍌';
}

async function getFruits() {
    const apple = await getApple();
    const banana = await getBanana();
    return `${apple} + ${banana}`;
}

getFruits().then(console.log); // 🍎 + 🍌
```
너무나도 간결해졌습니다.. 하지만 여기서도 문제가 있습니다!  
바로 사과를 받고 바나나를 받는 함수를 실행할 때 총합 6초라는 시간이 걸리죠..  
두 과일을 호출하는 것은 서로 연관성이 1도 없습니다. 그렇기 떄문에 굳이 직렬적인 호출을 할 이유가 없는 것이죠.

### 3. Why Using Async-Await?

- 프로미스 체이닝을 계속 하다보면 코드의 가독성이 떨어집니다.
- async 와 await는 Promise를 간결/간편하고 동기적으로 실행되는것 처럼 보이게 만들어주는 API입니다.
- async 와 await는 새로운 것이 추가 된게 아니라, 기존에 존재하는 Promise 위에 조금 더 간편한 API를 제공함 이런 것을 **syntactic sugar** 라고 한다 (Class도 마찬가지죠.)
