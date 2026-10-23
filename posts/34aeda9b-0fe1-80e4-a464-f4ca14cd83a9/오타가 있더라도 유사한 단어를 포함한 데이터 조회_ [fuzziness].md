---
order: 10
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 34aeda9b-0fe1-80e4-a464-f4ca14cd83a9
title: "오타가 있더라도 유사한 단어를 포함한 데이터 조회: [fuzziness]"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 346eda9b-0fe1-8009-8dce-dab63413d77f
    title: ElasticSearch
  - id: 346eda9b-0fe1-805b-bb2f-c81770700aff
    title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
  - id: 34aeda9b-0fe1-80e4-a464-f4ca14cd83a9
    title: "오타가 있더라도 유사한 단어를 포함한 데이터 조회: [fuzziness]"
excerpt: "목차 - 오타가 있더라도 유사한 단어를 포함한 데이터 조회: fuzziness - 오타가 있더라도 유사한 단어를 포함한 데이터를 조회하고 싶을 때 오타가 있더라도 유사한 단어를 포함한 데이터 조회: fuzziness --- 📖 구글 검색을 보면 오타가 발생되어도 사용자가 원하는 데이터가 잘 검색된다. 이와 같이 오타가 "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 346eda9b-0fe1-805b-bb2f-c81770700aff
created: 2026-04-22T04:56:18.146Z
updated: 2026-04-22T08:12:11.054Z
legacy_path: Main/ElasticSearch-dab63413d77f/[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)-c81770700aff/오타가 있더라도 유사한 단어를 포함한 데이터 조회- [fuzziness]-f4ca14cd83a9/index.md
legacy_category: ElasticSearch
source_url: https://beautiful-college-c84.notion.site/34aeda9b0fe180e4a464f4ca14cd83a9
---
> 
> 
> <a id="34aeda9b0fe1813e9d09c59736d808a4"></a>
> 
> 목차
> 
> - [오타가 있더라도 유사한 단어를 포함한 데이터 조회: fuzziness](#34aeda9b0fe1814089b4ec5f94354200)
> - [오타가 있더라도 유사한 단어를 포함한 데이터를 조회하고 싶을 때](#34aeda9b0fe181438bb1f648fd6d4720)

<a id="34aeda9b0fe1814089b4ec5f94354200"></a>

## 오타가 있더라도 유사한 단어를 포함한 데이터 조회&#58; <code>fuzziness</code>

---

> 📖 
> 
> ![](5ae4eaa5dd2a3bd9.webp)
> 
> <a id="34aeda9b0fe180de91e9f599f3176929"></a>
> 
> 구글 검색을 보면 <strong><u>오타가 발생되어도 사용자가 원하는 데이터가 잘 검색</u></strong>된다&#46; 
> 
> <a id="34aeda9b0fe18001bf28e069f6e9a7d2"></a>
> 
> 이와 같이 <strong><u>오타가 발생되어도 올바르게 검색</u></strong>되도록 하는 기능을 Elasticsearch의 <u>fuzziness 옵션을 사용</u>하면 쉽게 구현할 수 있다&#46;

<a id="34aeda9b0fe181438bb1f648fd6d4720"></a>

### 오타가 있더라도 유사한 단어를 포함한 데이터를 조회하고 싶을 때

<details>
<summary><strong>1&#46; 인덱스 생성 및 매핑 정의</strong></summary>

<a id="34aeda9b0fe1817b9c8bd8ff1b87e7c0"></a>

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

![](575cb5466fbd2c20.webp)

</details>

<details>
<summary><strong>2&#46; 데이터 삽입</strong></summary>

<a id="34aeda9b0fe18110a22fcf1566f27312"></a>

```json
POST /boards/_doc
{ "title": "elasticsearch 사용법" }
```

![](1e10e62897ddc02b.webp)

</details>

<details>
<summary><strong>3&#46; 도큐먼트 검색</strong></summary>

- ✅ 오타없이 키워드 검색
    <a id="34aeda9b0fe18182a30dd63ff98ccc17"></a>

    ```json
    GET /boards/_search
    {
      "query": {
        "match": {
          "title": "elasticsearch"
        }
      }
    }
    ```

    ![](80fd91e996ba3e1a.webp)

- ❌ 오타를 포함한 키워드 검색
    <a id="34aeda9b0fe180ba8073cc9cf3daf8a2"></a>

    ```json
    GET /boards/_search
    {
      "query": {
        "match": {
          "title": "elastiksearch"
        }
      }
    }
    ```

    ![](7e39f82f8fb22e3a.webp)

    <a id="34aeda9b0fe180bfb03cf499b05fc5b5"></a>

    위와 같이 오타가 포함된 키워드로 검색하면 아무 데이터도 조회되지 않는다&#46; 

- <strong><code>fuzziness</code></strong><strong> 옵션 적용</strong>
    <a id="34aeda9b0fe1807294dcdf5ced77e98d"></a>

    ```json
    GET /boards/_search
    {
      "query": {
        "match": {
          "title": {
            "query": "elastiksearch",
            "fuzziness": "AUTO"
          }
        }
      }
    }
    ```

    ![](c56e6155dd97c90d.webp)

    - <code>fuzziness &#58; AUTO</code> &#58; 단어 길이에 따라 오타 허용 개수를 자동으로 설정

    <a id="34aeda9b0fe180ebb113d719d068d8fc"></a>

    위와 같이  <code>fuzziness</code> 옵션을 적용하면 오타가 발생 되어도 정상 검색이 된다&#46; 

</details>
