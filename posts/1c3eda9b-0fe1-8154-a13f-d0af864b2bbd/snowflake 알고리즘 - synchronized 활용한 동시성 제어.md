---
order: 21
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8154-a13f-d0af864b2bbd
title: snowflake 알고리즘 - synchronized 활용한 동시성 제어
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-8154-a13f-d0af864b2bbd
    title: snowflake 알고리즘 - synchronized 활용한 동시성 제어
excerpt: "‣ 질문 - 질문1) snowflake 알고리즘에서 synchronized를 활용하여 동시성 제어를 하는데, 만약 각 도메인 모듈마다 멀티 서버를 구상한다면 동시성 제어가 가능한가요? - 질문2) 만약 안된다면, redis 와 같은 외부 미들웨어를 통해서 동시성제어를 하는 방식으로 해당 알고리즘을 수정해야 될까요? 답변 "
cover: null
icon: null
notionProperties:
  Tags: 🧐 질문
  상태: 의문점 정리 필요
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.661Z
updated: 2025-03-27T07:52:18.661Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/snowflake 알고리즘 - synchronized 활용한 동시성 제어-d0af864b2bbd/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18154a13fd0af864b2bbd
---
<a id="1c3eda9b0fe181eeac1fdb596d9be7ef"></a>

‣

<a id="1c3eda9b0fe1810ea0cde66dc94e9d4f"></a>

### 질문

- 질문1) snowflake 알고리즘에서 synchronized를 활용하여 동시성 제어를 하는데,
    <a id="1c3eda9b0fe1819cb169f3da47a861f2"></a>

    만약 각 도메인 모듈마다 멀티 서버를 구상한다면 동시성 제어가 가능한가요?

- 질문2) 만약 안된다면, redis 와 같은 외부 미들웨어를 통해서 동시성제어를 하는 방식으로 해당 알고리즘을 수정해야 될까요?

<a id="1c3eda9b0fe181769722f6487226753d"></a>

### 답변 

![](0713cefb5def638d.webp)

![](5e658bcc160f1172.webp)

<a id="1c3eda9b0fe181d09c3bd42b3f6b0daa"></a>

### 정리 

<a id="1c3eda9b0fe1811e9d13e84d810948ef"></a>

<strong>synchronized 는 JVM 내에서 동시성제어를 하는 방법으로 단일 서버환경에서 사용은 적절하나, 분산 서버 환경에서는 동시성제어에 있어 문제가 발생된다&#46; </strong>

<a id="1c3eda9b0fe18101b77bfd2d58c38ad0"></a>

<strong>그러나 snowflake 알고리즘</strong>(총 64 비트 이뤄짐)은 노드ID를 사용하는데, 각 서버마다 고유한 노드ID를 가진다면 <strong>synchronized  사용이 유효하다</strong>

- 극히 드문 확률로 nodeId가 동일하더라도 DB레벨에서 식별자에 대한 유니크 제약조건이 성립되기 때문에, 재처리 정도면 충분하다&#46;

<a id="1c3eda9b0fe18153badbd9528e51848c"></a>

<strong>각 서버가 고유의 ID를 가지지 않는다면 외부 미들웨어(redis …)를 사용하여 관리할 필요성이 있다&#46;</strong>

- 위에서 설명했듯이 재처리만으로 충분하다&#46; ( 검증 필요 )
