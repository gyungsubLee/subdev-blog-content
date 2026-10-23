---
order: 12
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 348eda9b-0fe1-80c2-b120-d3eff4e29738
title: "검색 키워드가 포함된 데이터 조회: [match]"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 346eda9b-0fe1-8009-8dce-dab63413d77f
    title: ElasticSearch
  - id: 346eda9b-0fe1-805b-bb2f-c81770700aff
    title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
  - id: 348eda9b-0fe1-80c2-b120-d3eff4e29738
    title: "검색 키워드가 포함된 데이터 조회: [match]"
excerpt: "목차 - 검색 키워드가 포함된 데이터 조회: match - 검색 키워드가 포함된 데이터를 조회하고 싶을 때: match 검색 키워드가 포함된 데이터 조회: match --- 📖 match 쿼리는 검색 키워드가 포함된 모든 도큐먼트를 조회한다. - text 타입의 필드에서만 사용한다. - keyword,long, inte"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 346eda9b-0fe1-805b-bb2f-c81770700aff
created: 2026-04-20T01:37:29.391Z
updated: 2026-04-22T04:51:25.271Z
legacy_path: Main/ElasticSearch-dab63413d77f/[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)-c81770700aff/검색 키워드가 포함된 데이터 조회- [match]-d3eff4e29738/index.md
legacy_category: ElasticSearch
source_url: https://beautiful-college-c84.notion.site/348eda9b0fe180c2b120d3eff4e29738
---
> 
> 
> <a id="348eda9b0fe180c691a1f6d14624d281"></a>
> 
> 목차
> 
> - [검색 키워드가 포함된 데이터 조회: match](#348eda9b0fe180aea4fffdca3721aaa1)
> - [검색 키워드가 포함된 데이터를 조회하고 싶을 때: match](#349eda9b0fe18091ab09c083e7c963b4)

<a id="348eda9b0fe180aea4fffdca3721aaa1"></a>

## 검색 키워드가 포함된 데이터 조회&#58; <code>match</code>

---

> 📖 
> 
> <a id="349eda9b0fe18084a550f2f40ab720a2"></a>
> 
> <code>match</code> 쿼리는 <strong>검색 키워드가 포함된 모든 도큐먼트를 조회</strong>한다&#46;
> 
> - <strong><u>text 타입의 필드</u></strong>에서만 사용한다&#46;
> 
> - <strong><code>keyword</code></strong><strong>,</strong><strong><code>long</code></strong><strong>, </strong><strong><code>integer</code></strong><strong>와 같은 타입의 필드</strong>에서는 <strong><u>사용하지 않</u></strong>는다&#46;

<a id="349eda9b0fe18091ab09c083e7c963b4"></a>

### 검색 키워드가 포함된 데이터를 조회하고 싶을 때&#58; <code>match</code>

<details>
<summary><strong>1&#46; 인덱스 생성 및 매핑 정의</strong></summary>

<a id="349eda9b0fe180d28c1bf868cc3c757b"></a>

```json
DELETE /boards

PUT /boards
{
  "mappings": {
    "properties": {
      "title": {
        "type": "text"
      }
    }
  }
}
```

![](a16393b8e300205a.webp)

</details>

<details>
<summary><strong>2&#46; 데이터 삽입</strong></summary>

<a id="349eda9b0fe1800da3a0df8f87cf2af4"></a>

```json
POST /boards/_doc
{
  "title": "편의점 과자 내돈내산 후기"
}
```

![](0792b160aa95bb92.webp)

</details>

<details>
<summary><strong>3&#46; 도큐먼트 검색</strong></summary>

<a id="349eda9b0fe180939963de93c7013aa8"></a>

```json
GET /boards/_search
{
  "query": {
    "match": {
      "title": "편의점 후기" 
    }
  }
}
```

![](4b4c9d41c0b8e932.webp)

</details>
