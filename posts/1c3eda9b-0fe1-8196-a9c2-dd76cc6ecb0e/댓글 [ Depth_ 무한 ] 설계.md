---
order: 33
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8196-a9c2-dd76cc6ecb0e
title: "댓글 [ Depth: 무한 ] 설계"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-8196-a9c2-dd76cc6ecb0e
    title: "댓글 [ Depth: 무한 ] 설계"
excerpt: "depth가 무한인 경우, 상 • 하위 댓글이 재귀적으로 무한할 수 있다. 이를 이전 [depth: 2] 의 방식으로 댓글을 설계하는 경우, 하위 댓글의 정렬 정보를 알기 위해서는 모든 상위 댓글의 정보가 필요할 수 있다. - 해당하는 하위 댓글에서 상위 댓글의 parent_comment_id를 재귀적으로 가져와야 댓글의"
cover: null
icon: null
notionProperties:
  Tags: "depth: 무한"
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.505Z
updated: 2025-03-27T07:52:18.505Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/댓글 [ Depth- 무한 ] 설계-dd76cc6ecb0e/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18196a9c2dd76cc6ecb0e
---
<a id="1c3eda9b0fe181b6af48cd646d3d47a2"></a>

depth가 <code>무한</code>인 경우, 상 • 하위 댓글이 재귀적으로 무한할 수 있다&#46;

![](b0dc29adbb81d312.webp)

<a id="1c3eda9b0fe181aa864dd9989c4e1ce8"></a>

이를 이전 <code>&#91;depth&#58; 2&#93;</code> 의 방식으로 댓글을 설계하는 경우, 하위 댓글의 정렬 정보를 알기 위해서는<strong> 모든 상위 댓글의 정보가 필요할 수 있</strong>다&#46; 

- 해당하는 하위 댓글에서 상위 댓글의 <code>parent&#95;comment&#95;id</code>를 재귀적으로 가져와야 댓글의 계층 구조를 판단할 수있다&#46;

<a id="1c3eda9b0fe1815280aefd5b00cc9077"></a>

무한 depth를 가지는 경우, 이론상으로 댓글 계층이 무한하다&#46; 

<a id="1c3eda9b0fe18182973fe6366568f06b"></a>

따라서 <strong><u>계속해서 </u></strong><strong><u>재귀</u></strong><strong><u>적으로 호출</u></strong>하여 최상의 노드까지 조회를 해야한다&#46; 

<a id="1c3eda9b0fe181cdad5fe1cfb8448828"></a>

또한 이후, 정렬에 대한 연산까지 이뤄져야 한다&#46; 

<a id="1c3eda9b0fe181998531efe4897088a6"></a>

매 조회마다 이러한 연산이 발생되면 이는 비용이 너무 크며, 데이커가 많아질 수록  병목 지점이 된다&#46;

![](d03d3b7ef16c0b81.webp)

<a id="1c3eda9b0fe1812c93f8d204e34070e9"></a>

이를, 위와 같이 모든 계층 구조를 저장한다면 <strong><u>한번에 계층 구조를 판단</u></strong>할 수 있다&#46;

<a id="1c3eda9b0fe18143a5f7d5eb031d274d"></a>

그렇다면 이러한 계층 구조를 어떻게 구현하는가?<br>

![](328bf5f6c8909b50.webp)

<a id="1c3eda9b0fe181d3b866c613a9010965"></a>

위와 같이 각 depth 별로 5개의 문자열로 경로 정보를 저장한다&#46;

![](5e2655227c8e3b8f.webp)

<a id="1c3eda9b0fe18146b220d7f8f6175d07"></a>

<strong>이를 통해, 문자열 개수</strong><em> </em>에 따라 해당 <strong><u>댓글의 depth</u></strong>를 알 수 있으며 <strong><u>5개의 문자</u></strong>를 잘라서 <strong><u>각 계층의 상위 노드를 구분</u></strong>할 수 있다&#46;

<details>
<summary>ex)</summary>

- depth&#58; <code>1</code>  → 문자열&#58; <code>5</code>

- depth&#58; <code>2</code>  → 문자열&#58; <code>10</code> 

- depth&#58; <code>3</code>  → 문자열&#58; <code>15</code>
    <a id="1c3eda9b0fe1815487f8c448767ddc18"></a>

    &#46; &#46; &#46;

- depth&#58; <code>n</code> &#45;&#62;  문자열&#58; <code class="language-math">5 &#42; n</code>

<a id="1c3eda9b0fe181e38537f99b9d0a8d4f"></a>

<br>

</details>

<a id="1c3eda9b0fe1814d9120ca78fbc7718c"></a>

여기서 표현 데이터를 어떻게 구성해야 할지를 고민할 필요가 있는데,

<a id="1c3eda9b0fe18173b1bbc4b0fedaeffe"></a>

만약 각 문자 표현 범위를 알파벳 대소문자 구분없이로 정한다면 총 26개의 범위를 가지며 이를 5자리 문자열로 표현하는 경우 가질 수 있는 경우의 수는 <code>11,881,376 </code>개이다&#46;

- <code class="language-math">26^5</code> = 11,881,376

<a id="1c3eda9b0fe181fe8b17db353fa93844"></a>

약 1100만의 개수는 식별자로 사용하기에는 매우 작은 숫자이다&#46;

<a id="1c3eda9b0fe181609ab8c82a1dc9d543"></a>

 따라서 표현 요소들를 어떻게 구성해야 할지 

![](cb5dc2d6e6f0c364.webp)

- 해당 예시는 <code>&#91; depth&#58; 5 &#93;</code>까지만 표현을 했다&#46; → <code>VARCHAR(25)</code>
