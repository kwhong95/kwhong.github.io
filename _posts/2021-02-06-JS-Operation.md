---
title: "JS - 연산 & 반복문"
categories: 
  - JavaScript
tags:
  - js
  - operation
  - while
toc: true
toc_sticky: true
toc_label: "주요 목차"
---

# {{ page.title }}

> 실제로 현업에서 주니어 개발자들이 태클을 많이 받는곳이 이 연산파트라고 합니다 ;)  

## 1. 지난 시간 복습하기

지난시간 변수에 대해서 공부를 했었는데 자주 사용하는 것들이 기억나시나요?  
바로 변경가능한 즉, `Read / Write`가 가능한 **let**과  
`Read only`인 **const** 가 있었죠?  
그래서 굳이 변경할 이유가 없는 고정된 값을 할당하는 변수라면 **const** 를 사용하는 편이  
좋다고 말씀드렸구요  
  
  또한 변수에 타입(Primitive & Object)에 따라서 메모리에 다르게 저장이 다르게 이루어집니다.  

**Primitive**

<img width="507" alt="스크린샷 2021-02-06 오후 5 01 53" src="https://user-images.githubusercontent.com/70752848/107112721-06501d80-689d-11eb-8095-a54564b2ccdc.png">

Primitive Type은 메모리에 직접 값이 할당되는 것을 볼 수 있습니다.

**Object**

<img width="923" alt="스크린샷 2021-02-06 오후 11 31 55" src="https://user-images.githubusercontent.com/70752848/107121015-82fdee80-68d3-11eb-8c25-78d643b16f7e.png">

Object Type은 메모리에 **Reference**가 저장되고  그 **Reference**가 잠기게 되고 내부 변수(name & age)의 값은 변경이 가능하는 것까지 알아보았습니다.

**Mutable Data Type**
  - **Object**
  **Object**는 내부 변수들을 변경할 수 있기 때문에 **Mutable**한 데이터입니다. 그리고 JS의 거의 모든 **Object**는 기본값으로 **Mutable** 설정을 가지고 있습니다.

**Immutable Data Type**
  - **Primitive Types**  
  Primitive 데이터는 변경 불가능한 데이터인데요.  
  예를 들면 
  ```js
  let name = 'hong';
  ```
  위의 `hong`이라는 `string data`이고, 각 글자하나를 변경할 수 없는 데이터 타입이기에 **Imutable** 하다고 합니다. 

- **Fronzen Object**   
  ```js
  object.freeze();
  ```
  말그대로 얼어버린 object 타입 또한 변경이 불가능한 **Imutable** 데이터 타입입니다.

## 2. String concatenation
이제 본격적으로 Operation에 대해서 알아보겠습니다.  
첫번째는 바로 문자열 연산입니다.
```js
console.log('my' + 'cat'); // mycat
console.log('1' + 2); // 12
console.log(`string literals: 1 + 2 = ${1 + 2}`); // string literals: 1 + 2 = 3
```
앞서 데이터 타입에서도 공부했었죠? 가장 중요한 것은 **template literals**를 잘 활용해서 표현하는 것입니다.

## 3. Numeric operators
```js
console.log(1 + 1); // add
console.log(1 - 1); // substract
console.log(1 / 1); // divide
console.log(1 * 1); // multiply
console.log(5 % 2); // remainder
console.log(2 ** 3); // exponentiation
```
보시다시피 모든 산술연산이 가능합니다 :)

## 4. ++, -- operators

### 1. PreIncrement operator
```js
let counter = 2;
const preIncrement = ++ counter;
console.log(`preIncrement: ${preIncrement}, counter: ${counter}`);
// preIncrement: 3, counter: 3
```
변수 앞에 **++** 기호를 사용한 연산자입니다. 특징은 말그대로 앞서 변수의 값을 처리해줍니다. `counter + 1` 값을 처리한 다음에 preIncrement에 할당시키는 것이죠.

### 2. PostIncrement operator
```js
// counter = 3
const postIncrement = counter ++;
console.log(`postIncrement: ${postIncrement}, counter: ${counter}`);
// postIncrement: 3, counter: 4
```
반대로 **postIncrement**는 먼저 counter 값을 먼저 할당한 뒤에 연산처리를 하는 기능입니다.

### 3. Decrement operator
```js
// counter = 4
const preDecrement = --counter;
console.log(`preDecrement: ${preDecrement}, counter: ${counter}`);
// preDecrement: 3, counter: 3

const postDecrement = counter--;
console.log(`postDecrement: ${postDecrement}, counter: ${counter}`);
// postDecrement: 3, counter: 2
```
마찬가지로 **Decrement** 똑같이 동작합니다. 이 연산은 추후에 로직을 구성할때 자주 사용하므로 꼭 익혀두셔야 합니다.

## 5. = Operators
```js
let x = 3;
let y = 6;
x += y; // x = x + y;
x -= y; // x = x - y;
x *= y; // x = x * y;
x /= y; // x = x / y;
```
다음은 **할당(Assignment) Operators** 입니다.  
주석 부분과 같이 동작하며 반복되는 x변수를 생략해서 작성합니다.

## 6. <= Operators
```js
console.log(10 < 6); // less than
console.log(10 <= 6); // less than or equal
console.log(10 > 6); // greater than
console.log(10 >= 6); // greater than or equal
```
다음은 **비교(Comparison) Operators** 입니다.
같거나 크고 작거나 같고 이런 연산자입니다 :)

## 7. Logical operators
> 이제부터 본격적인 로직을 작성하는데 중요한 연산자를 배웁니다!!

### 1. || (or)
```js
const value1 = true;
const value2 = 4 < 2;

console.log(`or: ${value1 || value2 || check()}`);
// or: true

function check() {
    for (let i = 0; i < 10; i++) {
        console.log('Shit...');
    }
    return true;
}
```
**Or 연산자** 인데요, 비교하는 것중에 **하나**라도 true를 반환하면 값이 true로 할당됩니다. 여기서 중요한점은 연산중에 true가 된다면 그곳에서 수행을 멈춥니다. 그리하여 뒤에 있는 `check()`는 수행되지 않기 때문에 출력되지 않는것을 볼 수 있습니다. 그리하여 복잡한 로직을 수행하는 것을 뒤로 배치하는 것이 효율적이겠죠?

### 2. && (and)
```js
console.log(`and: ${value1 && value2 && check()}`);
```
다음은 **And 연산자**입니다. 비교하는 세 변수가 **모두** true면 true를 반환하게 됩니다. 똑같이 false가 체킹되는 순간 수행을 멈춥니다. 그리하여 마찬가지로 무거운 로직은 뒤로 보내는 편이 효율적입니다. 보통 **null checking**을 할 때 사용하게 되는데요.

**null checking logic**
```js
if (nullableObject != null) {
  nullableObject.something;
}
```
`null` 이아니면 Object의 something값을 가져오는 로직인데요.  
위처럼 null이면 수행하지 않고 아니면 가져온다. 이런 개념으로 자주 사용합니다.

### 3. ! (not)
```js
console.log(!value1); // false
```
**Not 연산자**는 너무 쉽죠? 값을 반대로 바꾸어주는 연산자입니다.

## 8. Equality operators 
```js
const stringFive = '5';
const numberFive = 5;

console.log(stringFive == numberFive); // true
console.log(stringFive != numberFive); // false

console.log(stringFive === numberFive); // false
console.log(stringFive !== numberFive); // true
```
**==** 연산자는 비교적 루즈한 비교입니다. 오직 값만을 비교합니다.  
string 5 와 number 5는 내용은 5라는 값이기 때문에 비교시 true를 반환하죠.  
**===** 연산자는 비교적 엄격한 비교를 수행합니다. 값의 type까지 비교하고 되도록이면 이 연산을 사용하는 것을 선호합니다 엄격하면 그만큼 안정적인 로직이 작성되기 때문이죠 :)

**Object의 레퍼런스 비교**

```js
const kwhong1 = { name: 'kwhong' };
const kwhong2 = { name: 'kwhong' };
const kwhong3 = kwhong1;
console.log(kwhong1 == kwhong2); // false
console.log(kwhong1 === kwhong2); // false
console.log(kwhong1 === kwhong3); // true
```
**Object**를 비교할 때는 앞서 본 Reference의 개념을 잘 이해해야 합니다.  
바로 비교를 수행할 때 메모리에 참조된 래퍼런스를 비교하기 때문이죠.  
안의 변수와 값이 같게 할당되었지만 가르키고 있는 레퍼런스가 다르기 때문에 false가 반환되며 같은 레퍼런스를 가르키면 보시다시피 true가 반환됩니다.

### Quiz
```js
console.log(0 == false);
console.log(0 === false);
console.log('' == false);
console.log('' === false);
console.log(null == undefined);
console.log(null === undefined);
```
정답은??? :-)

## 9. If operators
```js
const name = 'kwhong';
if (name === 'kwhong') {
    console.log('Hello kwhong');
} else if (name === 'shkim') {
    console.log('Hello shKim');
} else {
    console.log('unknown');
}
```
정말정말 중요한 **Conditional 연산자(if)**입니다.  
if, else if, else 이 세 연산자로 값을 비교한 뒤 상황에 맞는 것을 출력하는 로직을 작성할 수 있습니다.

## 10. ? operators
```js
console.log(name === 'kwhong' ? 'yes' : 'no');
```
이것도 정말 중요한 **Ternary 연산자(?)**입니다.
값을 비교한 뒤 **?** 기호를 통해 true와 false의 반환에 따라 다른 출력을 가져오는 로직을 작성할 수 있습니다. 매우매우 유용하죠.

## 11. Switch operator
```js
const browser = 'IE';
switch (browser) {
    case 'IE':
        console.log('go away!');
        break;
    case 'Chrome':
        console.log('love you!');
        break;
    case 'Firefox':
        console.log('love you!');
        break;
    default:
        console.log('same all!');
        break;
}
```
다음도 정말 유용한 연산자인 **Switch**입니다.  
case로 경우의 수를 나누어 출력 값을 다르게 설정할 수 있죠.  
보시면 Chrome과 Firefox의 경우 출력값이 같죠?
```js
case 'Chrome':
case 'Firefox':
  console.log('love you');
  break;
```
그렇다면 이렇게 두 경우를 합쳐서 간단하게 로직을 작성할 수도 있습니다 :)

## 12. Loops
### 1. While loop
```js
let i = 3;
while (i > 0) {
    console.log(`while: ${i}`);
    // while: 3
    // while: 2
    // while: 1
    i--;
}
```
이번엔 **반복문**입니다. 먼저 **While문**인데요.  
이 반복문은 false를 반환하기 전까지 무한대로 반복하는 기능을 수행합니다.

### 2. Do-while loop
```js
// i = 0
do {
    console.log(`do while: ${i}`);
    // do while: 0
    i--;
} while (i > 0);
```
**Do while문**은 while과 다르게 먼저 로직을 수행한 뒤 조건을 검사합니다. 그래서 false를 반환하기 전에 수행했기 때문에 콘솔에 결과값이 찍히는 것을 확인할 수 있죠.

### 3. For loop
```js
for (let i = 3; i > 0; i = i - 2) {
    console.log(`inline variable for: ${i}`);
    // inline variable for: 3
    // inline variable for: 1
}
```
다음은 정말정말 자주보게 될 **for문**입니다. 위처럼 먼저 조건을 수행할 변수를 선언하고 어느 상황까지 로직을 수행할지, 로직을 어떻게 수행할지에 대한 것을 작성합니다.

### 4. nested loops
```js
for (let i = 0; i < 10; i++) {
    for (let j = 0; j < 10; j++) {
        console.log(`i: ${i}, j: ${j}`);
    }
}
```
While 과 For 문은 이렇게 nesting 해서 로직을 작성할 수도 있는데요.
이것은 [시간복잡도](https://blog.chulgil.me/algorithm/) 개념에서 `Big O(n^2)`가 됩니다. CPU의 성능상 안좋기 때문에 꼭 필요한 경우에만 사용하는 것이 좋습니다.

### 5. Quiz 
```js
// break, continue
// Q1. iterator from 0 to 10 and print only even numbers(use continue)

// Q2. iterate from 0 to 10 and print numbers until reaching 8(use break)
```
지금까지 배운것을 활용할 퀴즈입니다. 

### 6. Quiz - Solution
```js
// Q.1 Solution
for (let i = 0; i <= 10; i++) {
    if( i%2 !== 0 ) {
        continue;
    }
    console.log(`i: ${i}`);
}

// Q.2 Solution
for (let i = 0; i <= 10; i++) {
    if ( i > 8 ) {
        break;
    }
    console.log(`i: ${i}`);
}
```
정답은 절대 아니구요! 다르게 작성하셨어도 결과만 재대로 나왔다면 좋습니다 :)