---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81c7-a804-da38fe09f8b6
title: Redis 개념, 장점, 사례
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81b8-a968-f6b1b2a79b94
    title: Redis
  - id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
    title: 비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]
  - id: 1c3eda9b-0fe1-81c7-a804-da38fe09f8b6
    title: Redis 개념, 장점, 사례
excerpt: Redis --- 📖 레디스(Redis)는 Remote Dictionary Server의 약자로서, 키-값 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 비관계형 데이터베이스 관리 시스템(DBMS)이다. ⇒ 데이터 처리 속도가 엄청 빠른 NoSQL 데이터베이스 Redis 장점 다양한 장점을 가지고 있지
cover: null
icon: null
notionProperties:
  Tags: Ch 1,기본 개념
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
created: 2025-03-27T07:47:52.772Z
updated: 2025-03-27T07:47:52.772Z
legacy_path: Main/Redis-f6b1b2a79b94/비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]-cfbc9fd6e83a/Redis 개념, 장점, 사례-da38fe09f8b6/index.md
legacy_category: Redis
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181c7a804da38fe09f8b6
---
<a id="1c3eda9b0fe18179a5dede37c2039be4"></a>

## Redis

---

> 📖 
> 
> <a id="1c3eda9b0fe18136a796e1e200ec4f1d"></a>
> 
> <strong><u>레디스(Redis)</u></strong>는 <code>Remote Dictionary Server</code>의 약자로서, <code>키&#45;값</code> 구조의 <u>비정형 데이터를 저장하고 관리</u>하기 위한 오픈 소스 기반의 비관계형 데이터베이스 관리 시스템(DBMS)이다&#46; 
> 
> <a id="1c3eda9b0fe181d3973ff75dfaec938b"></a>
> 
> ⇒ <strong>데이터 </strong><strong><u>처리 속도가 엄청 빠른 NoSQL 데이터베이스</u></strong>

<details>
<summary>Redis 장점</summary>

<a id="1c3eda9b0fe1812fa69ccf90d396540f"></a>

다양한 장점을 가지고 있지만, 아래 1가지가 가장 중요하다&#46; 

> ✏️ 
> 
> <a id="1c3eda9b0fe18138aeb6db19e9a78ec7"></a>
> 
> <strong>레디스(Redis)</strong>는 <strong><u>인메모리(in&#45;memory)에 모든 데이터를 저장</u></strong>한다&#46; 
> 
> <a id="1c3eda9b0fe1810886d7f746a36bdd85"></a>
> 
> 따라서<strong><u> 데이터 처리 성능이 굉장히 빠르다&#46;</u></strong>
> 
> - 그만큼 <strong>비용이 크</strong>다&#46; 

<a id="1c3eda9b0fe1814e8fecf7c82a0eacc2"></a>

<strong>MySQL과 같은 </strong><strong><u>RDBMS의 데이터베이스</u></strong>는 대부분 <strong>디스크(Disk)에 데이터를 저장</strong>한다&#46; 

<a id="1c3eda9b0fe18101baafe185e5fb1004"></a>

하지만 <strong>Redis</strong>는 <u>메모리(RAM)에 데이터를 저장</u>하기 때문에, <strong><u>속도가 월등히 빠르다&#46; </u></strong>

- <strong>디스크(Disk)</strong>보다<u> </u><strong><u>메모리(RAM)</u></strong>에서의 <strong><u>데이터 처리속도</u></strong>가 <strong><u>월등하게 빠르다&#46;</u></strong>

- 따라서 그만큼 비용이 비싸다&#46; 

</details>

<details>
<summary>주요 사용 사례</summary>

> ✏️ 
> 
> <a id="1c3eda9b0fe18196804ac3653167ed67"></a>
> 
> <strong>주요 사용 사례</strong>
> 
> - 캐싱 (Caching)
> 
> - 세션 관리 (Session Management)
> 
> - 실시간 분석 및 통계 (Real&#45;time Analystics)
> 
> - 메시지 큐 (Message Queue)
> 
> - 지리공간 인덱싱 (Geospatial Indexing)
> 
> - 속도 제한 (Rate Limiting)
> 
> - 실시간 채팅 및 메시징 (Real&#45;time Chat And Messaging)

<a id="1c3eda9b0fe181c0ae58e2c9d5ab83e7"></a>

레디스(Redis)에 내장된 기능이 다양하다보니 여러 용도로 사용된다

<a id="1c3eda9b0fe1817e8534e6dae70fdaa8"></a>

레디스를 처음 배우는 입장에서 이 모든 사례를 익히려고 하면 막막할 수 밖에 없다&#46; 따라서 파레토의 법칙에 의해, 해당 강의에서는 <strong><u>현업에서 많이 사용</u></strong>되는 ‘<strong><u>캐싱(데이터 조회 성능 향상)</u></strong>’만 집중적으로 학습한다&#46; 

<a id="1c3eda9b0fe18176aaece83db3624fc7"></a>

‘캐싱(데이터 조회 성능 향상)’의 사례를 학습하다보면 자연스럽게 레디스의 기본 기능들이 익혀진다&#46;

<a id="1c3eda9b0fe181e8bd09c84224c67a6a"></a>

이렇게 배우면 레디스를 정말 빨리 익힐 수 있다&#46;

<a id="1c3eda9b0fe18180a870d731902ea1b0"></a>

그런 뒤에 레디스의 다른 사례에 대해서도 조금씩 학습하면서 살을 붙여나가는 것을 추천한다&#46; 

</details>

<details>
<summary>✅ 백엔드 채용 공고에 종종 등장하는 <strong><u>‘대용량 트래픽 처리 경험’</u></strong>, <strong><u>‘Redis 사용 경험’</u></strong></summary>

> ☝🏻 
> 
> <a id="1c3eda9b0fe1815ebf3fe4ab36acd179"></a>
> 
> 백엔드 개발자 채용 공고를 살펴보면 ‘<strong><u>대용량 트래픽</u></strong>’에 관한 얘기와 ‘<strong><u>NoSQ</u></strong><strong><u>L</u></strong>’에 관한 얘기가 자주 나온다&#46; <br>해당 역량은 서비스가 점점 고도화 될 수록 빼놓을 수 없는 부분이다&#46; 
> 
> <a id="1c3eda9b0fe1810ca613fa8fe7cac202"></a>
> 
>  ⇒ 이 2가지 역량을 만족하는 기술이 <code>Redis</code> 이다&#46;

<a id="1c3eda9b0fe1815c91e0fe3772035e37"></a>

<strong><u>대용량 트래픽을 처리</u></strong>하기 위해서 필수적으로 사용되는 기능이 <code>Redis의 캐싱(Caching)</code> 기능이다&#46;

<a id="1c3eda9b0fe1810790fedf1238b4c46b"></a>

또한 Redis는 NoSQL의 일종이다&#46;

</details>
