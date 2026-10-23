---
order: 57
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d9eda9b-0fe1-80bc-9cfe-eff1184902c2
title: "position: absolute"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d9eda9b-0fe1-80bc-9cfe-eff1184902c2
    title: "position: absolute"
excerpt: "position: absolute --- ✏️ 부모 요소 중에 position: relative, absolute, fixed, sticky 중 하나라도 선언된 부모가 있으면, 가장 가까운 부모를 기준으로 삼아 위치를 정렬한다. 만약 그런 부모가 없다면 브라우저 Viewport (화면 보이는 영역) 자체를 기준으로 잡아 "
cover: null
icon: null
notionProperties:
  Tags: position
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-18T04:33:55.018Z
updated: 2025-04-18T05:15:44.731Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/position- absolute-eff1184902c2/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d9eda9b0fe180bc9cfeeff1184902c2
---
<a id="1d9eda9b0fe1802cb2daf7a78375d2e5"></a>

## <code>position&#58; absolute</code>

---

> ✏️ 
> 
> <a id="1d9eda9b0fe180ec939ae79e2ecc7aa3"></a>
> 
> 부모 요소 중에 <code>position&#58; relative, absolute, fixed, sticky</code> 중 <strong>하나라도 선언된 부모</strong>가 있으면, <strong><u>가장 가까운 부모</u></strong><u>를 기준으로 삼아 위치를 정렬</u>한다&#46; 
> 
> <a id="1d9eda9b0fe18020be25df2a4b64f44c"></a>
> 
> 만약 그런 부모가 없다면  <strong><code>브라우저 Viewport</code></strong><code> (화면 보이는 영역)</code> 자체를 <strong>기준으로 잡아 위치를 정렬</strong>한다&#46;

<details>
<summary><strong>🧐 </strong><strong><code>브라우저의 Viewport</code></strong><strong> 란?</strong></summary>

> ✏️ 
> 
> <a id="1d9eda9b0fe1801fb131ecb5cd3f9bc9"></a>
> 
> <strong>Viewport란  </strong><strong><u>브라우저 창 안에서 실제로 웹페이지 내용이 보이는 영역</u></strong><em> </em>을 말한다&#46; 
> 
> - <strong>Viewport = 사용자가 볼 수 있는 화면 영역</strong>
> 
> - <strong>쉽게 말해  모니터 화면 자체가 아니라 </strong><strong><u>웹사이트가 “보이는” 그 창 부분</u></strong><strong>을 말한다&#46;</strong>

</details>

<details>
<summary>🧐 그러면 posiotn fixed 와 같이 고정된 형태로 보여진다는 건가? <br>화면에 보이는 vitew 영역은 유저에 의해 실시간으로 변경될텐데 어떻게 계산을 하고 정의되는가?</summary>

---

<a id="1d9eda9b0fe1803aae73dbda333b4f31"></a>

<strong><code>absolute</code></strong><strong>, </strong><strong><code>fixed</code></strong><strong>  둘다  좌표(positioning)를 기준으로 정렬되는 것은 같지만 동작이 다르다&#46; </strong>

|  | <code>absolute</code> | <code>fixed</code> |
| --- | --- | --- |
| 기준 | <strong>가까운 position 부모</strong> (없으면 Viewport) | <strong>항상 Viewport</strong> (부모 신경 안 씀) |
| 스크롤시 | 부모랑 같이 스크롤 따라감 | <strong>화면에 고정됨</strong>, 스크롤해도 안 움직임 |

<a id="1d9eda9b0fe180a2b423ce9aaf358545"></a>

position 부모가 없는 <code>absolute</code>는 <strong>브라우저가 </strong><strong><u>맨 처음 </u></strong><strong>로드될 때</strong><strong><u> Viewport를 기준</u></strong><strong>으로</strong> <code>top&#58;10px</code>, <code>left&#58;20px</code> 위치한다&#46;

<a id="1d9eda9b0fe180c5825cfd2d28f7ff24"></a>

<br>따라서 항상 viewport를 기준으로 잡는 position과 달리 <strong><u>스크롤 시 같이 위로 밀려서 사라진다&#46;</u></strong>

</details>

<details>
<summary>🧐 <strong>Viewport가 유저에 의해 실시간으로 바뀌는데, 어떻게 계산되는가?</strong></summary>

---

<a id="1d9eda9b0fe180dba054fa2a79614c17"></a>

브라우저 크기를 줄이거나 ( 리사이징 ), 모바일 기기 방향을 바꾸거나, 창을 최소화/확대하거나 할 때마다 <strong><u>실시간으로 재계산</u></strong> 된다&#46;

<a id="1d9eda9b0fe1809da0ecf7538abcdd67"></a>

브라우저는 아래와 같은 순서로 동작하는데, 

1. 브라우저가 Viewport 크기를 계산한다 &#46;

1. CSS 엔진이 top, left, right, bottom 같은 속성갑승ㄹ 기준으로 배치(Layout) 한다&#46; 

1. 유저가 창 크기를 바꾸면, 브라우저가 다시 Viewport 크기를 갱신하고, 그에 맞춰 다시 배치(Reflow) 한다&#46; 

<a id="1d9eda9b0fe180d3b88be9499ff15cd8"></a>

즉, <strong>Viewport는 “현재 화면 사이즈”를 항상 실시간으로 반영한다&#46;</strong>

<a id="1d9eda9b0fe180638773c5f7a0844eb0"></a>

따라서 <code>fixed</code> 요소는 매 프레임마다 Viewport 좌표를 기준으로 <strong>위치가 보정되며</strong>

<a id="1d9eda9b0fe180c886f2ca0ca958678b"></a>

<code>absolute</code>는 최소 기준을 잡은 후, 부모에 따라 움직이지만 부모가 스크롤 되면 같이 움진다&#46;<br>

</details>

<details>
<summary>🧐 그렇다면 <strong><code>position&#58; sticky</code></strong>는 어떻게 동작하는가?</summary>

> ✏️ 
> 
> <a id="1d9eda9b0fe18072b213f8019830c9ee"></a>
> 
> <strong><code>position&#58; sticky</code></strong>
> 
> ---
> 
> > <a href="#/post/1d5eda9b-0fe1-8077-9786-db7fc22a1fd6">페이지</a> 
> 
> <a id="1d9eda9b0fe180e6b23ed6cd0ddf22ce"></a>
> 
> <strong>sticky는 absolute와 fixed의 하이브리드</strong> 같은 개념이다&#46;
> 
> - <strong><u>원래는 normal flow </u></strong><strong>처럼 있다가, </strong><strong><u>특정 지점에 도달하면 화면에 ‘고정’</u></strong><strong>되는</strong> 포지션이다&#46;
> 
> <details>
> <summary><strong>sticky 기본 작동 흐름</strong></summary>
> 
> 1. <strong>처음엔 일반적인 흐름(normal flow)</strong> 으로 존재
> 
> 1. <strong>스크롤을 하다가 </strong><strong><u>특정 기준(top, left 등)을 넘</u></strong><strong>으면 </strong><strong><u>해당 부분 부터는 fixed처럼 화면에 고정</u></strong><strong>된다&#46;</strong>
> 
> </details>

</details>

<details>
<summary>ex) 부모 DOM에 position 선언이 없는 경우 </summary>

- html 
    <a id="1d9eda9b0fe180f5a7adfc259acbbc51"></a>

    ```html
    <body>
      <div class="child"></div>
    </body>
    ```

- css
    <a id="1d9eda9b0fe180ffb177cfef533dff0d"></a>

    ```css
    .child {
      position: absolute;
      top: 10px;
      left: 20px;
      width: 100px;
      height: 100px;
      background: red;
    }
    ```

<a id="1d9eda9b0fe180d2bb7cc35fef8bbeb4"></a>

부모인 <code>&#60;body&#62;</code>에 <code>position&#58; relative</code>도 없고, 조상에도 <code>relative</code> 가 존재하지 않는다&#46; 

<a id="1d9eda9b0fe18031b431d964fa60cd38"></a>

따라서 <code>child</code> DOM은 <strong>브라우저 Viewport</strong> 기준으로 <code>top&#58; 10px</code>, <code>left&#58; 20px</code>에 놓인다&#46;

<a id="1d9eda9b0fe18088b7eec51e6e1a341d"></a>

<strong>즉, </strong><strong><u>화면 제일 왼쪽 위 (0,0) 기준</u></strong><strong>으로 </strong><strong><u>10px 아래, 20px 오른쪽</u></strong><strong>으로 위치한다는 뜻이다&#46;</strong>

</details>
