---
order: 28
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 348eda9b-0fe1-8085-ad6e-eb586c89df9b
title: 기본 애널라이저 (Standard Analyzer)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 346eda9b-0fe1-8009-8dce-dab63413d77f
    title: ElasticSearch
  - id: 346eda9b-0fe1-805b-bb2f-c81770700aff
    title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
  - id: 348eda9b-0fe1-8085-ad6e-eb586c89df9b
    title: 기본 애널라이저 (Standard Analyzer)
excerpt: 목차 - 기본 애널라이저 (Standard Analyzer) - standard analyzer 표현 방식 - 예제 - standard analyzer 적용 기본 애널라이저 (Standard Analyzer) --- ✏️ Elasticsearch에서 제공하는 애널라이저로는 standard, simple, whitespac
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 346eda9b-0fe1-805b-bb2f-c81770700aff
created: 2026-04-20T08:50:10.938Z
updated: 2026-04-21T03:24:06.192Z
legacy_path: Main/ElasticSearch-dab63413d77f/[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)-c81770700aff/기본 애널라이저 (Standard Analyzer)-eb586c89df9b/index.md
legacy_category: ElasticSearch
source_url: https://beautiful-college-c84.notion.site/348eda9b0fe18085ad6eeb586c89df9b
---
> 
> 
> <a id="348eda9b0fe180178808ebdf758f6012"></a>
> 
> 목차
> 
> - [기본 애널라이저 (Standard Analyzer) ](#348eda9b0fe180f8867dd1830d9253a6)
> - [ standard analyzer 표현 방식](#348eda9b0fe180268966c3b2c2056470)
> - [ 예제 - standard analyzer 적용](#348eda9b0fe18000ba28f20dbf230e8e)

<a id="348eda9b0fe180f8867dd1830d9253a6"></a>

## 기본 애널라이저 (Standard Analyzer) 

---

> ✏️ 
> 
> <a id="348eda9b0fe180f9b859f474a5b71aa1"></a>
> 
> Elasticsearch에서 제공하는 애널라이저로는 <code>standard</code>, <code>simple</code>, <code>whitespace</code> 등 다양한 종류가 있으며 그 중 <strong><u>기본값</u></strong>으로 설정되어 있는 애널라이저는 <strong><u>standard analyzer</u></strong>이다&#46; 

![](4ac7c71600ead0c2.webp)

- <code>tokenizer(standard)</code> &#58; 공백 또는 <code>,</code>, <code>&#46;</code>, <code>&#33;</code>, <code>?</code>와 같은 문장 부호를 기준으로 문자열을 자름

- <code>token filter(lowercase)</code> &#58; 소문자로 변환

<a id="348eda9b0fe180268966c3b2c2056470"></a>

###  standard analyzer 표현 방식

<a id="348eda9b0fe1808088c3c38f6b65f71d"></a>

```json
// 방법 1
"analyzer": "standard"
```

<a id="349eda9b0fe1803198ced546f4cefe90"></a>

```json
// 방법 2
"char_filter": [], 
"tokenizer": "standard", 
"filter": ["lowercase"]
```

- Elasitcsearch에서 standard analyzer를 표현하는 방식은 크게 2가지가 있다&#46;

<a id="348eda9b0fe18000ba28f20dbf230e8e"></a>

###  예제 &#45; standard analyzer 적용

- 예제 &#45; 도큐먼트 3개 생성
    <a id="348eda9b0fe180e89565ec37952d9898"></a>

    ```json
    POST /products/_create/1
    {
      "name": "Apple 2025 맥북 에어 13 M4 10코어"
    }
    ```

    <a id="349eda9b0fe1804e82b8cb82d8ed2ac4"></a>

    ```json
    POST /products/_create/2
    {
      "name": "Apple 2024 에어팟 4세대"
    }
    ```

    <a id="349eda9b0fe1809b86dce0b499fa18e3"></a>

    ```json
    POST /products/_create/3
    {
      "name": "Apple 2024 아이패드 mini A17 Pro"
    }
    ```

- <strong>&#91;1단계&#93; character filter ❌</strong>


- <strong>&#91;2단계&#93; standard tokenizer</strong>
    > 공백 또는 <code>,</code>, <code>&#46;</code>, <code>&#33;</code>, <code>?</code>와 같은 문장 부호를 기준으로 문자열을 자름

    | <strong>토큰(token)</strong> | 도큐먼트 id |
    | --- | --- |
    | Apple | &#91;1, 2, 3&#93; |
    | 2025 | &#91;1&#93; |
    | 맥북 | &#91;1&#93; |
    | 에어 | &#91;1&#93; |
    | 13 | &#91;1&#93; |
    | M4 | &#91;1&#93; |
    | 10코어 | &#91;1&#93; |
    | 2024 | &#91;2, 3&#93; |
    | 에어팟 | &#91;2&#93; |
    | 4세대 | &#91;2&#93; |
    | 아이패드 | &#91;3&#93; |
    | mini | &#91;3&#93; |
    | A17 | &#91;3&#93; |
    | Pro | &#91;3&#93; |

- <strong>&#91;3단계&#93; lowercase</strong>
    > 소문자로 변환

    | 토큰(token) | 도큐먼트 id |
    | --- | --- |
    | <strong>apple</strong> | &#91;1, 2, 3&#93; |
    | 2025 | &#91;1&#93; |
    | 맥북 | &#91;1&#93; |
    | 에어 | &#91;1&#93; |
    | 13 | &#91;1&#93; |
    | <strong>m4</strong> | &#91;1&#93; |
    | 10코어 | &#91;1&#93; |
    | 2024 | &#91;2, 3&#93; |
    | 에어팟 | &#91;2&#93; |
    | 4세대 | &#91;2&#93; |
    | 아이패드 | &#91;3&#93; |
    | mini | &#91;3&#93; |
    | <strong>a17</strong> | &#91;3&#93; |
    | <strong>pro</strong> | &#91;3&#93; |
