---
title: "JS 데이터 타입"
categories: 
  - JavaScript
tags:
  - js
  - data
  - type
toc: true
toc_sticky: true
toc_label: "주요 목차"
---

# {{ page.title }}
> 프로그래밍 언어에서 가장 중요한것은 입력, 연산, 출력이라고 생각합니다.  
사용자들에게 정보를 전달하기 위해서는 위 3가지를 빼놓을 수 없기 때문인데요.  
CPU에 최적화된 연산, 메모리 사용을 최소화하는 것 또한 포인트가 됩니다 :)

## 1. Variable - Mutable
> 변수란? 변경될 수 있는 값을 의미합니다.

JS에서 변수를 선언 할 때는 `let`이라는 키워드를 사용합니다.(ES6에서 추가됨)

```js
let name = 'kwhong';
console.log(name); // kwhong
name = 'hello';
cosole.log(name); // hello
```

이렇게 변수를 선언하고 값을 할당한 뒤 다시 변수에 다른 값을 할당하고 출력하는 것을 해보았는데요 프로그램 입장에서 어떻게 된것인지 살펴보겠습니다.  
 
<img width="507" alt="스크린샷 2021-02-06 오후 5 01 53" src="https://user-images.githubusercontent.com/70752848/107112721-06501d80-689d-11eb-8095-a54564b2ccdc.png">

어플리케이션이 실행되면 어플리케이션마다 사용 가능한 **메모리**가 할당됩니다.
이 메모리는 제한적으로 할당이 되어집니다. 메모리에 변수 값이 할당되고 이를 가르키는 변수명이 있는 것이죠.

## 2. Block scope
> `{}(중괄호)`를 이용해서 Block Scope을 설정합니다.

```js
let globalName = 'global name';
{
  let name = 'kwhong';
  console.log(name); // kwhong
  name = 'hello';
  console.log(name); // hello
  console.log(globalName); //global name
}
console.log(name); // name is not defined!
console.log(globalName); // global name
```

Block Scope로 코드를 작성하면, Block 밖에서는 안의 코드를 알수 없게 됩니다.  
여기서 중요한 점은 global 변수는 항상 메모리에 참조되어있기 떄문에 많이 사용할 경우 메모리를 많이 잡아먹게 되고 성능이 떨어집니다. 그래서 if, for 같은 필요한 루프에서만 사용하는 것이 좋습니다.

## 3. var 사용하지마!
ES6 이후 let이 출범하면서 var는 사용하지 않는 것을 권장하고 있습니다.
```js 
// var (사용하지 말자...)
// var hoisting
console.log(age); // undefined
age = 4;
console.log(age); // 4
var age;
```
보시면 다른 언어입장에선 조금 미친짓이라고 생각이 드는데요.  
변수를 선언 및 할당하기 전에 출력이 가능하고 선언전에 할당해도 값이 출력이 됩니다...  
이것은 바로 var의 **호이스팅** 때문입니다. 호이스팅이란 어느곳에 선언해도 가장 위로 끌어올려주는 기능을 하는것인데요.  
 그래서 var를 사용하지 말자는 개발자들이 많은 목소리를 내고 있습니다.

**var의 단점**
1. 호이스팅으로 인해 변수가 자동으로 Global 변수로 할당된다.
2. Block Scope를 무시한다.

이것들로 인해 **var**는 어느정도의 규모 이상의 프로젝트에서 버그의 원흉이 됩니다. 선언하지도 않은 변수가 출력되는 등 여러가지 이슈들이 생기는 위험이 생길 수 있죠.


## 4. Constant - Immutable
```js
const dayInWeek = 7;
const maxNumber = 5;
```
**Const**는 할당하고 절대 바꿀수 없는 값을 의미합니다.  
이는 개발자들이 선호는 데이터 타입입니다. 이유는 3가지가 있습니다.
1. **보안**  
값을 변경할 수 없기에 외부에서 데이터를 변경하는 것을 방지할 수 있습니다.
2. **안정적인 프로세스**  
프로세스 안의 쓰레드들이 동시에 값에 접근하여 데이터를 변경할 수 있는데 동시에 값을 변경한다는 점은 위험할 수 있습니다. 그래서 그것을 방지하여 안정적인 프로세스를 구축할 수 있습니다.
3. **개발자의 실수 방지**  

## 5. Variable Types

### 1. Primitive - single
> 변수 타입중 가장 작은 타입

#### 1-1. number
```js
const count = 17; //integer
const size = 17.1 // decimal number
console.log(`value ${count}, type: ${typeof count}`);
// value : 17, type: number
console.log(`value ${size}, type: ${typeof size}`);
// value: 17.1 type: number
```
JS에서는 모든 실수, 정수들이 number 타입으로 정의됩니다. :)

```js 
const infinity = 1 / 0;
const negativeInfinity = -1 / 0;
const nAn = 'not a number' / 2;
console.log(infinity)
console.log(negativeInfinity)
console.log(nAn)
```
특수한 숫자 타입도 존재합니다. 

#### 1-2. string 
```js
const char = 'c';
const hong = 'Hong';
const greeting = 'hello' + hong;
console.log(`value: ${greeting}, type: ${typeof greeting}`);
// value: hello hong, type: string
const helloBob = `hi ${hong}!`; // template literals(string)
console.log(`value: ${helloBob}, type: ${typeof helloBob}`);
// value: hi hong!, type: string
```
위에서는 string 타입을 알아보았는데요. 특이한 점은 **+** 기호로 문자열을 합칠 수 있다는 점과 template literal을 통해서 `${}`안에 변수를 넣을 수 있습니다.  

#### 1-3. boolean
```js
const canRead = true;
const test = 3 < 1; // false
console.log(`value: ${canRead}, type: ${typeof canRead}`);
// value: true, type: boolean
console.log(`value: ${test}, type: ${typeof test}`);
// value: false, type: boolean
```
boolean 타입입니다. 참과 거짓을 표현하고 추후에는 boolean 타입으로 로직을 구성하는 경우가 많이 있고 간단하지만 굉장히 중요한 타입입니다.

#### 1-4 null & undefined
```js
let nothing = null;
console.log(`value: ${nothing}, type: ${typeof nothing}`);
// value: null, type: object

let x;
console.log(`value: ${x}, type: ${typeof x}`);
// value: undefined, type: undefined
```
두개의 차이가 느껴지시나요?  
보통 `null`은 변수에 빈공간 즉, 아무런 값도 넣지 않는다고 선언한 것이고  
`undefined`는 변수를 선언했는데 아무 값도 할당 되지 않은 것입니다.

## 1-5 symbol
```js
const symbol1 = Symbol('id');
const symbol2 = Symbol('id');
console.log(symbol1 === symbol2) // false
const gSymbol1 = Symbol.for('id');
const gSymbol2 = Symbol.for('id');
console.log(gSymbol1 === gSymbol2) // true
console.log(`value: ${symbol1}, type: ${typeof symbol1}`);
// TypeError: Cannot convert a Symbol value to a string
console.log(`value: ${symbol1.description}, type: ${typeof symbol1}`);
// value: id, type: symbol
```
`symbol`은 고유한 식별자를 선언할 때 사용합니다.  
보시다시피 똑같이 선언된 Symbol이지만 두 값을 비교했을 땐 다르다는 결과가 나옵니다. 
만약 같은 Symbol로 선언해주고 싶다면 `Symbol.for`를 사용하시면 되고  
값을 출력하기 위해선 `description`을 붙혀주셔야 합니다.


### 2. Object - box container
> 가장 변수들의 집합 

### 3. Function - first-class function
> JS에서는 함수 또한 데이터 타입 중 하나입니다. 즉, 함수도 변수에 할당하여 사용이 가능하고 함수의 파라미터로 전달이 가능하며, 함수의 리턴 타입으로 함수를 리턴할 수 있습니다.(first-class function)
