---
title: "JS Functions 함수"
categories: 
  - JavaScript
tags:
  - js
  - function
toc: true
toc_sticky: true
toc_label: "주요 목차"
---

<img width="275" alt="스크린샷 2021-02-07 오후 11 05 13" src="https://user-images.githubusercontent.com/70752848/107148885-fa498600-6998-11eb-8bf8-43a04e044789.png">

프로그램에는 다양하고 중요한 기능을 하는 **함수**들이 존재하는데요.  
그렇기 때문에 **함수**를 **Sub-Program**이라고 불려지기도 한답니다.  

<img width="358" alt="스크린샷 2021-02-07 오후 11 16 43" src="https://user-images.githubusercontent.com/70752848/107149179-8c9e5980-699a-11eb-82d0-ac1e54d2db5b.png">

함수의 구조를 그림으로 한번 표현해 봤는데요.  
함수는 대체적으로 Input(parameters)을 받아서 기능을 수행한 다음  
Output(return)으로 반환하는 것을 표현합니다.
그렇기 때문에 함수는 Input, Output을 설정하는 것도 중요하지만  
어떤 기능을 수행하는지 표현하기 위한 **네이밍** 또한 중요하다고 합니다.

**함수란 무엇인가?**
1. 프로그램의 기본 구성 요소입니다.
2. 하위 프로그램을 여러 번 사용 가능합니다.
3. 작업을 수행하거나 값을 계산합니다.

## 1. Function declaration

1. **function의 사용 방법**
```js
function name(pram1, param2) {
  body...
  return value;
}
```
2. **하나의 함수는 한가지 기능만 수행해야 한다.**  
3. 네이밍 방법  
함수는 무언가 기능을 수행하는 것이기 때문에   
`Do something`, `Command`, `Verb(동사)`의 형태로 작성해야 합니다.  
혹시 함수의 네이밍이 어렵다면 이 함수가 너무 많은 기능을 하고 있는지 생각해봐야합니다. 그렇지 않다면 어려울 이유가 없겠죠? :)
4. **JS에서 함수는 Object 입니다.**  
그렇기 때문에 함수는 다른 함수에 전달할 수도 있고 값으로 할당할 수 있게 됩니다.

```js
function printLog(message) {
  console.log(message);
}
printLog('Hello'); // Hello
```
이렇게 함수에 매개변수를 인가하여 콘솔에 무언가를 출력하는 기능을 수행하는 함수를 만들 수 있습니다.  
하지만 JS에는 타입이 없기 때문에 string을 출력하는 함수에 number를 넣어서 출력해도 출력이 가능하죠? 이건 상당히 큰 문제를 야기 할수 있습니다.  
그래서 보통 Typescript처럼 타입을 정의해주는 것을 선호합니다.
```ts
function printLog(message: string) {
  console.log(message);
}
```
이런식으로 타입을 지정해준다면 number를 입력하면 *Type Error* 가 발생하게 되죠. 그래서 꼭 JS를 공부한 뒤엔 TS를 공부하는 것을 추천합니다.

## 2. Parameters
함수에 인가하는 **Parameter**에 대해서 알아보겠습니다.  
primitive parameters는 메모리에 그대로 저장되어 있기 때문에 value 형태로 전달이 됩니다.  
object parameters 경우에는 레퍼런스가 저장되어 있기 때문에 ref가 전달이 되죠.  

```js
function changeName(obj) {
    obj.name = 'kwhong';
}
const anyName = { name: 'anyName' };
changeName(anyName);
console.log(anyName); 
//  { name: 'kwhong' }
```
위처럼 `anyName`의 오브젝트는 ref 형태로 메모리에 저장될 것이고요.  
`changName` 함수를 이용하여 오브젝트 ref를 변환하는 형태입니다.

## 3. Default Parameters
```js
function showMessage(message, from = 'unknown') {
    console.log(`${message} by ${from}`);
}
showMessage('Hi'); // Hi by unknown
```
`Default parameters`는 **ES6**부터 추가된 문법입니다.  
바로 parameter에 값을 직접 인가해주어 **Defalut value**를 설정해주는 것입니다.  

## 4. Rest Parameters
```js
function printAll(...arg) {
    for(let i = 0; i < arg.length; i++) {
        console.log(arg[i]);
    }
}

printAll('exciting', 'coding', 'kwhong');
// exciting
// coding
// kwhong
```
`Rest Parameters` 또한 **ES6**부터 추가된 문법인데요.  
`...arg`로 파라미터를 배열 형태로 설정이됩니다. 즉, `printAll()`에 인가된 파라미터가 `['exciting', 'coding', 'kwhong']` 이런 배열 형태로 설정이 되는 것이죠.

## 5. Local scope
```js
let globalMessage = 'global'; // global variable
function printMessage() {
    let message = 'Hello';
    console.log(message); // local variable
    console.log(globalMessage);
}
printMessage();
console.log(message); // Reference Error!
```
함수 프로그래밍을 할때 중요한 개념인 **Local scope**를 알아보겠습니다.  
이해를 쉽게 하기 위해 `'안에서는 밖이 보이지만 안에서는 밖을 볼 수 없다'`라는 개념인데요. 함수 내부의 변수는 함수 내부에서만 사용이 가능하고 외부에서는 접근할 수 없다는 개념입니다. 그래서 함수 내부의 message 변수는 밖에서 접근하려고하면 *Reference Error* 가 발생하게 되죠.

## 6. Return a value
```js
function sum(a, b) {
    return a + b;
}
const result = sum(1, 2); // 3
console.log(`sum: ${sum(1,2)}`); // sum: 3
```
함수는 값을 리턴하는 기능을 가지고 있습니다. (defalut: undefined)  

## 7. Early return, Early exit
```js
function upgradeUser(user) {
    if (user.point <= 10) {
        return;
    }
    // long upgrade logic ...
}
```
위 로직을 살펴보면 빠르게 리턴을 실행하고 추후에 다른 로직을 작성하는 것을 의미하는데요. 즉, 조건에 맞는 것은 빠르게 리턴을 해주고 부합할 시에 다른 로직을 수행하도록 작성하는 것이 가독성에 좋다고 합니다.

## 8. Function expression
> 함수 표현식에 대해서 알아보기 전에 혹시 First-class function에 대해서 기억이 나시나요?

**First-class function**은 간단히 다시 말하자면 함수는 변수로 설정이 가능하다는 것이었죠. 그래서 **함수 표현식**이 가능합니다.
```js
const print = function() {
    console.log('print');
}
print();
const printAgain = print;
printAgain();
const sumAgain = sum;
console.log(sumAgain(1, 3));
```
위 함수는 print 라는 const 변수로 설정된 함수입니다.  
이렇게 아무 이름없이 값으로 할당된 함수를 **anonymous function**라고 부릅니다. 또한 위처럼 다른 변수에 할당할 수도 있고 위에 정의한 sum 함수 또한 재할당해서 사용할 수 있습니다.  

**함수 표현식과 함수 선언의 차이점**  
함수 선언은 바로 **var** 처럼 **호이스팅**이 이루어집니다
그래서 많은 개발자들은 **함수 표현식**으로 함수를 작성하는 것을 선호합니다.  

## 9. Callback function
```js
function randomQuiz(answer, printYes, printNo) {
    if (answer === 'good') {
        printYes();
    } else {
        printNo();
    }
}

const printYes = function () {
    console.log('yes!');
}

const printNo = function () {
    console.log('no!');
}

randomQuiz('wrong', printYes(), printNo());
randomQuiz('good', printYes(), printNo());
```
**Callback Function**은 바로 함수의 매개 변수에 함수를 인가하여 표현하는 함수입니다. 위처럼 정답이면 `yes!`를 틀리면 `no!`를 출력하는 함수를 만들었는데요. 뒤에 호출부분에서 매개변수로 함수를 전달하는 것입니다.


## 10. Arrow function
```js
const simplePrint = function() {
  console.log('simplePrint!')l
}
```
**Arrow Function**은 함수를 작성할 때 매우 간결하게 작성할 수 있도록 도와주는 유용한 친구입니다.
```js
const simplePrint = () => console.log('simplePrint!');
```
보이시나요? function 키워드와 return, 블록을 작성하지 않아도 한줄에 간결하게 작성할 수 있습니다. :)

## 11. IIFE
```js
(function hello() {
    console.log('IIFE');
})();
```
함수를 사용하다보면 그 위치에서 바로 호출하고 싶은 경우가 생길 수 있습니다.  
이 때 바로 IIFE(Immediately Invoked Function Expression)를 사용하면 바로 호출이 가능합니다. 위처럼 말이죠 :)

## 12. Quiz 
```js
// Quiz
// function calculate(command a, b)
// command: add, sub, divide, multiply, remainder
```
이번까지 배운것을 활용할 퀴즈입니다. 정답은 다음 포스트에 :)