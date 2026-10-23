---
order: 14
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 14deda9b-0fe1-80d1-9901-d886795af2b2
title: RESTful api 설계 시 주의점
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 14aeda9b-0fe1-80fe-aa6c-d5d5adc42f01
    title: 7. 통화 변환 앱
  - id: 14deda9b-0fe1-80d1-9901-d886795af2b2
    title: RESTful api 설계 시 주의점
excerpt: 배경 --- 저번주 팀프로젝트에서 피드백 받은 내용이다. 해당 부분을 토대로 api 설계 시 아래와 같은 의문점이 들어 질문 후 해당 내용을 정리한다. 의문점 --- 환전 요청 API에서 어떤 유저의 요청인지 구분하기 위한 유저 Id(userId) 와 어떤 통화로 변환될 것인지를 알기 위해 통화 Id(currencyId)
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 14aeda9b-0fe1-80fe-aa6c-d5d5adc42f01
created: 2024-11-29T02:06:24.672Z
updated: 2024-11-29T03:25:00.081Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/7. 통화 변환 앱-d5d5adc42f01/RESTful api 설계 시 주의점-d886795af2b2/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/14deda9b0fe180d19901d886795af2b2
---
<a id="14deda9b0fe180beb24aeb512bd10e8c"></a>

### 배경

---

![](a5927c95d470b0cb.webp)

<a id="14deda9b0fe180fa9199d7a02143bfef"></a>

저번주 팀프로젝트에서 피드백 받은 내용이다&#46; 

<a id="14deda9b0fe180199106dc2490069b3b"></a>

해당 부분을 토대로 api 설계 시 아래와 같은 의문점이 들어 질문 후 해당 내용을 정리한다&#46; 

<a id="14deda9b0fe1809888fbd0ac0b6078ee"></a>

### 의문점

---

![](5427e4fbed99a3a6.webp)

<a id="14deda9b0fe180399873fd6683075df6"></a>

환전 요청  API에서 어떤 유저의 요청인지 구분하기 위한 <code>유저 Id(userId)</code> 와 어떤 통화로 변환될 것인지를 알기 위해 <code>통화 Id(currencyId)</code> 를 같이 넘겨줘야 한다&#46; 

<a id="14deda9b0fe1807ea91bd77c03873946"></a>

처음 설계한 것은 위 그림과 같은데, 요청 body에 <code>유저 Id(userId)</code>,  <code>통화 Id(currencyId)</code> 넘겨줬다&#46;

<a id="14deda9b0fe18060aa26f4b9c90e4baf"></a>

여기저 저번 팀프로젝트 피드백 내용이 생각이 나, <u><code>유저 Id(userId)</code></u><u>,  </u><u><code>통화 Id(currencyId)</code></u><u> 를  </u><u>url의 하위 요소가 아닌 Body로 넘겨주는 설계</u>가 올바른 것인지 확인 받기 위해 박성원 튜터님을 찾아가 질문을 드렸다&#46; 

<a id="14deda9b0fe18086bcade753a399525e"></a>

### 답변 내용 &#45; RESTapi 설계

---

<a id="14deda9b0fe1805c8bbfccd002b53318"></a>

튜터님께 답변 받은 내용들을 정리하면 아래와 같다&#46;

<a id="14deda9b0fe180a7b3bee6ad259222ea"></a>

### 1&#46; RESTfull API <code>HTTP메서드</code> 와 <code>URI</code>를 통해서 <u>명확하게 구분</u>할 수 있어야 한다&#46; <br>    이후 요청, 응답을 확인한다&#46;

<a id="14deda9b0fe1801b8e2ed35c2677feaf"></a>

‘REST api는 요청의 <u><code>HTTP메서드</code></u><u>와 </u><u><code>URI</code></u><u>만으로 구분이 명확</u>해야 하며 그 이후 요청, 응답을 확인한다’고 말씀하셨다&#46; 

- 그 이유를 생각해보면 HTTP 통신 시, URI로 정의 가능한 문제를 body애서 정의하는 것은 메세지에 본문이 더해지고 통신이 전달되는 메세지의 용량이 커져 더  많은 리소스를 낭비돼서 그런 것 같다&#46; 

<a id="14deda9b0fe18050ac89eb1789f72f98"></a>

따라서  ‘<code>유저 Id(userId)</code>,  <code>통화 Id(currencyId)</code> Body로 넘겨주는 것보다는 이전 학습했던 세션&#45;인증/인가를 통해 세션으로 유저의 상태정보를 넘겨주고, <code>통화 Id</code>를 <u>path variable</u>로 넘겨주는 것이 올바른 설계이다&#46; ‘

<a id="14deda9b0fe1803a818ee2a719772620"></a>

라고 답변 받았다&#46; 

<a id="14deda9b0fe180ceb616ebc14ab9a40f"></a>

### 2&#46; URI의 <u>마지막에 정의된 리소스</u>를 가지고 <u>엔티티를 다룬다</u>&#46; 따라서<u> 필터링할 정보는 앞쪽에 표시</u>한다&#46; 

<a id="14deda9b0fe180b4b416dd3d1671d0bd"></a>

위 답변을 받고 ’<code>/exchange&#45;requests/currency/{currencyId}</code> 이렇게 설계하면 되나요?’ 라고 질문 드렸는데,  <br>REST api에서는 <u>맨 마지막에 해당 요청에서 다루는 리소스(엔티티)를 정의</u>하며 <u>앞 쪽에 필터링한 정보</u>를 두는 것이  REST API에서 명확한 설계라고  말씀하셨다&#46; <br>

<a id="14deda9b0fe180f5a04ced381349c2f2"></a>

위 내용에 따라 변경한 URL 설계는 아래와 같다&#46; 

- <code>/currency/{currencyId}/exchange&#45;requests</code>

<a id="14deda9b0fe18097a07cdd44feb5ab2b"></a>

### 추가 내용

- 엔티티를 구분하기 위한 값으로 꼭 Long 타입이 들어갈 필요는 없다&#46; 
    - 구분을 할 수 있다는게 중점이다&#46;
