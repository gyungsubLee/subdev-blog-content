---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8118-adae-e182665bf45e
title: 캐싱을 통한 조회 성능 개선 전, 먼저 해야하는 것 - SQL 튜닝
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81b8-a968-f6b1b2a79b94
    title: Redis
  - id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
    title: 비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]
  - id: 1c3eda9b-0fe1-8118-adae-e182665bf45e
    title: 캐싱을 통한 조회 성능 개선 전, 먼저 해야하는 것 - SQL 튜닝
excerpt: ✏️ 데이터 조회 성능 개선 방법 - SQL 튜닝 - 캐싱 서버 활용 (Redis 등) - 레플리케이션 (Master/Slave 구조) - 샤딩 - DB 스케일업 (CPU, Memory, SSD 등 하드웨어 업그레이드) 많은 성능 개선 방법 중, 왜 ‘SQL 튜닝’을 먼저 고려해야 하는가? --- SQL 튜닝을 제외한 나
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
created: 2025-03-27T07:47:52.771Z
updated: 2025-05-11T16:02:43.049Z
legacy_path: Main/Redis-f6b1b2a79b94/비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]-cfbc9fd6e83a/캐싱을 통한 조회 성능 개선 전, 먼저 해야하는 것 - SQL 튜닝-e182665bf45e/index.md
legacy_category: Redis
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18118adaee182665bf45e
---
> ✏️ 
> 
> <a id="1c3eda9b0fe18150bf4fe8bf707c8e42"></a>
> 
> ### <strong>데이터 조회 성능 개선 방법</strong>
> 
> - SQL 튜닝
> 
> - 캐싱 서버 활용 (Redis 등)
> 
> - 레플리케이션 (Master/Slave 구조)
> 
> - 샤딩
> 
> - DB 스케일업 (CPU, Memory, SSD 등 하드웨어 업그레이드)

<a id="1c3eda9b0fe18125a05ee0caf7e49f5d"></a>

### 많은 성능 개선 방법 중,  왜 ‘SQL 튜닝’을 먼저 고려해야 하는가?

---

<a id="1c3eda9b0fe18108aae4ec8f68c3bcfb"></a>

<strong>SQL 튜닝을 제외한 </strong><strong><u>나머지 방법</u></strong>은 <strong>추가적인 시스템을 구축</strong>해야 한다&#46; 

-  추가 시스템 구축  및 관리 비용 증가

<a id="1c3eda9b0fe181dca577fcfd1419c94b"></a>

<strong><code>SQL 튜닝</code></strong>은 <strong><u>기존의 시스템 변경 없</u></strong>이 <strong><u>성능을 개선</u></strong>할 수 있다&#46;

<a id="1c3eda9b0fe181a9a29cd98265edb03a"></a>

<strong>SQL</strong><strong> 자체가 </strong><strong><u>비효율적</u></strong><strong>으로 작성</strong><strong>됐다면 </strong><strong>아무리 </strong><strong><u>시스템적으로 성능을 개선</u></strong><strong>한다고 하더라도 </strong><strong><u>한계</u></strong><strong>가 있다&#46;</strong>

<a id="1c3eda9b0fe1810da764ea783f743bf1"></a>

 SQL 튜닝을 통해 기본적으로 성능을 향상시킨다면, 시스템적인 성능 개선이 필요없거나 훨씬 간단한 개선으로 큰 성능 개선 효과를 얻을 수 있다&#46;

<a id="1c3eda9b0fe181da824cd8e9a4bfbdd1"></a>

<strong><u>DB 성능 개선 방법들</u></strong> 중 <strong><u>가장 가성비가 좋은 방법</u></strong><strong><u>이</u></strong><strong> </strong><strong><code>SQL 튜닝</code></strong><strong>이다&#46;</strong>
