---
order: 15
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1dbeda9b-0fe1-808d-a449-e3bc5990fb11
title: vw, vh, %
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1dbeda9b-0fe1-808d-a449-e3bc5990fb11
    title: vw, vh, %
excerpt: "vw, vh, % --- 📖 - vw: 브라우저 가로 길이(viewport width)의 1/100 - vh: 브라우저 세로 길이(viewport height)의 1/100 - %: 부모 요소의 크기를 기준으로한 % 크기 ex) vw, vh ✏️ - 1vw: 화면 가로 길이의 1% - 1vh: 화면 세로 길이의 1% 화"
cover: null
icon: null
notionProperties:
  Tags: 단위
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-20T01:18:09.386Z
updated: 2025-04-20T01:41:10.875Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/vw, vh, %-e3bc5990fb11/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1dbeda9b0fe1808da449e3bc5990fb11
---
<a id="1dbeda9b0fe18016860dcb480c9e2a62"></a>

## <strong><code>vw</code></strong><strong>, </strong><strong><code>vh</code></strong><strong>, </strong><strong><code>%</code></strong>

---

> 📖 
> 
> - <code>vw</code>&#58; <strong><u>브라우저 </u></strong><strong><u>가로</u></strong><strong><u> 길이(viewport width)</u></strong><strong>의 1/100</strong>
> 
> - <code>vh</code>&#58; <strong><u>브라우저 </u></strong><strong><u>세로</u></strong><strong><u> 길이(viewport height)</u></strong><strong>의 1/100</strong>
> 
> - <code>%</code>&#58; <strong><u>부모 요소의 크기</u></strong>를 기준으로한 <code>%</code> 크기

<details>
<summary>ex) <code>vw</code>, <code>vh</code></summary>

> ✏️ 
> 
> - <code>1vw</code>&#58; 화면 가로 길이의 1%
> 
> - <code>1vh</code>&#58; 화면 세로 길이의 1%

> 화면 &#45; 가로&#58;<code>1920px</code>, 세로&#58;<code>1080px</code>

- <code>1vw</code>&#58; 19&#46;2px

- <code>1vh</code>&#58; 10&#46;8px

</details>

<details>
<summary><strong>ex) </strong><strong><code>%</code></strong></summary>

<a id="1dbeda9b0fe1806ab263c379bd4681c8"></a>

```html
<div class="parent" style="width: 400px; height: 300px; background: lightblue;">
  <div class="child" style="width: 50%; height: 50%; background: orange;"></div>
</div>
```

- 부모 DOM( <code>&#46;parent</code> ) = width(가로)&#58; <code>400px</code>,  height(세로)&#58; <code>300px</code>

- 자식 DOM(<code>&#46;child</code>) = <strong>width&#58; </strong><strong><code>50%,</code></strong><strong> height&#58; </strong><strong><code>50%</code></strong>
    > <strong><code>자식 DOM 크기</code></strong><strong> </strong>=<strong> </strong><strong><code>부모 DOM 크기</code></strong><strong> </strong>x<strong> </strong><strong><code>%</code></strong>

    - <code>&#46;child</code> width = 400px × 0&#46;5 = <strong><u>200px;</u></strong>

    - <code>&#46;child</code> height = 300px × 0&#46;5 = <strong><u>150px</u></strong>

<a id="1dbeda9b0fe18084b549c30ac7e580a8"></a>

<br><br>

</details>

> 🗒️ 
> 
> <a id="1dbeda9b0fe1802f83f3d6ef139187e5"></a>
> 
> <strong>정리</strong>
> 
> ---
> 
> - <code>vw/vh</code>는 <strong><u>“브라우저 창” 기준</u></strong>
> 
> - <code>%</code>는 <strong><u>“부모 요소” 기준</u></strong>
