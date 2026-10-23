---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d9eda9b-0fe1-807e-9793-c4ff1b271f96
title: Content 5
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d9eda9b-0fe1-807e-9793-c4ff1b271f96
    title: Content 5
excerpt: ✏️ NOTE --- Content 5 --- 레이아웃 기본 - html, css, js HTML html Other Project Daebang Undustry 2025 THE Dopda Platform 2025 Y.studio Agency 2025 Hanhwa Chemical 2025 Daebang Undustry 2
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-18T05:51:04.026Z
updated: 2025-04-21T02:21:00.851Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/Content 5-c4ff1b271f96/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d9eda9b0fe1807e9793c4ff1b271f96
---
> ✏️ 
> 
> <a id="1dceda9b0fe1809ba229d7e6a66756b7"></a>
> 
> <strong>NOTE </strong>
> 
> ---

<a id="1dceda9b0fe1805fbe55f956028397ce"></a>

## Content 5

---

<a id="1dceda9b0fe180c6868ccbb5cbe52f25"></a>

### 레이아웃

<a id="1dceda9b0fe18032bb0fc6ef2ed96080"></a>

### 기본 &#45; html, css, js

<details>
<summary>HTML </summary>

<a id="1dceda9b0fe1806ab3ecd8aa27f3f4dc"></a>

```html
<!-- content 5 -->
<section class="con5">
  <div class="inner">
    <div class="mainTextBox">
      <h2>Other Project</h2>
    </div>
    <ul class="listBox">
      <li>
        <h3 data-color="a">Daebang</h3>
        <p>Undustry</p>
        <p>2025</p>
      </li>
      <li>
        <h3 data-color="b">THE Dopda</h3>
        <p>Platform</p>
        <p>2025</p>
      </li>
      <li>
        <h3 data-color="c">Y.studio</h3>
        <p>Agency</p>
        <p>2025</p>
      </li>
      <li>
        <h3 data-color="d">Hanhwa</h3>
        <p>Chemical</p>
        <p>2025</p>
      </li>
      <li>
        <h3 data-color="e">Daebang</h3>
        <p>Undustry</p>
        <p>2025</p>
      </li>
      <li>
        <h3 data-color="a">Phomain</h3>
        <p>vietnamese resturant</p>
        <p>2025</p>
      </li>
      <li>
        <h3 data-color="b">Phomain</h3>
        <p>Undustry</p>
        <p>2025</p>
      </li>
    </ul>
    <div class="imgBox box">
      <img src="images/img0.jpg" alt="">
    </div>
  </div>
</section>
```

</details>

<details>
<summary>CSS</summary>

<a id="1dceda9b0fe180d5a58ce4a4d95393de"></a>

```css
/* content 5 */
.con5 {  background-color: #fff; color: #141212; margin-bottom: 0; } 
.con5 .inner { padding: 50px; }
.con5 .inner .mainTextBox h2 { font-size: 100px; letter-spacing: -5px; font-weight: normal; text-transform: uppercase; }

.con5 .listBox { border-top: solid .5px #000; margin-top: 150px; }
.con5 .listBox li { display: grid; grid-template-columns: 1fr minmax(30%, auto) minmax(20%, auto); padding: 10px 0; border-bottom: solid .5px #000; cursor: pointer;}
.con5 .listBox li h3 { font-size: 40px; letter-spacing: -1px; font-weight: normal; }
.con5 .listBox li p { align-self: center;}
.con5 .imgBox { position: absolute; transform: scale(0); opacity: 0; z-index: 100; transition: all .1s; pointer-events: none;  transition: left 0.03s ease, top 0.03s ease;}
.wrap.on { overflow: hidden}

.con5 .listBox li:hover h3 { color: var(--sub-text-color); transition: all 0.2s; }

.con5 .listBox li h3[data-color="a"] { --sub-text-color: #3A8DFF; }  
.con5 .listBox li h3[data-color="b"] { --sub-text-color: #00C2C7; }  
.con5 .listBox li h3[data-color="c"] { --sub-text-color: #9B7EDC; }  
.con5 .listBox li h3[data-color="d"] { --sub-text-color: #FF7F50; }  
.con5 .listBox li h3[data-color="e"] { --sub-text-color: #FFC542; }  

```

</details>

<details>
<summary>js</summary>

<a id="1dceda9b0fe1802ebfb4f339cfcbb41b"></a>

```javascript

```

- 

</details>

<a id="1dceda9b0fe180eeaf3ed7518320864c"></a>

### 리액트 &#45; tailwind css

<details>
<summary>react</summary>

<a id="1dceda9b0fe180668309ec6d11eb15b5"></a>

```javascript

```

</details>
