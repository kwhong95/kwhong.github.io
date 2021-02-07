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

# {{ page.title }}

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
