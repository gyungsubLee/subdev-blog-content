---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: fffeda9b-0fe1-811b-8719-d035f3367370
title: 2) 이제 좀 벌었으니 flex 한 번 해볼까요?!
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 10aeda9b-0fe1-80c3-9114-e5ad96c892b3
    title: 1) SQL 문법 연습
  - id: fffeda9b-0fe1-811b-8719-d035f3367370
    title: 2) 이제 좀 벌었으니 flex 한 번 해볼까요?!
excerpt: ⚡ 실제 데이터 베이스를 연결하기 전, SQL 문법을 탄탄하게 다져봅시다. 여러분이 구매하고 싶은 상품들의 정보가 있는 products(상품) 테이블이 아래에 있습니다. | | | | | | --- | --- | --- | --- | | id | product_name | price | category | | 1 | 맥북
cover: null
icon: 🤩
notionProperties: {}
schema_version: 1
parent_id: 10aeda9b-0fe1-80c3-9114-e5ad96c892b3
created: 2024-09-23T11:02:03.427Z
updated: 2024-09-25T12:08:02.111Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/1) SQL 문법 연습-e5ad96c892b3/2) 이제 좀 벌었으니 flex 한 번 해볼까요-!-d035f3367370/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/fffeda9b0fe1811b8719d035f3367370
---
> ⚡ <strong>실제 데이터 베이스를 연결하기 전, SQL 문법을 탄탄하게 다져봅시다&#46; </strong>

<a id="fffeda9b0fe18181a66cc880fa9a0c03"></a>

여러분이 구매하고 싶은 상품들의 정보가 있는 products(상품) 테이블이 아래에 있습니다&#46;

|  |  |  |  |
| --- | --- | --- | --- |
| id | product&#95;name | price | category |
| 1 | 맥북 프로 | 1200 | 컴퓨터 |
| 2 | 다이슨 청소기 | 300 | 생활가전 |
| 3 | 갤럭시탭 | 600 | 컴퓨터 |
| 4 | 드롱기 커피머신 | 200 | 주방가전 |

1. <strong><code>products</code></strong> 테이블에서 제품 이름(product&#95;name)과 가격(price)만을 선택하는 쿼리를 작성해주세요&#46;

<a id="fffeda9b0fe181789526f858a7781b48"></a>

```sql
select product_name '제품명',
		   price '가격'
from products
```

1. <strong><code>products</code></strong> 테이블에서 제품 이름에 &#39;프로&#39;가 포함된 모든 제품을 선택하는 쿼리를 작성해주세요&#46;

<a id="10ceda9b0fe180709d2ac3c5ed595e81"></a>

```sql
select *
from products
where product_name like '%프로%'
```

1. <strong><code>products</code></strong> 테이블에서 제품 이름이 &#39;갤&#39;로 시작하는 모든 제품을 선택하는 쿼리를 작성해주세요&#46;

<a id="10ceda9b0fe180cca6bbf1cb2517e80c"></a>

```sql
select
from products
where product_name like '%갤%'
```

1. <strong><code>products</code></strong> 테이블에서 모든 제품을 구매하기 위해 필요한 돈을 계산하는 쿼리를 작성해주세요&#46;

<a id="10ceda9b0fe180f49dbcc1a80b5baebc"></a>

```sql
select sum(price) '총 구매 가격'
from products
```

> 🔥 <strong>과제를 완료했다면?</strong>

- 모든 문제의 raw 코드를 퀘스트로 제출해주세요&#46; 👉 <a href="https://forms.gle/B3wtrGwCncczskzR9">https&#58;//forms&#46;gle/B3wtrGwCncczskzR9</a>
