---
order: 54
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 229eda9b-0fe1-80f5-a931-ef08ae7a14ce
title: Database 개요
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 229eda9b-0fe1-80f5-a931-ef08ae7a14ce
    title: Database 개요
excerpt: "목차 - 데이터베이스 관리 시스템 - 1. RDBMS ( Relational DBMS ) - 2. NoSQL (Not Only SQL) - 3. CAP 이론 데이터베이스 관리 시스템 --- 1. RDBMS ( Relational DBMS ) ✏️ 관계형 데이터를 관리하는 DBMS - SQL: RDBMS에서 데이터를 관리하"
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-07T04:35:45.591Z
updated: 2025-07-07T17:32:08.614Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/Database 개요-ef08ae7a14ce/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/229eda9b0fe180f5a931ef08ae7a14ce
---
> 
> 
> <a id="229eda9b0fe181cd865bd1adbfc79c0a"></a>
> 
> <strong>목차</strong>
> 
> - [데이터베이스 관리 시스템](#229eda9b0fe181f2a0b7fb923fa6a197)
> - [1. RDBMS ( Relational DBMS )](#229eda9b0fe180d29eeaeead2605af50)
> - [2. NoSQL (Not Only SQL)](#229eda9b0fe180d6b164ec0e97b9f590)
> - [3. CAP 이론](#229eda9b0fe1803e8b74cb22030d4632)

<a id="229eda9b0fe181f2a0b7fb923fa6a197"></a>

## 데이터베이스 관리 시스템

---

<a id="229eda9b0fe180d29eeaeead2605af50"></a>

### 1&#46; RDBMS ( Relational DBMS )

> ✏️ 
> 
> <a id="229eda9b0fe1801687b9e9d75e9370dd"></a>
> 
> 관계형 데이터를 관리하는 DBMS
> 
> - <code>SQL</code>&#58; RDBMS에서 데이터를 관리하기 위해 설계된 언어
> 
> - ex) <code>MySQL</code>, <code>PostgreSQL</code> …

[MySQL &#58;&#58; MySQL 8&#46;4 Reference Manual &#58;&#58; 5&#46;6 Examples of Common Queries]()

<a id="229eda9b0fe180d6b164ec0e97b9f590"></a>

### 2&#46; NoSQL (Not Only SQL)

> ✏️ 
> 
> <a id="229eda9b0fe1807780ade53cb745089b"></a>
> 
> SQL을 사용하지 않는 DBMS
> 
> - ex) <code>Redis</code>, <code>MongoDB</code> …

<details>
<summary><strong>NoSQL의 등장 배경</strong></summary>

1. 웹 서비스의 폭발적인 성장
    - SNS, 온라인 쇼핑몰, IoT, 게임 등에서 <strong>수십억 건의 데이터</strong>가 실시간으로 생성됨

    - 기존 RDBMS는 <strong>수평적 확장</strong>(scale&#45;out)이 어려움

1. 다양한 형태의 데이터 등장
    - JSON, XML, 로그, 이미지, 비정형 텍스트 등 
        <a id="229eda9b0fe180b2a2d3e28908f29d00"></a>

        → 스키마 유연성 필요

    - 정해진 테이블 구조를 따르기 어려움&#46;
        - ex) 유저별로 저장되는 프로필 구조가 다를 때

1. 고가용성 및 분산 처리 요구
    - 글로벌 사용자에게 빠른 응답을 제공하려면 <strong>데이터를 여러 노드에 분산</strong>시켜야 함

    - CAP 이론에 따라 RDBMS보다 <strong>Availability</strong>에 초점을 둔 아키텍처 필요

1. <strong>성능과 확장성</strong>
    - RDB는 조인, 트랜잭션에 강하지만 <strong>수평 확장성</strong>과 <strong>쓰기 성능</strong>에 약함

    - 빅데이터 환경에서는 수천 TPS 이상을 감당해야 함 
        <a id="229eda9b0fe18046b844fe7142011a27"></a>

        → <strong>분산 아키텍처</strong> 기반 설계 필요

<a id="229eda9b0fe180f89e8fd06843ef4161"></a>

<br><br><br><br><br>

</details>

<details>
<summary><strong>NoSQL의 주요 유형</strong></summary>

| <strong>유형</strong> | <strong>설명</strong> | <strong>대표 DB</strong> |
| --- | --- | --- |
| <strong>Key&#45;Value 저장소</strong> | Key와 Value 쌍으로 저장 | Redis, DynamoDB |
| <strong>문서형(Document)</strong> | JSON, BSON 형태 문서 저장 | MongoDB, CouchDB |
| <strong>컬럼형(Column&#45;Family)</strong> | 컬럼 단위로 데이터 저장 | Cassandra, HBase |
| <strong>그래프형(Graph)</strong> | 노드 &#43; 엣지 구조의 관계 표현 | Neo4j, |

</details>

<details>
<summary>✅ <strong>NoSQL의 장점</strong></summary>

| <strong>장점</strong> | <strong>설명</strong> |
| --- | --- |
| <strong>수평 확장성 (Scale&#45;Out)</strong> | 서버 여러 대로 쉽게 분산 처리 가능 (샤딩, 클러스터링) |
| <strong>유연한 스키마</strong> | 미리 테이블 구조 정의 없이 다양한 형식의 데이터를 저장 |
| <strong>빅데이터 친화적</strong> | 대용량 데이터 저장/처리에 최적화되어 있음 |
| <strong>빠른 읽기/쓰기</strong> | RDB 대비 단순 구조로 처리 속도가 빠름 (특히 캐싱 구조에서 유리) |
| <strong>고가용성</strong> | 대부분 자동 복제, 장애 시 빠른 복구 가능 (ex&#46; MongoDB replica set |

</details>

<details>
<summary><strong>❌ NoSQL의 단점</strong></summary>

| <strong>단점</strong> | <strong>설명</strong> |
| --- | --- |
| <strong>복잡한 쿼리 미지원</strong> | JOIN, GROUP BY, 다중 트랜잭션 등 복잡한 쿼리 어려움 |
| <strong>일관성 보장 어려움</strong> | CAP 이론에서 ’C(Consistency)’를 완전히 보장하기 어려움 |
| <strong>표준화 미흡</strong> | SQL처럼 표준 쿼리 언어가 없어 사용법이 DB마다 다름 |
| <strong>데이터 중복</strong> | 정규화가 아닌 중복을 허용하는 구조 (데이터 무결성 관리 어려움) |
| <strong>학습 곡선</strong> | MongoDB, Cassandra, Redis 등 각각 특성에 따라 학습 필요 |

</details>

<details>
<summary>사용 예시</summary>

| <strong>사용 사례</strong> | <strong>추천 NoSQL</strong> |
| --- | --- |
| 실시간 캐시 | Redis |
| 유저 프로필 저장 (유동적인 구조) | MongoDB |
| IoT 센서 로그 저장 | Cassandra |
| 추천 시스템 / 소셜 네트워크 | Neo4j |
| 대용량 키&#45;밸류 저장 | DynamoDB (AWS) |

</details>

[NoSQL]()

[NoSQL이란 무엇인가요? NoSQL 데이터베이스 이해하기]()

[Data Modeling &#45; Database Manual &#45; MongoDB Docs]()

[Docs]()

[Welcome to Apache Cassandra’s documentation&#33; &#124; Apache Cassandra Documentation]()

<a id="229eda9b0fe1803e8b74cb22030d4632"></a>

### 3&#46; CAP 이론

> ✏️ 
> 
> <a id="229eda9b0fe180228101f6cc1a66cc65"></a>
> 
> <strong><code>CAP 이론</code></strong>은 <strong>분산 시스템</strong>에서 아래 3가지 요소들 중 <strong><u>동시에 2가지만 보장 가능</u></strong><strong>하다</strong>는 이론이다&#46;

<details>
<summary>3가지 요소</summary>

| <strong>요소</strong> | <strong>설명</strong> | 예시 |
| --- | --- | --- |
| <strong><code>C</code></strong><strong> – Consistency <br>(일관성)</strong> | 모든 노드에서 같은 시간에 같은 데이터가 조회됨 | A 서버에서 값을 10으로 수정하면, <strong>모든 서버가 즉시 10을 보여줌</strong> |
| <strong><code>A</code></strong><strong> – Availability <br>(가용성)</strong> | 클라이언트 요청에 대해 항상 응답이 옴 (오류가 아닌 응답) | 일부 노드에 장애가 생겨도, 정상 노드는 응답을 줌 |
| <strong><code>P</code></strong><strong> – Partition Tolerance<br> (분할 허용성)</strong> | 네트워크 단절이 발생해도 시스템이 정상 동작함 | 서버 간 통신이 끊겨도 각각의 서버는 독립적으로 동작함 |

</details>

<details>
<summary><strong>3가지 중 2가지만 보장</strong></summary>

<a id="229eda9b0fe180a38772dd1be1782ae5"></a>

<strong><u>CAP 이론</u></strong>에서는 <strong><code>P</code></strong><strong>(</strong><strong><code>Partition Tolerance</code></strong><strong>)</strong>는 분산 시스템에서 <strong>항상 필요한 전제조건</strong>으로 간주한다&#46;

<a id="229eda9b0fe180dda1ecdd9ddff42288"></a>

따라서 실제 시스템은 <strong><code>CP</code></strong>, <strong><code>AP</code></strong> 중 하나를 선택해야 하는 상황이 많다&#46;

| <strong>조합</strong> | <strong>설명</strong> | <strong>대표 시스템</strong> |
| --- | --- | --- |
| <strong><code>CP</code></strong><strong> <br>(일관성 &#43; 분할 허용)</strong> | 가용성 희생, <br>정확한 데이터 우선 | HBase, <br>MongoDB<br> (Strong Write Concern 시) |
| <strong><code>AP</code></strong><strong> <br>(가용성 &#43; 분할 허용)</strong> | 일관성 희생, <br>응답 속도 우선 | Cassandra, <br>Couchbase,<br> DynamoDB |
| <em>(CA는 실현 불가)</em> | P를 포기한 시스템은 분산 환경에 적합하지 않음 | 단일 서버형 SQL만 가능 |

</details>

> 💬 
> 
> > “만약 친구 둘과 대화 중인데 한 명의 휴대폰이 꺼졌다면,나머지 한 명에게 계속 이야기할지, 잠시 멈출지를 결정해야 함&#46;”
> 
> - <strong>Availability 유지</strong> = 꺼진 친구는 무시하고 계속 말함
> 
> <a id="229eda9b0fe180fe8ceed523efe1a8f6"></a>
> 
>        → 데이터 불일치 가능 (<code>AP</code>)
> 
> - <strong>Consistency 유지</strong> = 꺼진 친구 기다림 
> 
> <a id="229eda9b0fe180b7a17df0dac5305f16"></a>
> 
>        → 응답 지연됨 (<code>CP</code>)

[CAP theorem]()
