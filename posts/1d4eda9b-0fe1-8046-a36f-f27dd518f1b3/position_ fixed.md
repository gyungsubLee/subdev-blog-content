---
order: 56
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d4eda9b-0fe1-8046-a36f-f27dd518f1b3
title: "position: fixed"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d4eda9b-0fe1-8046-a36f-f27dd518f1b3
    title: "position: fixed"
excerpt: "position: fixed --- 📖 position:fixed --- position의 fixed 속성을 통해 화면에 DOM 요소를 고정시킬 수 있다. ☝🏻 [주의] z-index --- - fixed가 적용되면 해당 요소가 기존의 레이아웃 흐름을 벗어난다. 즉, 기존의 흐름에서 해당 DOM 요소가 높이(heigh"
cover: null
icon: null
notionProperties:
  Tags: position
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-13T05:53:58.180Z
updated: 2025-04-18T05:16:00.129Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/position- fixed-f27dd518f1b3/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d4eda9b0fe18046a36ff27dd518f1b3
---
<a id="1d5eda9b0fe1806f81a2e0d382988bb8"></a>

## <code>position&#58; fixed</code>

---

> 📖 
> 
> <a id="1d5eda9b0fe180939673c9ee1de7a738"></a>
> 
> <code>position&#58;fixed</code>
> 
> ---
> 
> <a id="1d5eda9b0fe180ba8d17cf0e16dbc441"></a>
> 
> <code>position</code>의 <code>fixed</code> 속성을 통해 화면에 DOM 요소를 고정시킬 수 있다&#46; 

> ☝🏻 
> 
> <a id="1d5eda9b0fe180659c5fc332c192b6b7"></a>
> 
> <strong>&#91;주의&#93; </strong><strong><code>z&#45;index</code></strong>
> 
> ---
> 
> - <code>fixed</code>가 적용되면 해당 요소가 기존의 레이아웃 흐름을 벗어난다&#46; 
>     <a id="1d5eda9b0fe1808eabc7f158ee1d17e0"></a>
> 
>      즉, 기존의 흐름에서 해당 DOM 요소가 높이(height) 값 상실하게 된다&#46; 
> 
>     <a id="1d5eda9b0fe1805abf47f997869b0530"></a>
> 
>     따라서 하위 요소가 레이아웃을 덮어씌워 가려지는 현상이 발생된다&#46; 
> 
> - 그렇기 때문에 <u><code>fixed</code></u><u> 속성 적용</u> 시,  <strong><code>z&#45;index</code></strong>를 줘서 <strong><u>맨 위에  고정적</u></strong>으로 보일 수 있도록 해야한다&#46;

<a id="1d4eda9b0fe18094b04cce2f7803dcf9"></a>

```css
.header {
		position:fixed;
		width: 100%;
		z-index: 9999;
}
```
