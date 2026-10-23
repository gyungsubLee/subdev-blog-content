---
order: 16
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81c9-9c67-f04287601241
title: Publish / Subscribe 모델
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
    title: RabbitMQ를 이용한 비동기 아키텍처
  - id: 1c3eda9b-0fe1-81c9-9c67-f04287601241
    title: Publish / Subscribe 모델
excerpt: Publish / Subscribe 모델 --- Pub/Sub은 메세지 발행(Publish)과 구독(Subscribe)의 개념을 기반으로 하는 메세징 패턴이다. 중간 브로커(Exchagne)를 두고 이를 통해, 구독자들(Subscriber)에게 메세지를 전달한다. Queue와 exchange를 Binding 한 뒤, pu
cover: null
icon: null
notionProperties:
  Tags: 개념
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
created: 2025-03-27T07:47:43.050Z
updated: 2025-03-27T07:47:43.050Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/RabbitMQ를 이용한 비동기 아키텍처-e28e651123f1/Publish - Subscribe 모델-f04287601241/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181c99c67f04287601241
---
<a id="1c3eda9b0fe18122823ef9691be72e32"></a>

## Publish / Subscribe 모델 

---

![](a2fc857f24599abd.webp)

<a id="1c3eda9b0fe181c88789cca5d30ed2a6"></a>

<strong><code>Pub/Sub</code></strong>은 <strong><u>메세지 발행(Publish)</u></strong><strong>과 </strong><strong><u>구독(Subscribe)</u></strong><strong>의 개념을 기반으로 하는 </strong><strong><u>메세징 패턴</u></strong>이다&#46;  

<a id="1c3eda9b0fe1816ca688c5fcf5c70d29"></a>

<strong><u>중간 브로커(Exchagne)</u></strong>를 두고 이를 통해, <strong><u>구독자들(Subscriber</u></strong><strong>)에게 </strong><strong><u>메세지를 전달</u></strong>한다&#46; 

<a id="1c3eda9b0fe181d18f07cdd985415794"></a>

<strong><code>Queue</code></strong>와 <strong><code>exchange</code></strong>를 <code>Binding</code> 한 뒤, <strong><code>publisher</code></strong>에서 <strong><u>메세지</u></strong>를 <strong><u>exchange 명칭(식별자)</u></strong>과 함께 보내면, 이를 rabbitMQ에서 받아 <strong><u>Binding 된 큐로 전송</u></strong>한다&#46; <br>해당 큐는 <u>구독된 </u><strong><u><code>subsriber</code></u></strong><u>에게 메세지를 전달</u>하고, 이를 <strong><code>subscriber</code></strong>가 <u>클라이언트로 전송</u>한다&#46; 

- <strong><code>Bindin</code></strong><code>g</code>&#58; <code>exchange</code>와 <code>Queue</code>와의 관계를 정의한 <strong><u>일종의 라우팅 테이블</u></strong>

- RabbitMQ에서는 <code>Fanout Exchange</code>를 통해 <u>연결된 모든 Queue에게 메세지를 전달</u>한다&#46;  ⇒ <strong>브로드캐스트</strong>

<a id="1c3eda9b0fe1814f9fa8c5a20bb62923"></a>

### 주요 특징

| 특징 | 설명 |
| --- | --- |
| <strong><code>유연성</code></strong><strong>, </strong><strong><code>확장성</code></strong> | &#45; Subscriber를 쉽게 추가 가능<br>&#45; 각 Subscriber들은 서로 독립적으로 동작 가능 |
| <strong><code>다대다(N&#58;M) 메세징</code></strong> | &#45; 하나의 메세지가 여러 Subscriber에게 전달됨 |
| <strong><code>구독자 독립성</code></strong> | &#45; 하나의 메세지가 어떤 Subscriber에게 전달될지 알 필요 없음<br>&#45; 메세지 전달을 브로커가 처리함 |
| <strong><code>비동기 메세징</code></strong> | &#45; Publisher와 Subscriber는 서로 독립적으로 동작하며, 동시에 실행될 필요 없음 |
| <strong><code>확장성</code></strong> | &#45; 여러 Subscriber를 추가하거나 제거해도 시스템이 영향을 받지 않음 |
| <strong><code>구독 제어</code></strong> | &#45; 구독자는 특정 조건(<code>routing key</code>, <code>topic</code> …)을 기반으로 메세지를 필터링하여 수신 가능<br>&#45; <strong><code>Fanout Exchange<br></code></strong>모든 구독자에게 메세지를 브로드캐스트<code>Routing Key</code>는 필요하지 않음<br>&#45; <strong><code>Topic Exchange</code></strong><strong>, <br>&#45; </strong><strong><code>Direct Exchange</code></strong><strong><br></strong>메세지를 선택적으로 전달 가능 |
