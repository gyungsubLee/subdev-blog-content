---
order: 38
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 346eda9b-0fe1-80bf-a1fd-eee30f99426f
title: Elastic search 개념 및 활용
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 346eda9b-0fe1-8009-8dce-dab63413d77f
    title: ElasticSearch
  - id: 346eda9b-0fe1-805b-bb2f-c81770700aff
    title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
  - id: 346eda9b-0fe1-80bf-a1fd-eee30f99426f
    title: Elastic search 개념 및 활용
excerpt: Elastic search --- 📖 Elasticsearch는 오픈 소스 분산, RESTful 검색 및 분석 엔진, 확장 가능한 데이터 저장소 및 벡터 데이터베이스이다. → 검색, 데이터 분석에 최적화된 데이터베이스 주요 활용 사례 1. 데이터 수집 및 분석 Elasticsearch는 대규모 데이터(ex. 로그 등)를
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 346eda9b-0fe1-805b-bb2f-c81770700aff
created: 2026-04-18T16:23:26.920Z
updated: 2026-04-18T16:31:16.627Z
legacy_path: Main/ElasticSearch-dab63413d77f/[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)-c81770700aff/Elastic search 개념 및 활용-eee30f99426f/index.md
legacy_category: ElasticSearch
source_url: https://beautiful-college-c84.notion.site/346eda9b0fe180bfa1fdeee30f99426f
---
<a id="346eda9b0fe180d5be55cff60935fb13"></a>

## Elastic search

---

> 📖 
> 
> <a id="346eda9b0fe1806db09fcd933809aeee"></a>
> 
> <code>Elasticsearch</code>는 오픈 소스 분산, RESTful 검색 및 분석 엔진, 확장 가능한 데이터 저장소 및 벡터 데이터베이스이다&#46;
> 
> <a id="346eda9b0fe18064bc3dddd5f8db62ec"></a>
> 
> →  <strong><u>검색, 데이터 분석에 최적화</u></strong>된 <strong>데이터베이스</strong>

<a id="346eda9b0fe1802c866fc78d72e618cb"></a>

### 주요 활용 사례

1. <code>데이터 수집 및 분석</code>
    <a id="346eda9b0fe180b19b3dd0862a79f8fd"></a>

    Elasticsearch는 <strong><u>대규모 데이터(ex&#46; 로그 등)를 수집 및 분석</u></strong>하는 데 최적화되어 있다&#46;<br>주로<code> Elasticsearch(데이터 저장)</code>, <code>Logstash(데이터 수집 및 가공)</code>, <code>Kibana(데이터 시각화)</code>를 같이 활용해 데이터를 수집 및 분석한다&#46;

1. <code>검색 최적화</code>
    <a id="346eda9b0fe1806a9a80e11a685a44b0"></a>

    Elasticsearch는 데이터가 많더라도 <strong><u>뛰어난 검색 속도</u></strong>를 가지고 있고, <br><strong><u>오타나 동의어를 고려해서 유연하게 검색</u></strong>할 수 있는 기능을 가지고 있다&#46; 

    - 쿠팡이나 배달의민족의 검색 기능도 전부 Elasticsearch를 활용해 구현됨
