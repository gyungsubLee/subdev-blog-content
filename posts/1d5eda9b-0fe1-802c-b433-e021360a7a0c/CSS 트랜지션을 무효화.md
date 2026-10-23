---
order: 64
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d5eda9b-0fe1-802c-b433-e021360a7a0c
title: CSS 트랜지션을 무효화
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d5eda9b-0fe1-802c-b433-e021360a7a0c
    title: CSS 트랜지션을 무효화
excerpt: "오류) display: none → display: inline: CSS 트랜지션을 무효화한다. --- 원인 ☝🏻 display 속성은 transition이 지원되지 않는 속성이다. 즉, display: none → display: inline은 브라우저가 바로 바꿔버리므로 애니메이션이 생략된다. 해결 1. displa"
cover: null
icon: null
notionProperties:
  Tags: 오류
  상태: 의문점 정리 필요
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-14T08:25:07.080Z
updated: 2025-04-14T08:25:53.000Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/CSS 트랜지션을 무효화-e021360a7a0c/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d5eda9b0fe1802cb433e021360a7a0c
---
<a id="1d5eda9b0fe180f680b0d15e24ec63b9"></a>

### 오류) <strong><code>display&#58; none</code></strong><strong> → </strong><strong><code>display&#58; inline</code></strong><strong>&#58; CSS 트랜지션을 무효화한다&#46;</strong>

---

<a id="1d5eda9b0fe1804ba26ef3bef58bb383"></a>

### 원인

> ☝🏻 
> 
> <a id="1d5eda9b0fe18011aaaddff57e60a8a7"></a>
> 
> <code>display</code> 속성은 <code>t</code><strong><code>ransition</code></strong><strong>이 지원되지 않는 속성이다&#46;</strong>
> 
> <a id="1d5eda9b0fe180f3925bdfca4fed14c7"></a>
> 
> 즉, display&#58; none → display&#58; inline은 <strong>브라우저가 바로 바꿔버리므로 애니메이션이 생략된다&#46;</strong>

<a id="1d5eda9b0fe180c5aa40eb4c6e57eaf4"></a>

### 해결

<a id="1d5eda9b0fe180129dbbf372b5cfaa45"></a>

<strong>1&#46; display 대신 </strong><strong><code>visibility</code></strong><strong>, </strong><strong><code>opacity</code></strong><strong>, </strong><strong><code>max&#45;height</code></strong><strong>, </strong><strong><code>pointer&#45;events</code></strong><strong> 등을 활용</strong>

<a id="1d5eda9b0fe180889273f2e5301decc0"></a>

```html
.menuBox {
  visibility: hidden;
  opacity: 0;
  max-height: 0;
  pointer-events: none;
  transition: all 0.6s;
}

.menuBox.on {
  visibility: visible;
  opacity: 1;
  max-height: 500px;
  pointer-events: auto;
}
```
