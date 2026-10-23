---
order: 47
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22aeda9b-0fe1-8035-b9ba-ed483053a3f6
title: "[ 의문점 ] pnpm 사용 이유"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22aeda9b-0fe1-8035-b9ba-ed483053a3f6
    title: "[ 의문점 ] pnpm 사용 이유"
excerpt: "목차 - pnpm: 현대 JavaScript 프로젝트를 위한 필수 선택 - 차이점 1) 패키지 Scope - 차이점 2) 패키지 구조 - 플랫, 비-플랫 - pnpm 장점 - 정리 pnpm: 현대 JavaScript 프로젝트를 위한 필수 선택 --- 📖 JavaScript 생태계에서 의존성 관리는 프로젝트의 안정성과 개"
cover: null
icon: 🧐
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-08T06:37:40.973Z
updated: 2025-07-10T04:08:46.406Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/[ 의문점 ] pnpm 사용 이유-ed483053a3f6/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22aeda9b0fe18035b9baed483053a3f6
---
> 
> 
> <a id="22aeda9b0fe180ba9968fd22bb0b3e7b"></a>
> 
> <strong>목차</strong>
> 
> - [ pnpm: 현대 JavaScript 프로젝트를 위한 필수 선택](#22aeda9b0fe1801c904beb51b498dbc9)
> - [차이점 1)  패키지 Scope ](#22aeda9b0fe18079b72bcfcc8838e2d0)
> - [차이점 2) 패키지 구조 - 플랫, 비-플랫](#22aeda9b0fe180af91fee3f52ab35a08)
> - [pnpm 장점](#22aeda9b0fe180e1b7b9c0637a719c4b)
> - [정리](#22aeda9b0fe180e49997de753caf7440)

<a id="22aeda9b0fe1801c904beb51b498dbc9"></a>

##  <code>pnpm</code>&#58; 현대 JavaScript 프로젝트를 위한 필수 선택

---

> 📖 
> 
> <a id="22aeda9b0fe1809ca582cdc424fe7fa7"></a>
> 
> JavaScript 생태계에서 의존성 관리는 프로젝트의 안정성과 개발 효율성을 좌우하는 핵심 요소이다&#46; 
> 
> <a id="22aeda9b0fe18066b171f4c9362b1c25"></a>
> 
> 특히 <code>Next&#46;js</code>와 같이 복잡하고 규모 있는 프레임워크를 다룰 때, 어떤 패키지 매니저를 선택하는가는 단순한 취향의 문제를 넘어선다&#46; 
> 
> <a id="22aeda9b0fe18061900fff3c9692c21e"></a>
> 
> 이러한 맥락에서 <code>pnpm</code>은 <strong><u>기존 npm의 한계를 극복</u></strong>하고 차세대 표준으로 자리 잡을 강력한 대안을 제시한다&#46;

<a id="22aeda9b0fe18079b72bcfcc8838e2d0"></a>

### 차이점 1)  패키지 Scope 

> ✏️ 
> 
> <a id="22aeda9b0fe180ab8b44d729dc4a4d35"></a>
> 
> <code>pnpm</code> 과 <code>npm</code>의 가장 근본적인 차이는 <code>node&#95;modules</code> 디렉터리를 구성하는 방식에 있다&#46;

<a id="22aeda9b0fe180558d8bee5e03fab6a0"></a>

<strong>&#91; 🤬 문제점 1&#93;  </strong>동일한 패키지가 여러 프로젝트에 중복으로 저장

<a id="22aeda9b0fe180fb800bc09b0f2f6fc3"></a>

<code>npm</code>은 <strong>각 프로젝트마다 의존성 패키지 전체를 복사</strong><strong>하여 </strong><strong>독립적인 </strong><strong><code>node&#95;modules</code></strong><strong>를 생성</strong>한다&#46;

<a id="22aeda9b0fe18027a72cf180d5bb7775"></a>

 이는 프로젝트 간 의존성 격리를 보장하지만, <strong><u>동일한 패키지가 여러 프로젝트에 중복으로 저장되어 심각한 디스크 공간 낭비를 초래</u></strong>한다&#46;

<a id="22aeda9b0fe1809c9413f3b2eaabdfd8"></a>

<strong>&#91; </strong> <strong>해결 &#93;  </strong><strong>중앙화된 전역 저장소(content&#45;addressable store)에서 관리하여 심볼릭 링크로  접근 허용</strong>

<a id="22aeda9b0fe1804dbf0dd727618c08f9"></a>

반면, <code>pnpm</code>은 <strong>패키지를 중앙화된 전역 저장소(content&#45;addressable store)</strong>에 <strong><u>단 한 번만 저장</u></strong>한다&#46; 

<a id="22aeda9b0fe180c98af0c3ad4333ceb2"></a>

그리고 각 프로젝트의 <code>node&#95;modules</code>에는 이 <strong>전역 저장소의 실제 파일을가리키는 </strong><strong><u>심볼릭 링크(symbolic link)</u></strong><strong>만을 생성</strong>한다&#46;

<a id="22aeda9b0fe180ba8b9ce3eab63754cd"></a>

 이 혁신적인 접근 방식은 <strong><u>디스크 사용량을 극적으로 감소</u></strong>시킨다&#46; 

<a id="22aeda9b0fe1802cb3eac09c8e044198"></a>

여러 프로젝트가 동일한 버전의 Next&#46;js를 사용하더라도, 실제 파일은 단 한 벌만 디스크에 존재하게 된다&#46; 

<a id="22aeda9b0fe180b9a116fbcafe734a7f"></a>

이는 곧바로 <strong><u>설치 속도의 향상</u></strong>으로 이어진다&#46; 

<a id="22aeda9b0fe1806da998ea6d60743894"></a>

<strong><u>이미 전역 저장소에 캐시된 패키지는 다시 다운로드할 필요 없이 링크 생성만으로 설치가 완료</u></strong>되므로, 반복적인 설치 작업에서 압도적인 속도 우위를 점한다&#46;

<a id="22aeda9b0fe180af91fee3f52ab35a08"></a>

### 차이점 2) 패키지 구조 &#45; 플랫, 비&#45;플랫

> <strong>&#91; 🤬 문제점 2&#93;  플랫 구조에 따른 </strong>유령 의존성(phantom dependency) 존재

<a id="22aeda9b0fe18037a2cadfef61037d33"></a>

기술적인 우위는 여기서 그치지 않는다&#46; 

<a id="22aeda9b0fe180ca85fcf29f0642410e"></a>

npm v3부터 도입된 <strong><u>&#34;플랫(flat)&#34;</u></strong><strong><u> </u></strong><strong><u><code>node&#95;modules</code></u></strong><strong><u> </u></strong><strong><u>구조</u></strong>는 심각한 부작용을 낳았다&#46; 

<a id="22aeda9b0fe1805a9253d0b913837c52"></a>

모든 하위 의존성까지 최상단에 끌어올리는 이 방식은 <strong><code>package&#46;json</code></strong>에 명시적으로 선언하지 않은 패키지, <br>이른바 <strong><u>유령 의존성(phantom dependency)에 코드상으로 접근</u></strong>할 수 있게 만든다&#46; 

<a id="22aeda9b0fe180d7ba45c78a1fb66c1f"></a>

이는 <strong><u>의도치 않은 버전 충돌이나 예기치 않은 버그의 잠재적 원인</u></strong>이 되어 프로젝트의 안정성을 저해한다&#46;

<a id="22aeda9b0fe180a2bfb7c39627f95e32"></a>

<strong>&#91; </strong><strong> 해결 &#93;  </strong><strong>중앙화된 전역 저장소(content&#45;addressable store)에서 관리하여 심볼릭 링크로  접근 허용</strong>

<a id="22aeda9b0fe1806393fbcb131fa09a26"></a>

<code>pnpm</code>은 이 문제를<strong><u> 비&#45;플랫(non&#45;flat)</u></strong><strong><u> </u></strong><strong><u><code>node&#95;modules</code></u></strong><strong><u> 구조</u></strong>로 해결한다&#46; <strong>오직 package&#46;json에 명시된 패키지만이 프로젝트 루트의 node&#95;modules에서 직접 접근 가능</strong>하도록 링크된다&#46; 

<a id="22aeda9b0fe180a7bfc3e7a49c63548a"></a>

이를 통해 <strong><u>개발자는 선언된 의존성만을 사용하도록 강제</u></strong>받으며, 이는 <strong><u>코드의 예측 가능성과 안정성을 크게 향상</u></strong>시킨다&#46;

<a id="22aeda9b0fe180e1b7b9c0637a719c4b"></a>

### pnpm 장점

<a id="22aeda9b0fe1800a856dceb47c876bdf"></a>

마지막으로, <code>pnpm</code>은 <strong><u>모노레포(Monorepo) 환경을 네이티브로 강력하게 지원</u></strong>한다&#46; 

<a id="22aeda9b0fe1802d90a8f8be0b887f3f"></a>

내장된 워크스페이스 기능은 여러 하위 프로젝트의 의존성을 효율적으로 관리하고 상호 연결하는 데 최적화되어 있어, 복잡한 대규모 애플리케이션 아키텍처에 완벽하게 부합한다&#46;

<a id="22aeda9b0fe180e49997de753caf7440"></a>

### 정리

> 🗒️ 
> 
> <a id="22aeda9b0fe180f5b4cced982c24f80d"></a>
> 
> 결론적으로, pnpm은 단순한 패키지 매니저를 넘어, 디스크 효율성, 설치 속도, 의존성 관리의 엄격함을 통해 현대 JavaScript 개발 환경의 생산성과 안정성을 한 단계 끌어올리는 필수적인 도구이다&#46;

| 특징 | <code>npm</code> | <code>pnpm</code> |
| --- | --- | --- |
| <strong>디스크 사용량</strong> | 높음 (프로젝트마다 중복 저장) | <strong>매우 낮음</strong> (전역 저장소 &#43; 링크) |
| <strong>설치 속도</strong> | 보통 | <strong>매우 빠름</strong> (링크 생성 위주) |
| <strong><code>node&#95;modules</code></strong><strong> 구조</strong> | 플랫 구조 (유령 의존성 위험) | <strong>비&#45;플랫 구조</strong> (엄격한 의존성 관리) |
| <strong>모노레포 지원</strong> | 지원 (Workspaces) | <strong>강력하게 지원</strong> (내장 기능) |
