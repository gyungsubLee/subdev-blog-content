---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 26feda9b-0fe1-8146-856c-c55134dcccd4
title: "[ 이론 ] Pagination"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 26feda9b-0fe1-8079-9060-e36e01d3f411
    title: 페이지네이션( Pagination )
  - id: 26feda9b-0fe1-8146-856c-c55134dcccd4
    title: "[ 이론 ] Pagination"
excerpt: "목차 - Pagination - Pagination의 종류 ( 2가지 ) - 1. Page Based Pagination - 2. Cursor Based Pagination /icons/taggray.svg 이전 정리 내용 - 페이지 Pagination --- 📖 Pagination: 많은 데이터를 부분적으로 나눠서 불"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 26feda9b-0fe1-8079-9060-e36e01d3f411
created: 2025-09-15T13:29:36.520Z
updated: 2025-10-18T06:53:43.904Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/페이지네이션( Pagination )-e36e01d3f411/[ 이론 ] Pagination-c55134dcccd4/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/26feda9b0fe18146856cc55134dcccd4
---
> 
> 
> <a id="26feda9b0fe181a28ad2e331a5925dbd"></a>
> 
> <strong>목차</strong>
> 
> - [Pagination](#26feda9b0fe18144a857fbdc8417cf98)
> - [ Pagination의 종류 ( 2가지 )](#26feda9b0fe1816b9ff9f13d42317447)
> - [1. Page Based Pagination](#26feda9b0fe18131b886eb3e8327b09f)
> - [2. Cursor Based Pagination](#271eda9b0fe180909dbed862c5149063)

> /icons/tag_gray.svg 
> 
> <a id="271eda9b0fe180dd8a82cab73ca3d3b3"></a>
> 
> <strong>이전 정리 내용</strong>
> 
> - <a href="#/post/1c3eda9b-0fe1-81bd-9548-f2eadadc9ae8">페이지</a> 

<a id="26feda9b0fe18144a857fbdc8417cf98"></a>

## Pagination

---

> 📖 
> 
> <a id="26feda9b0fe18126a824c35c74b4e959"></a>
> 
> <code>Pagination</code>&#58; 많은 데이터를 부분적으로 나눠서 불러오는 기술이다 

> ✏️ 
> 
> - <code>데이터 분할</code>
>     - 큰 분량의 데이터를 분할해서 다루기 쉽게 부분적으로 불러올 수 있다&#46; 
> 
> - <code>네이게이션 컨트롤</code>
>     - 다음 페이지, 이전 페이지 등 기능을 통해 쉽게 페이지 이동이 가능하다&#46; 
> 
> - <code>균일한 데이터 규격</code>
>     - 요청과 응답이 균일한 규격으로 제공되어 예측하기 쉽다&#46;
> 
> - <code>상태 유지</code> 
>     - Pagination 요청 자체에 상태 정보가 존재한다&#46;  (e&#46;g&#46; 몇번째 페이지 )
> 
> - <code>퍼포먼스 최적화</code>
>     - 한번에 필요한 분량의 데이터만 불러오기 때문에 퍼포먼스 최적화가 가능하다&#46; 

<a id="26feda9b0fe1816b9ff9f13d42317447"></a>

##  Pagination의 종류 ( 2가지 )

<a id="26feda9b0fe18131b886eb3e8327b09f"></a>

### 1&#46; Page Based Pagination

> ✏️ 
> 
> <a id="26feda9b0fe181c894a3d35dc8cf0913"></a>
> 
> 데이터를 페이지 기반으로 나눠서 처리한다&#46; 
> 
> - ex) <br>100개 데이터 한번에 20개 씩 가져온다면 5개의 페이지로 나눌 수 있다&#46; 

<details>
<summary>예제 ) 12 데이터, 4개 씩 조회</summary>

- <code>Page 1</code>&#58; 1 &#126; 4
    ![](e68f86856d558bf3.webp)

- <code>Page 2</code>&#58; 5 &#126; 8
    ![](3386206c583245ba.webp)

- <code>Page 3</code>&#58; 9 &#126; 12
    ![](e63f6073d7cd01a7.webp)

</details>

<details>
<summary>문제점 ) 데이터 삽입</summary>

![](20d154746de1435e.webp)

![](11080f3406f6e49d.webp)

![](8a860f4609ed36cd.webp)

- <code>리소스 중복 조회</code>
    - 신규 데이터 삽입 시, 중복 조회되는 데이터가 생긴다&#46; 

    - 서버 계층에서는 해결할 수 없다&#46;  ( 클라이언트에서 필터링 처리 )

    - 중복 조회되는 데이터 마다 추가적으로 비용이 든다&#46;

</details>

<details>
<summary>문제점 ) 데이터 삭제</summary>

![](39a02e26138adbf2.webp)

![](14c19c3284568fb6.webp)

- 다음 페이지 조회 시앞 데이터가 삭제 돼서, 조회가 누락되는 경우가 생긴다 <br>( 앞 페이지 끝을 다시 확인해야함 )

</details>

<a id="271eda9b0fe180909dbed862c5149063"></a>

### 2&#46; Cursor Based Pagination

> ✏️ 
> 
> <a id="271eda9b0fe180a4b647df9ddf2400f5"></a>
> 
> 마지막 불러온 데이터를 기반으로 다음 가져올 데이터를 정한다&#46; 
> 
> - ex) 
>     <a id="271eda9b0fe18052bfbcf514ccb4c7cf"></a>
> 
>     마지막으로 불러온 데이터가 20번이었다면 다음 요청은 21번부터 가져온다/

<details>
<summary>예제 ) 12 데이터, 4개 씩 조회</summary>

- <code>Page 1</code>&#58; 1 &#126; 4
    ![](3053b2cbf15ab297.webp)

- <code>Page 2</code>&#58; 5 &#126; 8
    ![](371c124685236f25.webp)

- <code>Page 3</code>&#58; 9 &#126; 12
    ![](4e0b5d16721181af.webp)

</details>

<details>
<summary>예제 ) 데이터 삽입</summary>

![](4f9c80066690c42d.webp)

![](23a4b631e8fcc5e2.webp)

</details>

<details>
<summary>예제 ) 데이터 삭제</summary>

![](a62f15894686274c.webp)

![](f5c58589971cc811.webp)

</details>

> ❗ 
> 
> <a id="272eda9b0fe180cbbf9feb5a1598706f"></a>
> 
> <code>Cursor 기반 페이징 처리</code>를 통해 <code>Page 기반 페이징 처리</code>의 단점을 해결할 수 있다&#46;  그러나 더 구현 난이도가 높다&#46;
> 
> - 특히 <code>uuid 기반 페이징 처리</code> 시 어렵다&#46;
