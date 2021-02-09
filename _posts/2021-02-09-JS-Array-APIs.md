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

### Q3. make this array look like this: [5, 4, 3, 2, 1]
```js
const array = [1, 2, 3, 4, 5];
```

### Q4. make new array without the first two elements
```js
const array = [1, 2, 3, 4, 5];
```

```js
class Student {
    constructor(name, age, enrolled, score) {
        this.name = name;
        this.age = age;
        this.enrolled = enrolled;
        this.score = score;
    }
}
const students = [
    new Student('A', 29, true, 45),
    new Student('B', 28, false, 80),
    new Student('C', 30, true, 90),
    new Student('D', 40, false, 66),
    new Student('E', 18, true, 88),
];
```
앞으로는 위의 클래스로 퀴즈를 풉니다.

### Q5. find a student with the score 90

## 3. Soluctions

### Q1
```js
const fruits = ['🍎', '🍌', '🍊'];
const result = fruits.join();
console.log(result); // 🍎,🍌,🍊
```
- **API : Join**  
- syntax : `join(separator?: string): string;`

### Q2
```js
const fruits = '🍎, 🍌, 🍊, 🍉';
const result = fruits.split(',');
console.log(result); // [ '🍎', ' 🍌', ' 🍊', ' 🍉' ]
```
- **API : Split**
- syntax : `split(separator: string | RegExp, limit?: number): string[];`

### Q3
```js
const array = [1, 2, 3, 4, 5];
const result = array.reverse();
console.log(result); // [ 5, 4, 3, 2, 1 ]
```
- **API : Reverse**
- syntax : `reverse(): T[];`
- 주의 사항: array 자체도 바뀝니다.

### Q4
```js
const array = [1, 2, 3, 4, 5];
const result = array.slice(2, 5);
console.log(array); // [1, 2, 3, 4, 5]
console.log(result); // [3, 4, 5]
```
- **API : Slice**
- syntax : `slice(start?: number, end?: number): T[];`

### Q5
```js
const result = students.find(student => student.score === 90);
console.log(result); // Student { name: 'C', age: 30, enrolled: true, score: 90 }
```
- **API : Find**
- syntax : `find<S extends T>(predicate: (this: void, value: T, index: number, obj: T[]) => value is S, thisArg?: any): S | undefined;`
