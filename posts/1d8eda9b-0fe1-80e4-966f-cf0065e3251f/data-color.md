---
order: 48
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d8eda9b-0fe1-80e4-966f-cf0065e3251f
title: data-color
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d8eda9b-0fe1-80e4-966f-cf0065e3251f
    title: data-color
excerpt: "data-color --- 변수명으로 색상 지정 가능하다. css .con3 .listBox li .img { background-color: var(--sub-color); border-radius: 10px; text-align: center; padding: 30% 0; } . . . .con3 .listBox li"
cover: null
icon: null
notionProperties:
  Tags: 변수
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-17T08:31:48.227Z
updated: 2025-04-18T05:19:30.716Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/data-color-cf0065e3251f/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d8eda9b0fe180e4966fcf0065e3251f
---
<a id="1d8eda9b0fe18069b973fb5ed52a44e7"></a>

## <code>data&#45;color</code>

---

<a id="1d8eda9b0fe180d398cdc20e614c3897"></a>

변수명으로 색상 지정 가능하다&#46; 

<a id="1d8eda9b0fe1805bb62de4a2086f3de9"></a>

```css
.con3 .listBox li .img { background-color: var(--sub-color); border-radius: 10px; text-align: center; padding: 30% 0; }

 . . .

.con3 .listBox li[data-color="a"]{--sub-color: #d1dbfd;}
.con3 .listBox li[data-color="b"]{--sub-color: #90c3cd;}
.con3 .listBox li[data-color="c"]{--sub-color: #ff764a;}
.con3 .listBox li[data-color="d"]{--sub-color: #47b172;}
.con3 .listBox li[data-color="e"]{--sub-color: #ffb84f;}
```

- 위와 같이 <strong><u>클래스명을 지정</u></strong>하여  해당 DOM에 색상을 지정할 수 있다&#46; 

<details>
<summary>html &#45; 각 클래스(css)  지정</summary>

<a id="1d8eda9b0fe180a7a467c765b612fd74"></a>

```css
<ul class="listBox">
  <li data-color="a">
    <p class="img"><img src="images/projects.png" alt=""></p>
    <h4>
      <span class="a">Title</span>
      <span class="b">2025</span>
    </h4>
  </li>
  <li data-color="b">
    <p class="img"><img src="images/projects.png" alt=""></p>
    <h4>
      <span class="a">Title</span>
      <span class="b">2025</span>
    </h4>
  </li>
  <li data-color="c">
    <p class="img"><img src="images/projects.png" alt=""></p>
    <h4>
      <span class="a">Title</span>
      <span class="b">2025</span>
    </h4>
  </li>
  <li data-color="d">
    <p class="img"><img src="images/projects.png" alt=""></p>
    <h4>
      <span class="a">Title</span>
      <span class="b">2025</span>
    </h4>
  </li>
  <li data-color="e">
    <p class="img"><img src="images/projects.png" alt=""></p>
    <h4>
      <span class="a">Title</span>
      <span class="b">2025</span>
    </h4>
  </li>
  <li data-color="a">
    <p class="img"><img src="images/projects.png" alt=""></p>
    <h4>
      <span class="a">Title</span>
      <span class="b">2025</span>
    </h4>
  </li>
  <li data-color="b">
    <p class="img"><img src="images/projects.png" alt=""></p>
    <h4>
      <span class="a">Title</span>
      <span class="b">2025</span>
    </h4>
  </li>
  <li data-color="c">
    <p class="img"><img src="images/projects.png" alt=""></p>
    <h4>
      <span class="a">Title</span>
      <span class="b">2025</span>
    </h4>
  </li>
  <li data-color="d">
    <p class="img"><img src="images/projects.png" alt=""></p>
    <h4>
      <span class="a">Title</span>
      <span class="b">2025</span>
    </h4>
  </li>
</ul>
```

</details>
