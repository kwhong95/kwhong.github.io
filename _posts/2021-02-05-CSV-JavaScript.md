---
title: "CSV파일을 JS에서 활용하기"
categories: 
  - JavaScript
tags:
  - js
  - csv
last_modified_at: 2021-02-05T08:06:00 -0500
toc: true
toc_sticky: true
toc_label: "주요 목차"
---

## 1. CSV란 무엇인가?

<img width="173" alt="스크린샷 2021-02-05 오후 9 22 57" src="https://user-images.githubusercontent.com/70752848/107033221-53c67f00-67f8-11eb-9670-7ebe049c3f62.png">

필드와 필드 간의 데이터 요소들이 `,(콤마)` 형태로 구분되어 있는 파일 형태를 의미합니다. 위처럼 데이터를 콤마를 기준으로 나눠지고 있죠.

## 2. 목표

그리하여 저는 저 CSV 파일을 JS 언어로 읽어들이고 비동기 그래프를 그릴 예정입니다.

## 3. CSV 파일을 Js 배열로 반환하기

**파일구조**
```
root
 ├── node_modules
 ├── data.csv
 ├── csvLoader.js
 └── package.json
```

1. **Importing dependencies**

```
npm install fs csvtojson json2csv
```
일단 csv파일을 불러오기 위해 도움을 줄 위 3가지를 설치합니다.


```js
const fs = require('fs');
const csv = require('csvtojson');
const { Parser } = require('json2csv');
```

이렇게 `Importing`을 해주시고요.

2. csv를 불러올 함수 작성

```js
(async () => {

    // Load the data
    const data = await csv().fromFile('data.csv');

    // Show the data
    console.log(data);

})();
```
비동기 함수를 사용해서 실제 데이터가 로드되는지 확인할거구요.  
csv를 Json으로 로드하여 가져옵니다.
그럼 재대로 가져왔는지 확인합니다.
```
node csvLoader
```

<img width="462" alt="스크린샷 2021-02-05 오후 11 39 37" src="https://user-images.githubusercontent.com/70752848/107047676-6dbd8d00-680b-11eb-94d4-7729cb6d11af.png">

이렇게 CSV파일의 데이터들이 잘 출력되는 것을 확인했습니다!
참 쉽죠?