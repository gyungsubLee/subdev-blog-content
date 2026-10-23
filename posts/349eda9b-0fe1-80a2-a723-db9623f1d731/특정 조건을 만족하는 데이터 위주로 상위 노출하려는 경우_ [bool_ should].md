---
order: 9
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 349eda9b-0fe1-80a2-a723-db9623f1d731
title: "특정 조건을 만족하는 데이터 위주로 상위 노출하려는 경우: [bool: should]"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 346eda9b-0fe1-8009-8dce-dab63413d77f
    title: ElasticSearch
  - id: 346eda9b-0fe1-805b-bb2f-c81770700aff
    title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
  - id: 349eda9b-0fe1-80a2-a723-db9623f1d731
    title: "특정 조건을 만족하는 데이터 위주로 상위 노출하려는 경우: [bool: should]"
excerpt: "목차 - 특정 조건을 만족하는 데이터 위주로 상위 노출하려는 경우: bool - should - bool must vs bool should - 예시 - [[실습] bool should를 통한 특정 문서 상위 노출](349eda9b0fe181479f56c67f7ce1c934) [5.4 Bool : Should | Elas"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 346eda9b-0fe1-805b-bb2f-c81770700aff
created: 2026-04-21T12:37:51.827Z
updated: 2026-04-22T08:12:16.939Z
legacy_path: Main/ElasticSearch-dab63413d77f/[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)-c81770700aff/특정 조건을 만족하는 데이터 위주로 상위 노출하려는 경우- [bool- shoul-db9623f1d731/index.md
legacy_category: ElasticSearch
source_url: https://beautiful-college-c84.notion.site/349eda9b0fe180a2a723db9623f1d731
---
> 
> 
> <a id="349eda9b0fe181bf8fc2c91daa4ca223"></a>
> 
> 목차
> 
> - [특정 조건을 만족하는 데이터 위주로 상위 노출하려는 경우: bool -  should](#349eda9b0fe181759614cab6b772bf53)
> - [bool must vs bool should](#34aeda9b0fe18045aae2de3a9b03a1fa)
> - [예시](#34aeda9b0fe180229d57c12b8ea726f8)
> - [[실습] bool should를 통한 특정 문서 상위 노출](#349eda9b0fe181479f56c67f7ce1c934)

[5&#46;4 Bool &#58; Should &#124; Elastic 가이드북]()

<a id="349eda9b0fe181759614cab6b772bf53"></a>

## 특정 조건을 만족하는 데이터 위주로 상위 노출하려는 경우&#58; bool &#45;  <code>should</code>

---

> 📖 
> 
> <a id="349eda9b0fe181fa9500f652b65cc1dd"></a>
> 
> Elasticsearch의 <code>bool should</code>는 여러 조건 중 하나 이상에 맞으면 되는 절? 이다&#46; 
> 
> <a id="34aeda9b0fe1803cb21df0872dbd5279"></a>
> 
> 다만 단독으로 쓰는지 <code>must</code>나 <code>filter</code>와 같이 쓰는지에 따라 동작이 달라진다&#46; 
> 
> - <code>should</code>의 조건을 충족시키는 데이터일 경우 score(점수)에 가산점을 부여해 상위 노출될 가능성이 높아진다&#46;
> 
> - bool 쿼리는 여러 하위 쿼리를 조합하는 용도이고, 그 중 should는 보통 OR 성격으로 이해하면 된다&#46; 
> 
> - 조건이 많을수록 점수(score)에 유리해질 수 있어, 관련성 높은 문서를 상위로 노출하려는 경우 많이 사용한다&#46; 

> ✏️ 
> 
> <a id="34aeda9b0fe180e9ae31f64505601f4f"></a>
> 
> 동작 방식
> 
> 1. <code>should</code>만 있으면, 기본적으로 <code>should</code> 절 중 적어도 하나는 매치되어야 한다&#46; 
> 
> 1. <code>must</code>나 <code>filter</code>와 함께 있으면, <code>should</code>는 보통 결과를 보강하는 역할을 하고 점수에 영향을 준다&#46; 
> 
> 1. <code>minimum&#95;should&#95;match</code>를 쓰면, should 절 중 몇 개를 반드시 만족해야 하는지 정할 수 있다 

> ⚠️ 
> 
> - <code>should</code>를 무조건 <code>or</code>로만 생각하면 헷갈릴 수 있다&#46; 
> 
> - 특히 <code>must</code> 와 같이 쓰면, <code>should</code>는 결과를 넓히기 보다 <strong><u>점수만 올리는 역할</u></strong>처럼 동작하는 경우가 많다&#46;

<a id="34aeda9b0fe18045aae2de3a9b03a1fa"></a>

### <code>bool must</code> vs <code>bool should</code>

<a id="34aeda9b0fe1804baff0f7e1dea341d1"></a>

must는 반드시 만족해야 하는 조건이고, should는 만족하면 더 좋지만 필수는 아닌 조건이다&#46; 

<a id="34aeda9b0fe180df8648f2da10ac0172"></a>

다만 must 와 should를 같이 쓰면 should는 보통 결과를 보강하거나 점수에 반영하는 역할을 한다&#46; 

<a id="34aeda9b0fe180eda4a1c50973d2c8d8"></a>

핵심 차이

- <code>must</code>&#58; 모든 조건을 만족해야 결과에 포함된다&#46; <code>AND</code>와 유사

- <code>should</code>&#58; 하나 이상 만족하면 유리하다&#46; <code>OR</code>처럼 이해할 수 있지만 ‘선택 조건’ 에 가깝다&#46;

<a id="34aeda9b0fe1806d9037e322d8d6f25e"></a>

즉, <code>must</code>는 주로 필수 필터링, <code>should</code>는 관련성 점수 향상에 많이 사용한다&#46; 

<a id="34aeda9b0fe180229d57c12b8ea726f8"></a>

### 예시

<details>
<summary>1&#46;  title이 ‘elasticsearch’인 문서 중에서, tags가 ‘search’ 또는 ‘ranking’인 문서를 더 상위 노출</summary>

<a id="34aeda9b0fe18018a676dcd15e1bd1d3"></a>

```json
{
	"query": {
		"bool": {
			"must": {
				{ "match": { "title": "elasticsearch" } }
			},
			"should": {
				{ "match": { "tags": "search"} },
				{ "match": { "tags": "ranking"} }
			}
		}	
	}
}
```

</details>

<details>
<summary>2&#46; 고객이 쇼핑몰에서 ‘노트북’을 검색했을 때 다음 조건을 만족하는 상품을 상위 노출</summary>

> ❗ 
> 
> <a id="34aeda9b0fe180149315f807ca2ccac9"></a>
> 
> 요구사항
> 
> - 최근 출시된 제품
> 
> - 평점이 높은 제품
> 
> - 특정 브랜드(예&#58; Apple)
> 
> <a id="34aeda9b0fe180e09f2cdaad78b943ed"></a>
> 
> 의 문서에 대해서 더 상위 검색이 가능하도록 쿼리 구성

<a id="34aeda9b0fe18091b406e04e5c29a287"></a>

```json
GET products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "multi_match": {
            "query": "노트북",
            "fields": ["name^3", "description^1", "category^2"]
          }
        }
      ],
      "should": [
        {
          "range": {
            "release_date": {
              "gte": "now-1y"
            }
          }
        },
        {
          "range": {
            "rating": {
              "gte": 4.5
            }
          }
        },
        {
          "term": {
            "brand.keyword": "Apple"
          }
        }
      ]
    }
  }
}

```

</details>

<details>
<summary>3&#46; 사용자가 “백엔드 개발자”를 검색했을 때, 다음 조건을 만족하는 상품을 상위 노출</summary>

> ❗ 
> 
> <a id="34aeda9b0fe18009b1a5d9f2e657e4df"></a>
> 
> 요구사항
> 
> - 원격 근무 가능
> 
> - 연봉 6,000만 원 이상
> 
> - 유명 기업(예&#58; 네이버, 카카오, 당근)
> 
> <a id="34aeda9b0fe18021891cf1d5dde1dab7"></a>
> 
> 의 문서에 대해서 더 상위 검색이 가능하도록 쿼리 구성

<a id="34aeda9b0fe180faa337c710377546f9"></a>

```json
GET jobs/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "multi_match": {
            "query": "백엔드 개발자",
            "fields": ["title^3", "description^1", "skills^2"]
          }
        }
      ],
      "should": [
        {
          "term": {
            "remote": true
          }
        },
        {
          "range": {
            "salary": {
              "gte": 60000000
            }
          }
        },
        {
          "terms": {
            "company.keyword": ["네이버", "카카오", "당근"]
          }
        }
      ]
    }
  }
}

```

</details>

<details>
<summary>4&#46; 사용자가 네이버에서 &#34;챗GPT&#34;로 블로그를 검색했을 때, 다음 조건을 만족하는 글을 더 상위 노출</summary>

> ❗ 
> 
> <a id="34aeda9b0fe180d3abfce79dc930e400"></a>
> 
> 요구사항
> 
> - 제목에 &#34;챗GPT&#34;가 포함된 글
> 
> - 작성일이 최근일수록
> 
> - 좋아요 수가 많은 글
> 
> <a id="34aeda9b0fe18043aa9bc918916bf9b8"></a>
> 
> 의 문서에 대해서 더 상위 검색이 가능하도록 쿼리 구성

<a id="34aeda9b0fe1801fa692f2d1b958dc0f"></a>

```json
GET blogs/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "content": "챗GPT"
          }
        }
      ],
      "should": [
        {
          "match_phrase": {
            "title": {
              "query": "챗GPT",
              "boost": 3
            }
          }
        },
        {
          "range": {
            "published_at": {
              "gte": "now-30d"
            }
          }
        },
        {
          "field_value_factor": {
            "field": "like_count",
            "factor": 1.2,
            "modifier": "log1p",
            "missing": 0
          }
        }
      ]
    }
  }
}

```

</details>

<a id="349eda9b0fe181479f56c67f7ce1c934"></a>

### &#91;실습&#93; bool should를 통한 특정 문서 상위 노출

> ❗ 
> 
> <a id="34aeda9b0fe1802cb743c660522b7d64"></a>
> 
> 요구사항
> 
> <a id="34aeda9b0fe18073949af9e6ea8c22e8"></a>
> 
> <strong><u>평점이 높</u></strong>고 <strong><u>좋아요 수가 많</u></strong>은 글을 <strong>상위 노출</strong>

<details>
<summary><strong>1&#46; 인덱스 생성 및 매핑 정의</strong></summary>

<a id="349eda9b0fe18103a89bd8c1d5615d71"></a>

```json
ELETE /products

PUT /products
{
  "mappings": {
    "properties": {
      "name":   { 
        "type": "text",
        "analyzer": "nori"
      },
      "rating": { "type": "double" },
      "likes":  { "type": "integer" }
    }
  }
```

</details>

<details>
<summary><strong>2&#46; 데이터 삽입</strong></summary>

<a id="349eda9b0fe1816b8d76d6de8436dba1"></a>

```json
// 키워드("무선 이어폰")와 관련성은 적지만, 좋아요 수가 높고, 평점이 좋은 경우
POST /products/_doc
{
  "name": "무선 충전기 C타입",
  "rating": 4.9,
  "likes": 300
}

// 키워드("무선 이어폰")와 관련성은 높지만, 좋아요 수가 낮고, 평점도 낮은 경우
POST /products/_doc
{
  "name": "소니 무선 이어폰 WF",
  "rating": 3.8,
  "likes": 15
}


// 키워드("무선 이어폰")와 관련성도 높고, 좋아요 수도 높고, 평점도 높은 경우
POST /products/_doc
{
  "name": "갤럭시 버즈2 무선 이어폰",
  "rating": 4.8,
  "likes": 310
}

// 키워드("무선 이어폰")와 관련성이 아예 없는데, 좋아요 수는 높고, 평점도 높은 경우
POST /products/_doc
{
  "name": "삼성 노트북 13인치",
  "rating": 5.0,
  "likes": 1000
}
```

</details>

<details>
<summary><strong>3&#46;1&#46; should 조건 없이 검색 </strong></summary>

<a id="349eda9b0fe181108c38f515426b8d51"></a>

```json
GET /products/_search
{
    "query": {
        "match": {
            "name": "무선 이어폰"
        }
    }
}
```

<a id="34aeda9b0fe18077b3e6d340836c7eb5"></a>

<strong>응답값</strong>

<a id="34aeda9b0fe18023b8b4d1ca304f8882"></a>

```json
{
  "took": 2,
  "timed_out": false,
  "_shards": {
    "total": 1,
    "successful": 1,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 3,
      "relation": "eq"
    },
    "max_score": 0.6409958,
    "hits": [
      {
        "_index": "products",
        "_id": "z0-AlZYBWhYNXJPWkb6p",
        "_score": 0.6409958,
        "_source": {
          "name": "소니 무선 이어폰 WF",
          "rating": 3.8,
          "likes": 15
        }
      },
      {
        "_index": "products",
        "_id": "0E-AlZYBWhYNXJPWlr56",
        "_score": 0.5863999,
        "_source": {
          "name": "갤럭시 버즈2 무선 이어폰",
          "rating": 4.8,
          "likes": 310
        }
      },
      {
        "_index": "products",
        "_id": "zk-AlZYBWhYNXJPWjb70",
        "_score": 0.12974027,
        "_source": {
          "name": "무선 충전기 C타입",
          "rating": 4.9,
          "likes": 300
        }
      }
    ]
  }
}
```

<a id="34aeda9b0fe180afb801c3e98d3e95e4"></a>

쿼리의 조건에 따라 <code>“무선 이어폰”</code> 키워드와 아예 관련이 없는 데이터는 조회되지 않았다&#46;

<a id="34aeda9b0fe180849b62d608dc52890e"></a>

저품질(평점이 낮거나 좋아요 수가 적은 상품)의 상품이 상위에 노출되었다&#46; <br>이런 경우 사용자 경험에 좋지 않을 수 있다&#46; 

<a id="34aeda9b0fe1807ea6d4e4f116e4f2cf"></a>

따라서 <code>should</code>를 활용해 저품질 상품이 상위에 노출되지 않도록 수정한다&#46; 

</details>

<details>
<summary><strong>3&#46;2&#46; should 활용하여 검색</strong></summary>

<a id="34aeda9b0fe180deb6fdc94e5a02c6b3"></a>

```json
GET /products/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "name": "무선 이어폰" 
          }
        }
      ],
      "should": [
        {
          "range": {
            "rating": {
              "gte": 4.5 // 4.5 이상의 평점의 상품일 경우 score에 가산점 부여
            }
          }
        },
        {
          "range": {
            "likes": {
              "gte": 100 // 좋아요 수가 100개 이상인 상품일 경우 score에 가산점 부여
            }
          }
        }
      ]
    }
  }
}
```

<a id="349eda9b0fe18144adc0c4b739326756"></a>

<strong>응답값</strong>

<a id="34aeda9b0fe18057bd18fdb052d6d086"></a>

```json
{
  "took": 6,
  "timed_out": false,
  "_shards": {
    "total": 1,
    "successful": 1,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 3,
      "relation": "eq"
    },
    "max_score": 2.5864,
    "hits": [
      {
        "_index": "products",
        "_id": "0E-AlZYBWhYNXJPWlr56",
        "_score": 2.5864,
        "_source": {
          "name": "갤럭시 버즈2 무선 이어폰",
          "rating": 4.8,
          "likes": 310
        }
      },
      {
        "_index": "products",
        "_id": "zk-AlZYBWhYNXJPWjb70",
        "_score": 2.1297402,
        "_source": {
          "name": "무선 충전기 C타입",
          "rating": 4.9,
          "likes": 300
        }
      },
      {
        "_index": "products",
        "_id": "z0-AlZYBWhYNXJPWkb6p",
        "_score": 0.6409958,
        "_source": {
          "name": "소니 무선 이어폰 WF",
          "rating": 3.8,
          "likes": 15
        }
      }
    ]
  }
}
```

- 1번째 데이터
    -  검색 키워드와 관련성이 높고, 평점이 좋고, 좋아요 수가 높은 상품이 가장 상위에 노출됨

- 2번째 데이터
    - 검색 키워드와 관련성이 조금 낮더라도, 평점이 좋고, 좋아요 수가 높은 상품이 2번째 키워드로 노출됨

- 3번째 데이터 
    - 검색 키워드와 관련성은 높았으나, 평점이 낮고 좋아요 수가 낮아서 하단에 배치됨

<a id="34aeda9b0fe180fbb518d1fbe0c0e7d5"></a>

이와 같이 <code>score</code>에 가산점을 주는 bool 쿼리의 <code>should</code>를 활용해 원하는 조건을 갖추고 있는 <br>데이터를 상단에 노출되게 만들 수 있다&#46; 

</details>
