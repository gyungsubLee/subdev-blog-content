---
order: 12
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8167-a9c7-f03c520be861
title: 캐시 ( Cache ), 캐싱 ( Cachig )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81b8-a968-f6b1b2a79b94
    title: Redis
  - id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
    title: 비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]
  - id: 1c3eda9b-0fe1-8167-a9c7-f03c520be861
    title: 캐시 ( Cache ), 캐싱 ( Cachig )
excerpt: 캐시 ( Cache ) --- ✏️ 캐시(Cache)란, 원본 저장소보다 빠르게 가져올 수 있는 임시 데이터 저장소를 의미한다. - 캐시(Cache)라는 단어는 전반적인 개발 분야에서 통용돼서 쓰인다. ex) 캐싱 ( Caching ) --- ✏️ 캐싱(Caching)이란 캐시(Cache, 임시 데이터 저장소)에 접근해서
cover: null
icon: null
notionProperties:
  Tags: Ch 3,캐싱 전략
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
created: 2025-03-27T07:47:52.770Z
updated: 2025-03-27T07:47:52.770Z
legacy_path: Main/Redis-f6b1b2a79b94/비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]-cfbc9fd6e83a/캐시 ( Cache ), 캐싱 ( Cachig )-f03c520be861/index.md
legacy_category: Redis
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18167a9c7f03c520be861
---
<a id="1c3eda9b0fe18101b455d56cfc873b3f"></a>

## 캐시 ( Cache )

---

![](275743a57accd7cd.webp)

> ✏️ 
> 
> <a id="1c3eda9b0fe1810d8fdeec13eeb9ab3e"></a>
> 
> <strong><code>캐시(Cache)</code></strong>란, <strong>원본 저장소보다 빠르게 가져올 수 있는 임시 데이터 저장소</strong>를 의미한다&#46; 
> 
> - 캐시(Cache)라는 단어는 전반적인 개발 분야에서 통용돼서 쓰인다&#46; 

<details>
<summary>ex)</summary>

![](606b926d28e18db1.webp)

</details>

<a id="1c3eda9b0fe181e78901ddf4b4d7cc4e"></a>

## 캐싱 ( Caching )

---

> ✏️ 
> 
> <a id="1c3eda9b0fe18120af14d4fddf80e3bc"></a>
> 
> <strong><code>캐싱(Caching)</code></strong>이란 <strong><u>캐시(Cache, 임시 데이터 저장소)에 접근</u></strong><strong>해서 </strong><strong><u>데이터를 빠르게 가져오는 방식</u></strong>을 의미한다&#46;

<a id="1c3eda9b0fe1819884acec7e8906368d"></a>

현업에서는 아래와 같이 얘기하는 편이다&#46; 

> “이 API는 응답 속도가 너무 느린데? 이 응답 데이터는 <strong><code>캐싱(Cahing)</code></strong><strong> </strong>해두고 쓰는 게 어때?’ 

<a id="1c3eda9b0fe1818f92effc0f0f586894"></a>

이 말을 풀어서 설명하자면 

> ‘<strong><u>API 응답 결과</u></strong>를 원본 저장소보다 빠르게 가져올 수 있는 <strong><u>임시 데이터 저장소에 저장</u></strong>해두고, <strong><u>빠르게 조회할 수 있게 만</u></strong>드는 게 어때?<strong>’</strong>

<a id="1c3eda9b0fe181f9bee4fb098fcac91b"></a>

라는 의미이다&#46;
