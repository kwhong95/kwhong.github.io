---
title: "데이터 시각화의 기본"
categories: 
  - Data Visualization
tags:
  - data-visualization
  - chapter1
last_modified_at: 2021-02-05T08:06:00 -0500
toc: true
toc_sticky: true
toc_label: "주요 목차"
---

# Chapter1. 데이터 시각화의 기본
학습 목표
1. 데이터 시각화란?
2. 제시한 데이터에 관한 대시보드 설계
3. 데이터 시각화 기본의 정리와 요약

## 1. 데이터를 시각화하는 이유
**숫자의 시각화**가 왜 중요할까?

<img width="721" alt="스크린샷 2021-02-05 오후 5 59 23" src="https://user-images.githubusercontent.com/70752848/107012219-15bb6200-67dc-11eb-8e73-1f80d85b9be8.png">

위의 표를 보면 각 숫자가 무엇을 의미하는지, 숫자의 패턴과 추세의 차이를 구별할 수 있으신가요?

저는 전혀 모르겠습니다... 심지어 소수점자리까지 의식하니 굉장히 어렵게만 느껴집니다.

이번엔 이 표를 차트화해서 파악해보도록 합시다.

<img width="300" alt="스크린샷 2021-02-05 오후 8 21 11" src="https://user-images.githubusercontent.com/70752848/107027612-b9623d80-67ef-11eb-97c9-df5a3fcef256.png"> |<img width="300" alt="스크린샷 2021-02-05 오후 8 33 41" src="https://user-images.githubusercontent.com/70752848/107028835-70ab8400-67f1-11eb-8c8f-0995ae137561.png">
:---:|:---:
<img width="300" alt="스크린샷 2021-02-05 오후 8 38 05" src="https://user-images.githubusercontent.com/70752848/107029238-0e06b800-67f2-11eb-87f8-8059c6d0f454.png"> | <img width="300" alt="스크린샷 2021-02-05 오후 8 40 43" src="https://user-images.githubusercontent.com/70752848/107029476-6b9b0480-67f2-11eb-86ea-725195bf049d.png">

> 그래프는 Google Chart를 활용하여 JS 언어로 만들었습니다.

차이가 느껴지시나요? 숫자를 차트로 옮겨서 보면 표와 같은 통계적 지표로는 알수 없는 것들이 보이기 시작합니다. 바로 데이터를 시각화하고 시각의 힘에 의존하면, 우리가 직접 보면서 느낄 수 있는 관계와 추세같은 것들이 보이기 시작합니다.

**매출의 동향이 어떠한가**

<img width="852" alt="스크린샷 2021-02-05 오후 9 10 24" src="https://user-images.githubusercontent.com/70752848/107032090-938c6700-67f6-11eb-87d8-f4ce2ba690e1.png">

다음은 주요 유통업체 오프라인 13개사, 온라인 13개사 및 전체 26개사 전년 동월 대비 식품군 매출액 성장률으로 우리나라 산업통상자원부에서 발표한 CSV 파일 형식입니다. 역시 표로 데이터를 표현하니 가독성도 떨어지고 성장률이 눈에 보이기는 하지만 정확한 추이를 보기 힘듭니다. 그렇다면 **라인 그래프**로 표현해보면 어떨까요? 