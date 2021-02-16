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
> HTML 축소하기 : HTML 코드를 최대한 축소하고 주석, 공백 및 새줄을 제거한다.

**왜?**  
> 불필요한 공간, 주석 및 속성을 모두 제거하면 HTML 크기가 줄어들고 사이트의 페이지로드 시간이 빨라지며 사용자의 다운로드 속도가 분명히 줄어 듭니다.

**어떻게?**  
> 대부분의 프레임 워크에는 웹 페이지 축소를 용이하게하는 플러그인이 있습니다. 자동으로 작업을 수행 할 수있는 NPM 모듈을 사용할 수 있습니다. 

- 🎁[HTML 축소 | 코드 축소](http://minifycode.com/html-minifier/)
- 🎁[온라인 HTML | CSS | JS 압축기](https://refresh-sf.com/)


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

- 🔍[페이지 로드 속도 향상을 위한 `style & script` 가이드](https://www.internetmarketingninjas.com/tools/free-tools/pagespeed)

### 1.2 iframe 수 최소화
> 다른 기술 도입의 가능성이 없는 경우에만 **iframe**을 사용합니다. 가능한 **iframe**을 피할것!

**왜?**  
> iframe은 따지고 보면 장점도 많은 친구이지만 성능을 다른 기술보단 성능이 떨어지는 것임을 알고 있어야합니다. **iframe의 장점과 단점**을 알아보죠

**장점 & 단점**

*`<iframe>`의 장점*  
- 광고나 뱃지 같은 로딩이 느린 third-party-content 대체
- Security sandox
- Script 병렬 다운로드  

*`<iframe>`의 단점*
- 비어있어도 성능을 많이 잡아먹는다
- page onload를 차단
- 비의미론적인 마크업(Non-semantic)

## 2. CSS
> 모든 CSS 파일을 축소하고 주석,공백을 제거하라

**왜?**
> CSS 파일이 축소되면 콘텐츠가 더 빠르게로드되고 더 적은 데이터가 클라이언트로 전송됩니다. 프로덕션에서 항상 CSS 파일을 축소하는 것이 중요합니다. 대역폭 비용을 낮추고 리소스 사용량을 낮추려는 모든 비즈니스에 유용하며 사용자에게 유용합니다.

**어떻게?**
> 도구를 사용하여 빌드 또는 배포 전에나 배포 중에 파일을 자동으로 축소합니다.

- 🎁[CSSnano](https://cssnano.co/): CSS를 많은 최적화를 통해 실행하여 최종 결과가 배포 환경에서 가능한 작도록 실행
- 🎁[CSS Minifier](https://goonlinetools.com/css-minifier/)


### 2.1 CSS 파일 로드시 DOM 로드 차단 방지
> CSS 파일은 DOM이로드되는 데 시간이 걸리는 것을 방지하기 위해 로드 차단을 방지합니다.
```html
<link  rel = " preload " href = " global.min.css " as = " style " onload = " this.rel = 'stylesheet' "> 
<noscript > <link  rel = " stylesheet " href = " global.min. css " > </noscript >
```
**왜?**
> CSS 파일은 페이지로드를 차단하고 페이지 렌더링을 지연시킬 수 있습니다. **preload** 를 사용하면 브라우저가 페이지의 내용을 표시하기 시작하기 전에 실제로 CSS 파일을 로드 할 수 있습니다.

**어떻게?**
> `rel`속성에 **preload**를 추가하고 `as="style"` 를 `<link>`요소에 추가 해야합니다 .
- 🎁[필라멘트 그룹별 loadCSS](https://github.com/filamentgroup/loadCSS)
- 🔍[PreLoad CSS 예시](https://gist.github.com/thedaviddias/c24763b82b9991e53928e66a0bafc9bf)

### 2.2 Critical CSS
> 중요한 CSS(스크롤 없이 보이는 부분)는 페이지의 보이는 부분을 렌더링하는데 사용되는데 사용하는 모든 CSS를 의미합니다. 주요 CSS 호출 이전과 그사이에  `<style>` 태그에 한 줄로 삽입합니다(가능한 경우 축소 가능).

**왜?**
> 중요한 CSS를 인라인하면 웹 페이지의 렌더링 속도를 높이고 서버에 대한 요청 수를 줄일 수 있습니다.

**어떻게?**
> 온라인 도구 또는 Addy Osmani가 개발한 플러그인을 사용하여 중요한 CSS를 (따로)생성합니다.

- 🔍[Critical CSS의 이해](https://www.smashingmagazine.com/2015/08/understanding-critical-css/)
- 🎁[Addy Osmani의 Critical-path CSS 추출 및 인라인화](https://github.com/addyosmani/critical)

### 2.3 임베디드 또는 인라인 CSS 사용하지 않기
> HTTP/2 에는 유효하지 않습니다.

**왜?**
> 첫 번째 이유 중 하나는 콘텐츠와 디자인 을 분리 하는 것이 좋은 습관이기 때문 입니다. 또한 유지 관리가 용이 ​​한 코드를 확보하고 사이트에 액세스 할 수 있도록 유지하는 데 도움이됩니다. 그러나 성능과 관련하여 HTML 페이지의 파일 크기와로드 시간이 줄어들 기 때문입니다.

**어떻게?**
> 항상 외부 스타일 시트를 사용하거나 CSS를 `<head>`에 포함합니다(다른 CSS 성능 규칙을 따릅니다).

- 📋[CSS 모범 사례 : CSS 인라인 스타일 피하기](https://www.lifewire.com/avoid-inline-styles-for-css-3466846)

### 2.4 스타일 시트 복잡성 분석하기
> 스타일 시트를 분석하면 문제, 중복 및 중복 CSS 선택기에 플래그를 지정하는 데 도움이 될 수 있습니다.

**왜?**
> 때로는 CSS에 중복 또는 유효성 검사 오류가있을 수 있으며, CSS 파일을 분석하고 이러한 복잡성을 제거하면 CSS 파일 속도를 높이는 데 도움이 될 수 있습니다 (브라우저에서 더 빨리 읽을 수 있기 때문).

**어떻게?**
> CSS 전처리기를 사용하여 CSS를 구성해야합니다. 아래 나열된 일부 온라인 도구는 코드를 분석하고 수정하는데도 도움이 될 수 있습니다.

- 🎁[TesyMyCSS | CSS 성능 최적화 및 확인](https://www.testmycss.com/)
- 🎁[CSS Stats](https://cssstats.com/)
- 🎁[Macbre의 analyze-css: CSS 선택기 복잡성 및 성능 분석](https://github.com/macbre/analyze-css)
- 🎁[WALLACE](https://www.projectwallace.com/) 는 CSS를 시간이 지남에 따라 통계를 저장하므로 변경사항을 추적할 수 있습니다.

## 3. 이미지

### 3.1 이미지 최적화
> 이미지 최적화 : 사용자에게 직접적인 영향을 주지 않고 이미지가 최적화하고 압축시킨다.

**왜?**
> 최적화 된 이미지는 브라우저에서 더 빨리로드되고 더 적은 데이터를 소비합니다.

**어떻게?**
> 가능하면 CSS3 효과를 사용하세요(작은 이미지 대체).  
가능하면 이미지에 인코딩 된 텍스트 대신 글꼴을 사용하세요.  
SVG 사용: 도구를 사용하고 85 미만의 수준 압축을 지정하세요.

- 🔍[이미지 최적화 | 웹 기초 | Google 개발자](https://web.dev/fast/#optimize-your-images)
- 🎁[TinyJPG - 지능적 JPEG 이미지 압축](https://tinyjpg.com/)
- 🎁[Kraken.io - 온라인 이미지 최적화 도구](https://kraken.io/web-interface)
- 🎁[Compressor.io - JPEG 사진 및 PNG 이미지 최적화 및 압축](https://compressor.io/)
- 🎁[Cloudinary - 이미지 분석 도구](https://webspeedtest.cloudinary.com/)
- 🎁[ImageEngine - 이미지 웹 페이지 로딩 테스트](https://demo.imgeng.in/#!/)
- 🎁[SVGOMG-SVG 벡터 그래픽 파일 최적화](https://jakearchibald.github.io/svgomg/)

### 3.2 이미지 형식을 적절하게 선택하기
**왜?**
> 이미지로 인해 웹 사이트 속도가 느려지지 않도록 이미지에 해당하는 형식을 선택하세요. 사진 인 경우 JPEG는 대부분 PNG 또는 GIF보다 더 적합합니다. 그러나 파일 크기를 줄일 수있는 nex-gen 형식을 찾는 것을 잊지 마시구요. 각 이미지 형식에는 장단점이 있습니다. 가능한 최선의 선택을하려면 이를 아는 것이 중요합니다.

**어떻게?**
> [Lighthouse](https://developers.google.com/web/tools/lighthouse/)를 사용하여 궁극적으로 차세대 형식(예 : JPEG 2000m JPEG XR 또는 WebP)을 사용할 수 있는 이미지를 식별합니다.  
다른 형식을 비교하고 PNG8 이 PNG16보단 낫지만 그렇지 않을 수도 있습니다.

- 🔍[차세대 형식의 이미지 제공 | 웹 개발자를 위한 도구 | Google 개발자](https://web.dev/uses-webp-images/)
- 🔍[웹 사이트에 적합한 이미지 형식은 무엇일까?](https://www.sitepoint.com/what-is-the-right-image-format-for-your-website/)
- 🔍[PNG8-The Clear Winner](https://www.sitepoint.com/png8-the-clear-winner/)
- 🔍[8비트 vs 16비트 - 사용해야 하는 색 농도가 중요한 이유](https://www.diyphotography.net/8-bit-vs-16-bit-color-depth-use-matters/)

## 4. JavaScript

### 4.1 JS 최적화
>  모든 JavaScript 파일를 축소하고 주석, 공백 및 새 줄이 프로덕션 파일에서 제거합니다 (HTTP / 2를 사용하는 경우에도 유효 함).

**왜?**
> 불필요한 공백, 주석 및 중단을 모두 제거하면 JavaScript 파일의 크기가 줄어들고 사이트의 페이지로드 시간이 빨라지고 사용자의 다운로드 속도가 분명히 줄어 듭니다.

**어떻게?**
> 아래 제안된 선물들을 사용하여 빌드 또는 배포 전이나 배포 중에 파일을 자동으로 축소합니다.

- 🎁[Uglify-js-npm](https://www.npmjs.com/package/uglify-js)
- 🎁[온라인 JS 압축기](https://refresh-sf.com/)
- 🔍[HTTP/2 의 차이점 | 여전히 축소 후 연결해야하는가?](https://scaleyourcode.com/blog/article/28)

### 4.2 JS 차단 방지
> JavaScript 파일은 속성을 `async`사용하여 비동기식으로 로드 되거나 `defer`를 통해 지연됩니다.

```html
<!--지연 속성--> 
<script  defer  src = " foo.js "> </script>

<!--비동기 속성--> 
<script  async  src = " foo.js "> </ script>
```

**왜?**
> 자바 스크립트는 HTML 문서의 일반적인 구문 분석을 차단하므로 파서가 `<script>`태그 (특히 `<head>` 내부에 있음 )에 도달하면 가져 오기 및 실행을 중지합니다. 스크립트가 페이지 상단에 배치되는 경우 추가 `async`하거나 `defer`를 적극 권장하지만 `</body>`태그 바로 앞에있는 경우 가치가 떨어 집니다. 그러나 성능 문제를 피하기 위해 항상 이러한 속성을 사용하는 것이 좋습니다.

**어떻게?**
> 스크립트 태그에 속성으로 추가 `async`(스크립트가 다른 스크립트에 의존하지 않는 경우) 또는 `defer`(스크립트가 비동기 스크립트에 의존하는 경우).  
작은 스크립트가 있는 경우 비동기 스크립트 위에 인라인 스크립트 위치를 사용할 수 있습니다.

- 🔍[렌더링 차단 JS 제거](https://developers.google.com/speed/docs/insights/BlockingJS)
- 🎁[JS 로딩 연기](https://www.internetmarketingninjas.com/tools/free-tools/pagespeed)

## 5. 서버
### 5.1 HTTPS의 장점(를 사용하자!)

**왜?**
> HTTPS는 전자 상거래 웹 사이트뿐만 아니라 데이터를 교환하는 모든 웹 사이트를위한 것입니다. 사용자가 공유 한 데이터 또는 외부 엔터티와 공유 된 데이터입니다. 오늘날 최신 브라우저는 안전하지 않은 사이트의 기능을 제한합니다. (예 : 인스턴스가 HTTPS를 사용하지 않는 경우 지리적 위치, 푸시 알림 및 서비스 워커가 작동하지 않습니다.) 그리고 오늘날은 이전보다 SSL 인증서로 프로젝트를 설정하는 것이 훨씬 더 쉽습니다 (그리고 Let 's Encrypt 덕분에 무료로 제공 ).

- 🔍[HTTPS를 사용하는 이유 | Cloudflare](https://www.cloudflare.com/learning/ssl/why-use-https/)
- 🔍[웹 성능 저하 없이 HTTPS 활성화 | Moz](https://moz.com/blog/enabling-https-without-sacrificing-web-performance)
- 🔍[HTTPS가 웹 사이트 성능에 미치는 영향](https://wp-rocket.me/blog/https-affects-website-performance/)
- 🔍[HTTP vs HTTPS vs HTTP2 - 실제 사례](https://www.tunetheweb.com/blog/http-versus-https-versus-http2/)
- 🔍[HTTP vs HTTPS - 둘다 직접 테스트](https://www.httpvshttps.com/)

### 5.2 웹페이지 크기를 최소화하기
> 최소 1500 KB 미만, 이상적 크기는 500 KB 미만이며, 리소스를 최대한 줄이세요.

**왜?**
> 500KB 단위로 표시됩니다 웹의 상태에 따라 킬로바이트의 중앙값이 1500KB 표시됩니다. (모바일 그렇습니다.) 최상의 사용자 경험을 제공 할 때마다 사용자, 네트워크 연결, 디바이스에 최대한 많이야합니다.

**어떻게?**
> 프론트 엔드 성능 체크리스트의 모든 규칙은 리소스와 코드를 최대한 줄이도록하고 있습니다.

- 🔍[페이지의 무게](https://httparchive.org/reports/page-weight#bytesTotal)
- 🎁[내 사이트는 얼마일까?](https://whatdoesmysitecost.com/)
- 🎁[web-Chrome DevTools에서 전체 페이지 크기 측정 - 스택 오버플로](https://stackoverflow.com/questions/38239980/measure-full-page-size-in-chrome-devtools)

### 5.3 페이지 로드시간 단축하기
> 이상적 시간은 3초 이내이며, 당연히 사용자에게 빠르게 콘텐츠가 전송되어야 합니다.

**왜?**
> 웹 사이트나 앱이 빨라질수록 많은 사용자의 바운스 증가합니다. 한편 전송이 느리다면 현 사용자나 미래의 사용자를 잃을 가능성도 있습니다. 이것은 주제에 대한 많은 연구가치를 증명합니다.

**어떻게?**
> Page Speed ​​Insight 또는 WebPageTest 와 같은 온라인 툴을 이용해 무엇이 페이지를 느리게 만드는지 분석하고, 프론트엔드 체크리스트를 이용해 로드 시간을 개선하세요.

- 🎁[모바일 사이트 속도 비교](https://www.thinkwithgoogle.com/feature/testmysite/)
- 🎁[모바일 웹 사이트 속도 및 성능 테스트](https://www.thinkwithgoogle.com/feature/testmysite/)
- 🔍[2018년 평균 페이지 로드 시간 - 비교해보면 당신은 어떤가요?](https://www.thinkwithgoogle.com/feature/testmysite/)

### 5.4 TTFB 시간을 줄이기
> TTFB란 서버에 HTTP 요청을 보내고 브라우저가 첫 정보를 수신하기까지 걸리는 시간을 의미합니다. 1.3초 이내로 가능하도록 노력해봅시다.

- 🔍[TTFB(Time to First Byte)](https://www.internetmarketingninjas.com/tools/free-tools/pagespeed)
- 🎁[글로벌 지연 테스트 도구](https://latency.apex.sh/)

### 5.5 쿠키의 크기 조절하기
> 만약 쿠키를 사용한다면 각 쿠키가 4096 바이트를 넘으면 안되며, 도메인이 20개 이상의 쿠키를 가져가선 안됩니다.

**왜?**
> 쿠키는 HTTP 헤더에서 웹 서버와 브라우저 사이에 교환됩니다. 사용자의 응답 시간에 제한적으로 사용하기 쉽습니다.

**어떻게?**
>불필요한 쿠키를 제거하세요.

- 🔍[쿠키](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)
- 🔍[웹 사이트 성능: 쿠키는 맛이 좋지 않습니다](https://www.monitis.com/blog/website-performance-cookies-dont-taste-so-good/)
- 🔍[Google의 웹 성능 모범 사례 #3: 요청 오버 헤드 최소화](https://www.globaldots.com/blog/googles-web-performance-best-practices-3-minimize-request-overhead)

### 5.6 HTTP 요청 최소화
> 항상 모든 파일의 요청이 웹사이트나 어플리케이션에 필수 인지 확인하세요.

- 🔍[외부 CSS 결합](https://www.internetmarketingninjas.com/tools/free-tools/pagespeed)
- 🔍[외부 JS 결합](https://www.internetmarketingninjas.com/tools/free-tools/pagespeed)

### 5.7 동일한 프로토콜에서 파일 제공
> 예를들어 HTTPS를 사용하는 웹사이트에서 HTTP를 사용하여 소스에서 가져오는 파일을 제공하는 웹사이트를 피하세요. 웹사이트에서 HTTPS를 사용하는 경우 외부파일은 동일한 프로토콜에서 가져와야 합니다.

### 5.8 연결 가능한 파일 제공
> 연결 불가능 즉 404 요청을 하지 마세요

- 🔍[잘못된 요청을 피하는 방법](https://www.internetmarketingninjas.com/tools/free-tools/pagespeed)

### 5.9 올바른 HTTP 캐시 헤더 설정
> 브라우저와 서버 사이 비용이 큰 왕복을 피하도록 HTTP 헤더를 설정하세요.

- 🔍[브라우저 캐싱에 캐시 제어 사용](https://www.internetmarketingninjas.com/tools/free-tools/pagespeed)

### 5.10 GZIP | Brotli 압축 활성화
> Gzip 또는 Brotli와 같은 압축 방법을 사용하여 JS파일의 크기를 줄이세요. 더 작은 파일을 사용할수록 사용자가 더 빠르게 소스를 다운받을 수 있으므로 성능이 향상됩니다.

- 🎁[무료 GZIP 압축 체커](https://www.websiteplanet.com/ko/webtools/gzip-compression/)
- 🔍[사이트 속도 개선 - Brotli 압축으로 속도 개선해보기](https://happist.com/561373/%EC%82%AC%EC%9D%B4%ED%8A%B8-%EC%86%8D%EB%8F%84-%EA%B0%9C%EC%84%A0-%EB%B8%8C%EB%A1%9C%ED%8B%80%EB%A6%AC-%EC%95%95%EC%B6%95brotli-compression%EC%9C%BC%EB%A1%9C-%EC%86%8D%EB%8F%84%EB%A5%BC-%EA%B0%9C)
- 🔍[CAN I USE..?](https://caniuse.com/brotli)

