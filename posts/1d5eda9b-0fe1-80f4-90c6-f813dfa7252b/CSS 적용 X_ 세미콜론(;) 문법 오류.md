---
order: 65
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d5eda9b-0fe1-80f4-90c6-f813dfa7252b
title: "CSS 적용 X: 세미콜론(;) 문법 오류"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d5eda9b-0fe1-80f4-90c6-f813dfa7252b
    title: "CSS 적용 X: 세미콜론(;) 문법 오류"
excerpt: "오류 --- css / header 설정/ header { position: fixed; width: 100%; z-index: 9999;} header .inner { padding: 30px 50px 0; } header .inner .logo { width: 150px; display: flex; justify-co"
cover: null
icon: null
notionProperties:
  Tags: 오류
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-14T06:44:38.628Z
updated: 2025-04-14T06:49:05.396Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/CSS 적용 X- 세미콜론(;) 문법 오류-f813dfa7252b/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d5eda9b0fe180f490c6f813dfa7252b
---
<a id="1d5eda9b0fe180798308ef395314fc9c"></a>

### 오류 

---

<a id="1d5eda9b0fe18089843ffb60250787c3"></a>

```css

/* header 설정*/
header { position: fixed; width: 100%; z-index: 9999;}
header .inner { padding: 30px 50px 0; }
header .inner .logo { width: 150px; display: flex; justify-content: space-between; }
header .inner .logo span { padding: 0 1px; };
header .inner .logo span img { width: 100%; };
```

<a id="1d5eda9b0fe180428af1cb48b16e8a17"></a>

위 CSS에서 <code>span</code>, <code>img</code> DOM에 정의한 css가 적용되지 않음

<a id="1d5eda9b0fe180edb73ff8a3b9ca39eb"></a>

### 해결

---

> <strong>원인&#58; </strong><strong>🤬 잘못된 문법</strong>

-  세미콜론(<code>;</code>) 다음에 또 세미콜론(<code>;</code>) 붙이면 <strong>해당 CSS 룰이 무시된다&#46;</strong>

<a id="1d5eda9b0fe18000ae21ccc10f09c2b2"></a>

```css
header .inner .logo span { padding: 0 1px; };
header .inner .logo span img { width: 100%; };
```

> <strong>해결</strong>

- 끝에  세미콜론(<code>;</code>)  제거

<a id="1d5eda9b0fe1803f8d9cf235c4304f32"></a>

```css
header .inner .logo span { padding: 0 1px; }
header .inner .logo span img { width: 100%; }
```
