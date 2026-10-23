---
order: 35
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 348eda9b-0fe1-8079-9877-d81ea7d5293e
title: Elasticsearch의 기본 용어 - 인덱스, 도큐먼트, 매핑, 필드
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 346eda9b-0fe1-8009-8dce-dab63413d77f
    title: ElasticSearch
  - id: 346eda9b-0fe1-805b-bb2f-c81770700aff
    title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
  - id: 348eda9b-0fe1-8079-9877-d81ea7d5293e
    title: Elasticsearch의 기본 용어 - 인덱스, 도큐먼트, 매핑, 필드
excerpt: 🤔 MySQL과 Elasticsearch를 비교하면서 학습하면 훨씬 더 빠르게 학습 가능하다. Elasticsearch 의 기본 용어 정리 | MySQL | Elasticsearch | | --- | --- | | 테이블(table) | 인덱스(index) | | 컬럼(column) | 필드(field) | | 레코드(
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 346eda9b-0fe1-805b-bb2f-c81770700aff
created: 2026-04-20T00:38:18.508Z
updated: 2026-04-20T01:13:39.561Z
legacy_path: Main/ElasticSearch-dab63413d77f/[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)-c81770700aff/Elasticsearch의 기본 용어 - 인덱스, 도큐먼트, 매핑, 필드-d81ea7d5293e/index.md
legacy_category: ElasticSearch
source_url: https://beautiful-college-c84.notion.site/348eda9b0fe180799877d81ea7d5293e
---
> 🤔 
> 
> <a id="348eda9b0fe180659134e3d0a584f87c"></a>
> 
> <code>MySQL</code>과 <code>Elasticsearch</code>를 비교하면서 학습하면 훨씬 더 빠르게 학습 가능하다&#46;

<a id="348eda9b0fe1808bac91dd588907e034"></a>

###  Elasticsearch 의 기본 용어 정리 

| <code>MySQL</code> | <code>Elasticsearch</code> |
| --- | --- |
| 테이블(table) | 인덱스(index) |
| 컬럼(column) | 필드(field) |
| 레코드(record), 로우(row) | 도큐먼트(document) |
| 스키마(schema) | 매핑(mapping) |

- <code>MySQL</code>
    - 데이터베이스

    - 데이터 <strong><u>저장/조회/수정/삭제(CRUD)</u></strong> 가능

    - 데이터를 저장을 위해 <strong><u>가장 먼저 </u></strong><strong><u>테이블(table)</u></strong><strong><u>을 만</u></strong>든다&#46; 

    - 테이블을 만들 때 <strong><u>어떤 유형의 데이터를 넣을 지 </u></strong><strong><u>스키마(schema)</u></strong><strong><u>를 정의</u></strong>한다&#46; 

    - <strong><u>테이블의 </u></strong><strong><u>컬럼(column)</u></strong><strong><u>에 맞게 데이터를 저장</u></strong>한다&#46; 

- <code>Elasticsearch</code>
    - 데이터베이스

    - 데이터 <strong><u>저장/조회/수정/삭제(CRUD)</u></strong> 가능

    - 데이터를 저장을 위해 <strong><u>가장 먼저 </u></strong><strong><u>인덱스(index)</u></strong><strong><u>를 만</u></strong>든다&#46; 

    - 인덱스를 만들 때 <strong><u>어떤 유형의 데이터를 넣을 지 </u></strong><strong><u>매핑(mapping)</u></strong><strong><u>을 정의</u></strong>한다&#46; 

    - <u>테이블의 </u><strong><u>필드(field)</u></strong><u>에 맞게 데이터를 저장</u>한다&#46; 

<a id="348eda9b0fe180ab92b4c04c462392f8"></a>

###  Elasticsearch 의 검색 기능

<a id="348eda9b0fe18006a6e1dea487e73f03"></a>

lasticsearch는 검색에 최적화된 기능을 많이 제공한다&#46;

- 동의어를 고려한 검색

- 오타를 고려한 검색

- 검색어 자동 완성 기능

- 검색어와 가장 관련성이 높은 순서대로 데이터를 조회하는 기능

<a id="348eda9b0fe180d59ccbdf228bfdaccc"></a>

이후 실습에서 CRUD 와 더 상세한 방법론들을 학습한다&#46;
