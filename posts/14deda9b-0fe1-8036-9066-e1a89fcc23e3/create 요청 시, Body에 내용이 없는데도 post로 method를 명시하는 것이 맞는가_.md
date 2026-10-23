---
order: 13
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 14deda9b-0fe1-8036-9066-e1a89fcc23e3
title: create 요청 시, Body에 내용이 없는데도 post로 method를 명시하는 것이 맞는가?
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 14aeda9b-0fe1-80fe-aa6c-d5d5adc42f01
    title: 7. 통화 변환 앱
  - id: 14deda9b-0fe1-8036-9066-e1a89fcc23e3
    title: create 요청 시, Body에 내용이 없는데도 post로 method를 명시하는 것이 맞는가?
excerpt: "질문 내용 환전 내용 생성하는 url 이전 REST API 질문에서 body로 명시한 내용을 pathvariable로 명시하기 떄문에, get 요청과 동일한 것 같아 Method를 get으로 변경했다. 지금 생각해보면 왜 이런 의문점이 들었는지도 모르겠음..? 답변 --- 1. 유저가 환전할 금액이 body에 포함되어야 "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 14aeda9b-0fe1-80fe-aa6c-d5d5adc42f01
created: 2024-11-29T03:07:49.178Z
updated: 2024-11-29T04:22:00.086Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/7. 통화 변환 앱-d5d5adc42f01/create 요청 시, Body에 내용이 없는데도 post로 method를 명시하-e1a89fcc23e3/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/14deda9b0fe180369066e1a89fcc23e3
---
<a id="14deda9b0fe1808ea7d0c88721b87127"></a>

### 질문 내용

![](a7772b39fdf10d96.webp)

<a id="14deda9b0fe180ffaf18d5a00e47ee20"></a>

환전 내용 생성하는 url

<a id="14deda9b0fe180b98becd86160339b55"></a>

이전 REST API 질문에서 body로 명시한 내용을 pathvariable로 명시하기 떄문에, <br>get 요청과 동일한 것 같아 Method를 get으로 변경했다&#46; 

> <del>지금 생각해보면 왜 이런 의문점이 들었는지도 모르겠음&#46;&#46;?</del>

<a id="14deda9b0fe180078588f021738f4dd7"></a>

### 답변

---

1. 유저가 환전할 금액이 body에 포함되어야 한다 &#46; <br>따라서 body에 내용이 없는 것은 올바르지 않다&#46; 

1. 데이터베이스의 조작이 들어가기 때문에, POST로 메서드를 명시해야한다&#46; 

<a id="14deda9b0fe180c19e09df22537ce36d"></a>

위와 같은 답변을 말씀해주셨다&#46; 

<a id="14deda9b0fe1809e8ccced0c487f9abc"></a>

해당 내용을 정리하자면, HTTP METHOD는 각 CRUD의 특징을 나타낸다&#46; 

- C&#58; POST

- R&#58; GET

- U&#58; PUT, PATCH, POST

- D&#58; DELETE

<a id="14deda9b0fe180f49b12c488e301c38a"></a>

<br>Body의 유무가 아닌 각 특징에 해당되도록 명시해야한다&#46; <br> <u>사용자로부터 받아오지 않고 비지니스 로직에서 처리</u>되<strong>어도 </strong>DB에 변경이 발생되는 것은 조회가 아닌 생성이기 때문에,  GET이 아닌 POST로 명시하는 것이 올바른 설계이다&#46; 

<a id="14deda9b0fe180d4a74dfc65e1e3182b"></a>

따라서 아래와 같이 GET을 다시 POST로 명시했다&#46;

![](3e45d07be7b7d12c.webp)
