---
title: "JS - ArrayAPIs"
categories: 
  - JavaScript
tags:
  - js
  - array
  - APIs
toc: true
toc_sticky: true
toc_label: "주요 목차"
---

# {{ page.title }}

> 10가지 Quiz를 통해서 배열의 API들을 활용해봅시다!

## 1. 내가 생각한 유용한 Array APIs 정리
### 1. Slice
```js
const fruits = ['🍎', '🍌', '🍊'];
    console.log(fruits.slice());
    console.log(fruits.slice(start = 1, end = 2));
    // ['🍎', '🍌', '🍊']
    // ['🍌']
```

배열을 복사하는 개념, 시작과 (끝 -1) 지점을 정할 수 있습니다.

### 2. Join
```js
console.log(fruits.join('/')); // 🍎/🍌/🍊
```
배열의 모든 요소를 문자열로 합칩니다. with 구분자!

### 3. Every
```js
const isInApple = () => fruits.includes('🍎');

console.log(fruits.every(isInApple)); // true
```
`every()` 메서드는 배열 안의 모든 요소가 주어진 판별 함수를 통과하는지 테스트합니다.

### 4. Map
```js
const fruitsColorRed = fruits.map(fruit => 'red' + fruit);
console.log(fruitsColorRed); // [ 'red🍎', 'red🍌', 'red🍊' ]

```
`map()` 메서드는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환합니다.

### 5. Filter
```js
const result = fruits.filter(fruit => fruit === '🍌');
console.log(result); // [ '🍌' ]
```
`filter()` 메서드는 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환합니다.

### 6. Reduce
```js
const reducer = (assemble ,fruit) => assemble + fruit;
console.log(fruits.reduce(reducer)); // 🍎🍌🍊
```
`reduce()` 메서드는 배열의 각 요소에 대해 주어진 **리듀서(reducer)** 함수를 실행하고, 하나의 결과값을 반환합니다.

## 2. Quizs

### Q1. make a string out of an array
```js
const fruits = ['🍎', '🍌', '🍊'];
```

### Q2. make an array out of a string
```js
const fruits = '🍎, 🍌, 🍊, 🍉';
```

## 3. Soluctions

### Q1
```js
const fruits = ['🍎', '🍌', '🍊'];
const result = fruits.join();
console.log(result);
```
- **API : Join**  
- syntax : `join(separator?: string): string;`

### Q2
```js
const fruits = '🍎, 🍌, 🍊, 🍉';
const result = fruits.split(',');
console.log(result);
```
- **API : Split**
- syntax : `split(separator: string | RegExp, limit?: number): string[];`