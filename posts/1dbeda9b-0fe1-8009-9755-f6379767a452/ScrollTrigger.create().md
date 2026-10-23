---
order: 13
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1dbeda9b-0fe1-8009-9755-f6379767a452
title: ScrollTrigger.create()
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1dbeda9b-0fe1-8009-9755-f6379767a452
    title: ScrollTrigger.create()
excerpt: "ScrollTrigger.create() --- 📖 ScrollTrigger.create({ trigger: selector, ... }) --- 해당하는 요소들에 대해 각각 ScrollTrigger를 적용시키다. - selector: 순회 중인 각각의 DOM 요소 ex) javascript gsap.utils.toAr"
cover: null
icon: null
notionProperties:
  Tags: GSAP 개념
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-20T01:44:01.237Z
updated: 2025-04-20T01:56:31.166Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/ScrollTrigger.create()-f6379767a452/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1dbeda9b0fe180099755f6379767a452
---
<a id="1dbeda9b0fe1806cbcb8ffb280294bb0"></a>

## <strong><code>ScrollTrigger&#46;create()</code></strong>

---

> 📖 
> 
> <a id="1dbeda9b0fe1803194e3d639cf8fb807"></a>
> 
> <strong><code>ScrollTrigger&#46;create(</code></strong><strong><code>{ trigger&#58; selector, &#46;&#46;&#46; }</code></strong><strong><code>)</code></strong>
> 
> ---
> 
> <a id="1dbeda9b0fe180f2bdb2e80c213f2ba3"></a>
> 
> 해당하는 요소들에 대해 <strong><u>각각 ScrollTrigger를 적용</u></strong>시키다&#46; 
> 
> - <strong><code>selector</code></strong><strong>&#58; 순회 중인 각각의 DOM 요소</strong>

<details>
<summary>ex) </summary>

<a id="1dbeda9b0fe18032b44cd4e9b00857ee"></a>

```javascript
gsap.utils.toArray('.con3 .listBox li').forEach((selector, idx) => {
    ScrollTrigger.create({
        trigger: selector,
        start: '30% 50%',
        onEnter: () => {
            gsap.set(selector, {
                rotationX: '-65deg',
                z: '-500px',
                opacity: 0
            }),
            gsap.to(selector, {
                rotationX: 0,
                z: 0,
                opacity: 1,
                delay: idx % 3 * .05
            })
        },
        markers: true
    })
})
```

- <code>gsap&#46;utils&#46;toArray(&#39;&#46;con3 &#46;listBox li&#39;)</code>
    - <code>&#46;con3 &#46;listBox li</code> selector를 가진 모든 DOM을 가져와 배열로 생성

- <code>&#46;forEach((selector, idx) =&#62; { ScrollTrigger&#46;create({…})})</code>
    - DOM 배열의 DOM들을 순화하며 각각 ScrollTriger를 적용시킴

</details>
