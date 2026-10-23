---
order: 19
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81d6-9083-ed6fdf596d95
title: 왜 Shard Key는 게시판 ID로 설정하는가?
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-81d6-9083-ed6fdf596d95
    title: 왜 Shard Key는 게시판 ID로 설정하는가?
excerpt: Shard Key 적용 근거 --- 게시글 서비스는 게시판 단위로 서비스를 이용한다. - 게시판 단위로 게시글 목록 조회 게시판 ID로 샤딩 Key를 구성해야 동일한 게시판에 속한 게시글들이 같은 DB에 저장된다. 따라서 조회 및 삭제 처리하는데 수월하다. [ 🤬 Bad Case ] Shard Key = article_
cover: null
icon: null
notionProperties:
  Tags: 🧐 질문
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.661Z
updated: 2025-03-27T07:52:18.661Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/왜 Shard Key는 게시판 ID로 설정하는가--ed6fdf596d95/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181d69083ed6fdf596d95
---
<a id="1c3eda9b0fe181118902d1ea01db60fd"></a>

## Shard Key 적용 근거

---

<a id="1c3eda9b0fe1814cbd8de21506f2ebe6"></a>

게시글 서비스는 게시판 단위로 서비스를 이용한다&#46; 

- 게시판 단위로 게시글 목록 조회

<a id="1c3eda9b0fe181ea95fbc38230d1bfb2"></a>

<strong><u>게시판 ID로 샤딩 Key를 구성</u></strong>해야 <strong><u>동일한 게시판에 속한 게시글들이 같은 DB에 저장</u></strong>된다&#46;

<a id="1c3eda9b0fe181c2b93ed8f9c9ad61eb"></a>

따라서 <strong><u>조회 및 삭제 처리하는데 수월</u></strong>하다&#46; 

<a id="1c3eda9b0fe181da98dceb04d7f052ab"></a>

### <strong>&#91; 🤬 Bad Case &#93;</strong> Shard Key = <strong><code>article&#95;id</code></strong> 

---

<a id="1c3eda9b0fe181cc80fbe6ffde78309f"></a>

만약 <strong><code>Shard Key</code></strong>가 <strong><code>article&#95;i</code></strong><code>d</code> 면 동일한 게시판에 속한 게시글이 아래의 그림과 같이 별도의 샤드에 저장될 수 있다&#46;

![](4897200a352f33cf.webp)

- <code>게시판(board) 1</code> 
    -  <strong><code>게시글(article) 1</code></strong> &#45;&#62; <strong><u>좌측 샤드</u></strong>

    -  <strong><code>게시글(article) 2</code></strong>  → <strong><u>우측 샤드</u></strong>

- <code>게시판(board) 2</code> 
    -  <strong><code>게시글(article) 3</code></strong> &#45;&#62; <strong><u>좌측 샤드</u></strong>

    -  <strong><code>게시글(article) 4</code></strong>  → <strong><u>우측 샤드</u></strong>

<a id="1c3eda9b0fe1815d82b6daf125ba04bf"></a>

따라서 <strong><u>각 게시판의 게시글 목록 조회</u></strong> 시, <strong>게시글이 속한 모든 샤드에 조회 요청</strong>을 해야 한다&#46; 

<a id="1c3eda9b0fe181348e97ea0b6be46095"></a>

만약 <strong>N개의 샤드</strong> 라면 <strong><u>게시글은 N개의 샤드로 분산</u></strong>되어 있으므로, <strong>게시글 목록 조회를 위해 N개의 쿼리를 날려 목록을 만들어내는 복잡한 처리가 필요</strong>하다&#46; 

<a id="1c3eda9b0fe181e4929ec5e488f40b94"></a>

### &#91; 😎 Best Case &#93; Shard Key = <strong><code>board&#95;id</code></strong>

---

![](0a6ff0b4c5d06b14.webp)

- <code>게시판(board) 1</code> 
    - <strong><code>게시글(article) 1</code></strong><strong>, </strong> <br><strong><code>게시글(article) 2</code></strong><strong><br> ⇒ </strong> <strong><u>좌측 샤드</u></strong>

- <code>게시판(board) 2</code> 
    - <strong><code>게시글(article) 3</code></strong> , <br><strong><code>게시글(article) 4</code></strong> <br>⇒  <strong><u>우측 샤드</u></strong>

<a id="1c3eda9b0fe1817a89e3cdced0d7702c"></a>

<code>샤드 키 (Shard Key)</code>를 <code>게시판 ID (board&#95;id)</code>로  위와 그림과 같이 <strong><u>각 게시판 마다 단일 샤드에 저장</u></strong>할 수 있다&#46;

<a id="1c3eda9b0fe1817b9f88fbded4b9db5e"></a>

따라서 <strong><u>게시판의 모든 게시글 조회</u></strong> 시, <strong><u>단일 샤드</u></strong><strong>에서만 요청</strong>하여 효율적으로 처리할 수 있다&#46;
