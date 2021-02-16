---
title: "프론트엔드 성능 체크리스트"
categories: 
  - Front-End-Skills
tags:
  - front-end
  - performance
  - checklist
toc: true
toc_sticky: true
toc_label: "주요 목차"
---

참고 자료 : [Front-End-Performance-Checklist](https://github.com/thedaviddias/Front-End-Performance-Checklist#html) - David Dias

# 프론트 엔드 성능 체크리스트 - 요약본
> 다른 웹보다 빠르게 실행되는 유일한 프론트 엔드 성능 검사 목록!  
목표 : "성능을 염두에 두고 설계와 코딩을 하자"

웹 페이지를 제작함에 있어 성능은 큰 주제이며 항상 "백엔드" 또는 "관리자"만의 책임은 아니며, 프론트 엔드의 책임 또한 크게 작용합니다. 나날이 발전하는 새로운 기술들 속에서도 진정한 프론트엔드로 살아남기 위해서는 성능 체크에 대해서 최소한 알고 있어야하고 프로젝트에 적용하는 방법을 숙지하고 있어야 합니다.  

참고 문헌에서 **우선 순위**가 높은 것들로만 구성하였습니다.  
더 세심한 성능 체크를 하고싶으시다면 위 참고자료에서 더욱 많은 자료를 얻으실 수 있습니다.

## 1. HTML
### 1.1 JS 태그 앞에 항상 CSS 태그 배치
> JavaScript 코드를 사용하기 전에 CSS가 항상로드되었는지 확인합니다.

```html
<!-- 👎 --> 
<script  src = " jquery.js "> </script> 
<script  src = " foo.js "> </script> 
<link  rel = " stylesheet " href = " foo.css "/>

<!-- 👍🏻 --> 
<link  rel = " stylesheet " href = " foo.css "/>
<script  src = " jquery.js "> </script> 
<script  src = " foo.js "> </script>
```

**왜?**  
> JavaScript 앞에 CSS 태그가 있으면 더 나은 **병렬 다운로드**가 가능하여 브라우저 **렌더링 시간이 단축**됩니다.


**어떻게?**
> head안에 존재하는 `<link>` & `<style>` 태그를 `<script>` 태그 위에 배치한다.

- [페이지 로드 속도 향상을 위한 `style & script` 가이드](https://www.internetmarketingninjas.com/tools/free-tools/pagespeed)

### 1.2 iframe 수 최소화
> 다른 기술 도입의 가능성이 없는 경우에만 **iframe**을 사용합니다. 가능한 **iframe**을 피할것!

**왜?**  
> iframe은 따지고 보면 장점도 많은 친구이지만 성능을 다른 기술보단 성능이 떨어지는 것임을 알고 있어야합니다. **iframe의 장점과 단점**을 알아보죠

**장점 & 단점**
*<iframe>의 장점*  
- 광고나 뱃지 같은 로딩이 느린 third-party-content
- Security sandox
- Script 병렬 다운로드  

*<iframe>의 단점*
- 비어있어도 성능을 많이 잡아먹는다
- page onload를 차단
- 비의미론적인 마크업(Non-semantic)