---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1dbeda9b-0fe1-80d7-af68-f15d86c4962c
title: gsap.set(selector, {…})
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1dbeda9b-0fe1-80d7-af68-f15d86c4962c
    title: gsap.set(selector, {…})
excerpt: "gsap.set(selector, {…}) --- 📖 gsap.set(selector, {…}) --- 애니메이션 시작 전 미리 상태를 세팅 ex) javascript gsap.set(selector, { rotationX: '-65deg', z: '-500px', }) - 애니메이션 시작 전 해당하는 selector("
cover: null
icon: null
notionProperties:
  Tags: GSAP 개념
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-20T01:56:32.187Z
updated: 2025-04-20T02:03:48.763Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/gsap.set(selector, {…})-f15d86c4962c/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1dbeda9b0fe180d7af68f15d86c4962c
---
<a id="1dbeda9b0fe180cea1e1e39e872cc2b6"></a>

## <code>gsap&#46;set(selector, {…})</code>

---

> 📖 
> 
> <a id="1dbeda9b0fe180aabef1e8e5364dd3c1"></a>
> 
> <strong><code>gsap&#46;set(selector, {…})</code></strong>
> 
> ---
> 
> <a id="1dbeda9b0fe180248004cd36a2394071"></a>
> 
> <strong>애니메이션 </strong><strong><u>시작 전</u></strong><u> </u><strong><u>미리 상태를 세팅</u></strong>

<a id="1dbeda9b0fe180b4aa83febc47163d89"></a>

ex) 

![](b27e24f8bd819068.webp)

<a id="1dbeda9b0fe180579114eaf29aa2e0c1"></a>

```javascript
gsap.set(selector, {
    rotationX: '-65deg',
    z: '-500px',
})
```

- <strong><u>애니메이션 시작 전</u></strong>  <strong><u>해당하는 selector(DOM)의 <br>CSS 효과를 정의</u></strong>함
