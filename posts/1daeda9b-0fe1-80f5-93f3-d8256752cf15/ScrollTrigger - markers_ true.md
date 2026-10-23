---
order: 23
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1daeda9b-0fe1-80f5-93f3-d8256752cf15
title: "ScrollTrigger - markers: true"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1daeda9b-0fe1-80f5-93f3-d8256752cf15
    title: "ScrollTrigger - markers: true"
excerpt: "ScrollTrigger - markers: true --- javascript gsap .registerPlugin(ScrollTrigger); // gsap 라이브러리의 ScrollTrigger 등록 gsap.timeline({ scrollTrigger: { trigger: '.visual', start: '100% "
cover: null
icon: null
notionProperties:
  Tags: JS( GSAP )
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-19T03:21:57.125Z
updated: 2025-04-19T07:34:03.811Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/ScrollTrigger - markers- true-d8256752cf15/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1daeda9b0fe180f593f3d8256752cf15
---
<a id="1daeda9b0fe180bbbbe2dc922d784843"></a>

## ScrollTrigger &#45; markers&#58; true

---

<a id="1daeda9b0fe180339b1ff2a0efea2b20"></a>

```javascript

   gsap .registerPlugin(ScrollTrigger);  // gsap 라이브러리의 ScrollTrigger 등록

    gsap.timeline({
        scrollTrigger: {
            trigger: '.visual',
            start: '100% 100%',
            end: '100% 0',
            scrub: 1,   
            markers: true
        }
    })
```

![](99950089515c1ffe.webp)

![](15511d650d312106.gif)

- <code>scrollTrigger { makers&#58; true }</code>설정 시, 렌더링 화면에 <strong><u>scroll 이벤트의 시작과 끝점을 표시</u></strong>한다&#46;
