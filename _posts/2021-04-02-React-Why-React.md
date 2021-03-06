---
title: "리액트를 다루는 기술-1장-왜 리액트인가?"
categories:
  - JavaScript
tags:      
  - react 
toc: true    
toc_sticky: true
toc_label: "주요 목차"    
---

## 1.1.1 리액트 이해

> 리액트는 JS 라이브러리로 사용자 인터페이스를 만드는데 유용한 오직 V(View)만 신경쓰는 라이브러리

#### 자주 쓰이는 용어들
1) 컴포넌트: 특정 부분이 어떻게 생길지 정하는 선언체
- 재사용이 가능한 API 로 수많은 기능들을 내장
- 하나의 컴포넌트에서 해당 컴포넌트의 생김새와 작동 방식을 정의
2) 렌더링: 사용자 화면에 뷰를 보여주는 것
- 데이터가 변할 때마다 새롭게 리렌더링하면서 성능을 아끼고 최적의 사용자 경험을 제공
- **초기 렌더링**과 데이터 변경으로 인한 **리렌더링**의 이해

### 1.1.1.1 초기 렌더링
> "어떤 UI 관련 프레임워크, 라이브러리를 사용하든지 간에 맨 처음에 어떻게 보일지를 정하는 초기 렌더링이 필요하다"

#### `render` 함수
> "컴포넌트가 어떻게 생겼는지 정의하는 역할을 한다"

```
render() { ... }
```

- `html` 형식의 문자열을 반환하지 않고, 뷰가 어떻게 생겼고 어떻게 작동하는지에 대한 정보를 지닌 객체를 반환
- 컴포넌트 내부에는 또 다른 컴포넌트들이 들어갈 수 있음
- `render` 함수 실행 시 내부에 있는 컴포넌트들도 재귀적으로 렌더링
- 최상위 컴포넌트의 렌더링 작업이 끝나면 지니고 있는 정보들을 사용하여 HTML 마크업(markup)을 만들고, 우리가 정하는 실제 페이지의 DOM 요소 안에 주입 
<img width="661" alt="스크린샷 2021-04-02 오전 11 14 42" src="https://user-images.githubusercontent.com/70752848/113373001-d60c9300-93a4-11eb-8bf0-bdbebbe560a5.png">
  
> "문자열 형태의 HTML 코드를 생성한 후 특정 DOM에 해당 내용을 주입하면 이벤트가 적용된다"

### 1.1.1.2 조화 과정
> "리액트에서 뷰를 업데이트할 때는 업데이트 과정을 거친다라고 하기 보다는 조화 과정(reconciliation)을 거친다"

- 컴포넌트에서 데이터 변화가 있을 때 새로운 요소로 갈아 끼움
- 새로운 데이터를 가진 `render` 함수의 재호출
  + 결과를 곧바로 DOM에 반영하지 않고 이전 `render` 함수가 만든 컴포넌트 정보와 현재 컴포넌트 정보를 비교
<img width="961" alt="스크린샷 2021-04-02 오전 11 47 10" src="https://user-images.githubusercontent.com/70752848/113374883-2b4aa380-93a9-11eb-838c-8e77cdffbf2b.png">
  + JS를 사용하여 두 가지 뷰를 최소한의 연산으로 비교한 후, 둘의 차이를 알아내 최소한의 연산으로 DOM 트리를 업데이트
  
