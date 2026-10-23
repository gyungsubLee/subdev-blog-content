---
order: 52
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d8eda9b-0fe1-80da-98e5-e4ee0a426af2
title: "원근감: perspective"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d8eda9b-0fe1-80da-98e5-e4ee0a426af2
    title: "원근감: perspective"
excerpt: "원근감 애니메이션: perspective --- 📖 위와 같이 z축에 대한 애니메이션 효과( 멀리서 가까이 )를 주기위해서는 부모 요소에게 원근감을 줘야한다. - css-perspective: 요소에 원근감을 줄 수 있다. - ex) perspective: 900px ⚠️ [주의] overflow:hidden 적용 필요"
cover: null
icon: null
notionProperties:
  Tags: z축
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-17T07:39:11.708Z
updated: 2025-04-18T05:18:43.503Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/원근감- perspective-e4ee0a426af2/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d8eda9b0fe180da98e5e4ee0a426af2
---
<a id="1d8eda9b0fe180aeb1e9ff654df82108"></a>

## 원근감 애니메이션&#58; <code>perspective</code>

---

> 📖 
> 
> ![](6bf1a6a8ad6e67eb.gif)
> 
> <a id="1d8eda9b0fe180eebef3f85e7e67727a"></a>
> 
> 위와 같이 <strong><u>z축</u></strong><strong><u>에 대한 애니메이션 효과</u></strong>( 멀리서 가까이 )를 주기위해서는 <strong><u>부모 요소에게 원근감</u></strong>을 줘야한다&#46; 
> 
> - css&#45;<code>perspective</code>&#58; 요소에 원근감을 줄 수 있다&#46;
> 
> - ex) <code>perspective&#58; 900px</code>

> ⚠️ 
> 
> <a id="1d8eda9b0fe18080a99dc73a17b6072c"></a>
> 
> &#91;주의&#93; <code>overflow&#58;hidden</code> 적용 필요
> 
> ---
> 
> <a id="1d8eda9b0fe18040b50be4aad65cc387"></a>
> 
> 위와 같은 애니메이션 효과를 주기 위해서는 스크롤 이벤트를 적용해야 한다&#46; 
> 
> <a id="1d8eda9b0fe180b4bc89e011e7f8f2bf"></a>
> 
> 여기서 스크롤 이벤트 적용(triger) 시, <strong><u>가로 스크롤에 대한 값이 생성</u></strong>된다&#46; 
> 
> <a id="1d8eda9b0fe1802183c4d6455814b895"></a>
> 
> 따라서 <code>overflow&#58;hidden</code>을 적용해야 한다&#46;
> 
> - 동일하게 부모 요소에 적용한다&#46; 

<details>
<summary>예시</summary>

<a id="1d8eda9b0fe180aab483d65a6cf47597"></a>

```css

```

</details>
