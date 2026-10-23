---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 34aeda9b-0fe1-8000-9c83-cc80724b9874
title: 페이지네이션 (Pagination), 정렬(Sorting)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 346eda9b-0fe1-8009-8dce-dab63413d77f
    title: ElasticSearch
  - id: 346eda9b-0fe1-805b-bb2f-c81770700aff
    title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
  - id: 34aeda9b-0fe1-8000-9c83-cc80724b9874
    title: 페이지네이션 (Pagination), 정렬(Sorting)
excerpt: 목차 - 페이지네이션 (Pagination), 정렬(Sorting) - 페이지네이션 (Pagination) - 정렬 (Sorting) 페이지네이션 (Pagination), 정렬(Sorting) --- 📖 서버의 과부하를 방지하기 위해 데이터 조회 시 필수적으로 적용해야 하는 기능이 페이지네이션(Pagination)이다.
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 346eda9b-0fe1-805b-bb2f-c81770700aff
created: 2026-04-22T08:25:22.936Z
updated: 2026-04-22T08:45:06.871Z
legacy_path: Main/ElasticSearch-dab63413d77f/[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)-c81770700aff/페이지네이션 (Pagination), 정렬(Sorting)-cc80724b9874/index.md
legacy_category: ElasticSearch
source_url: https://beautiful-college-c84.notion.site/34aeda9b0fe180009c83cc80724b9874
---
> 
> 
> <a id="34aeda9b0fe1810b91abca62f3fc7f39"></a>
> 
> 목차
> 
> - [페이지네이션 (Pagination), 정렬(Sorting)](#34aeda9b0fe181869ffdd19be6316a8a)
> - [페이지네이션 (Pagination)](#34aeda9b0fe181d2a645c5cb126482dc)
> - [정렬 (Sorting)](#34aeda9b0fe18027a053ca3db450c00a)

<a id="34aeda9b0fe181869ffdd19be6316a8a"></a>

## 페이지네이션 (Pagination), 정렬(Sorting)

---

> 📖 
> 
> <a id="34aeda9b0fe1817da755e82923cf8b13"></a>
> 
> <strong><u>서버의 과부하를 방지</u></strong>하기 위해 데이터 조회 시 필수적으로 적용해야 하는 기능이 <strong><u>페이지네이션(Pagination)</u></strong>이다&#46;
> 
> <a id="34aeda9b0fe18031ab5dc14f3fe711f5"></a>
> 
>  Elasticsearch에서도 <strong><u>페이지네이션(Pagination) 기능을 지원</u></strong>한다&#46; 
> 
> <a id="34aeda9b0fe18025ac6ce3e91582a1d2"></a>
> 
> 또한 <strong><u>정렬(Sorting)</u></strong>도 지원한다&#46; 

<a id="34aeda9b0fe181d2a645c5cb126482dc"></a>

### 페이지네이션 (Pagination)

<details>
<summary><strong>1&#46; 인덱스 생성 및 매핑 정의</strong></summary>

<a id="34aeda9b0fe18148ad14d8aa6585c876"></a>

```json
DELETE /boards

PUT /boards
{
  "mappings": {
    "properties": {
      "title": { 
        "type": "text",
        "analyzer": "nori"
      },
      "likes": { "type": "long" }
    }
  }
}
```

![](ff8b6004e7d4e63c.webp)

</details>

<details>
<summary><strong>2&#46; 데이터 삽입</strong></summary>

<a id="34aeda9b0fe181daa3d0f560b5fbead4"></a>

```json
POST /boards/_doc
{
  "title": "1번 글",
  "likes": 12
}

POST /boards/_doc
{
  "title": "2번 글",
  "likes": 35
}

POST /boards/_doc
{
  "title": "3번 글",
  "likes": 1
}

POST /boards/_doc
{
  "title": "4번 글",
  "likes": 11
}

POST /boards/_doc
{
  "title": "5번 글",
  "likes": 72
}

POST /boards/_doc
{
  "title": "6번 글",
  "likes": 10
}

POST /boards/_doc
{
  "title": "7번 글",
  "likes": 5
}
```

![](8adaae31de9f5831.webp)

</details>

<details>
<summary><strong>3&#46; 페이지네이션을 적용한 검색(조회)</strong></summary>

> ✏️ 
> 
> - <code>size</code> &#58; 한 페이지에 불러올 데이터 개수 (SQL문의 <code>LIMIT</code>과 동일)
> 
> - <code>from</code> &#58; 몇 번째 데이터부터 불러올 지 (SQL문의 <code>OFFSET</code>과 동일, <code>0</code>부터 시작)
>     - <code>from</code> = (페이지 수 &#45; 1) x <code>size</code>

<a id="34aeda9b0fe181fdae0dc8d38b0cde4a"></a>

```json
// 1 페이지
GET /boards/_search
{
  "query": {
    "match": {
      "title": "글"
    }
  },
  "size": 3,
  "from": 0
}
```

![](8eaabd882ee3fa2e.webp)

<a id="34aeda9b0fe18012b9c2ed686795a8db"></a>

```json
// 2 페이지
GET /boards/_search
{
  "query": {
    "match": {
      "title": "글"
    }
  },
  "size": 3,
  "from": 3
}
```

![](54d8745966a5fb67.webp)

<a id="34aeda9b0fe180c3aa63f5fe51702452"></a>

```json
// 3 페이지
GET /boards/_search
{
  "query": {
    "match": {
      "title": "글"
    }
  },
  "size": 3,
  "from": 6
}
```

![](2ea99ba6509dd12a.webp)

</details>

<a id="34aeda9b0fe18027a053ca3db450c00a"></a>

### 정렬 (Sorting)

<details>
<summary>예시) 좋아요 수(likes) 내림차순 정렬</summary>

<a id="34aeda9b0fe18017a772e0c2f5f47788"></a>

```json
GET /boards/_search
{
  "query": {
    "match": {
      "title": "글"
    }
  },
  "sort": [
    {
      "likes": {
        "order": "desc"
      }
    }
  ]
}
```

![](1b6565e03eedc59d.webp)

</details>
