---
order: 99
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: fffeda9b-0fe1-8179-bfc7-ca54b0eabcf8
title: Lv5. 가장 많이 팔린 품목은?
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: fffeda9b-0fe1-8179-bfc7-ca54b0eabcf8
    title: Lv5. 가장 많이 팔린 품목은?
excerpt: 📖 SQL의 기본적인 쿼리문을 작성할 수 있다면, 달리기반 과제에 도전해보아요. 단순 문법을 사용하는 것 뿐 아니라 내가 정말 원하는 데이터를 출력하기 위한 한 걸음이 될 거예요! 💪🏻과제를 수행하고나 나면 할 수 있어요! - 여러 테이블 간의 관계를 이해하고 이를 조인하여 필요한 데이터를 추출할 수 있다. - 고객
cover: null
icon: 🏆
notionProperties: {}
schema_version: 1
parent_id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
created: 2024-09-23T11:03:34.061Z
updated: 2024-09-23T11:04:12.791Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/Lv5. 가장 많이 팔린 품목은--ca54b0eabcf8/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/fffeda9b0fe18179bfc7ca54b0eabcf8
---
> 📖 SQL의 기본적인 쿼리문을 작성할 수 있다면, 달리기반 과제에 도전해보아요&#46; <br>단순 문법을 사용하는 것 뿐 아니라 내가 정말 원하는 데이터를 출력하기 위한 한 걸음이 될 거예요&#33; 

<a id="fffeda9b0fe181d78321fe07a27fce82"></a>

### 💪🏻과제를 수행하고나 나면 할 수 있어요&#33;

- 여러 테이블 간의 관계를 이해하고 이를 조인하여 필요한 데이터를 추출할 수 있다&#46;

- 고객별 총 구매 금액, 주문 수, 카테고리별 최다 판매 제품 등 데이터를 다양한 기준으로 집계하는 능력을 기를 수 있다&#46;

- 특정 조건에 맞는 데이터를 서브쿼리로 추출하고, 이를 메인 쿼리의 결과에 반영하는 방법을 익힐 수 있다&#46;

- 판매 데이터를 분석하여 고객과 제품의 판매 패턴을 이해하고, 이를 SQL로 표현할 수 있다&#46;

- 복잡한 쿼리를 작성하면서 성능을 고려하여 효율적인 SQL 쿼리를 작성하는 능력을 키울 수 있다&#46;

> ⚡ <strong>Notification&#58; 과제 시작 전 확인할 내용&#33;</strong>

<a id="fffeda9b0fe1816a85b4fd3376de655c"></a>

### ✅ 과제 시작 전 다음 내용을 셀프 체크해보세요&#46; 

- [ ] <code>SELECT</code>, <code>FROM</code>, <code>WHERE</code>, <code>JOIN</code> 등의 기본 SQL 문법

- [ ] <code>INNER JOIN</code>, <code>LEFT JOIN</code> 등을 사용해 여러 테이블을 결합하는 방법

- [ ] <code>SUM</code>, <code>COUNT</code>, <code>MAX</code> 등의 집계 함수와 이를 <code>GROUP BY</code>와 함께 사용하는 방법

<a id="fffeda9b0fe181c5a8f5ce19f6b74faf"></a>

<a href="https://beautiful-college-c84.notion.site/6969102902394ba3998014546ede7e9f">페이지</a> 

> 🍀 <strong>본격적으로 시작해 볼까요?</strong>

<a id="fffeda9b0fe1819783d4c6e9ee968247"></a>

### 문제&#58;

<a id="fffeda9b0fe1815ba97bdda450830ffa"></a>

<strong>Products</strong> 테이블&#58;

| ProductID | ProductName | Category | Price |
| --- | --- | --- | --- |
| 1 | Laptop | Electronics | 1000 |
| 2 | Smartphone | Electronics | 800 |
| 3 | Headphones | Electronics | 150 |
| 4 | Coffee Maker | Home | 200 |
| 5 | Blender | Home | 100 |

<a id="fffeda9b0fe181e08735d1badd55cbbb"></a>

<strong>Orders</strong> 테이블&#58;

| OrderID | ProductID | OrderDate | Quantity | CustomerID |
| --- | --- | --- | --- | --- |
| 101 | 1 | 2024&#45;02&#45;01 | 2 | 1 |
| 102 | 3 | 2024&#45;02&#45;02 | 1 | 2 |
| 103 | 2 | 2024&#45;02&#45;03 | 1 | 1 |
| 104 | 4 | 2024&#45;02&#45;04 | 3 | 3 |
| 105 | 1 | 2024&#45;02&#45;05 | 1 | 2 |
| 106 | 5 | 2024&#45;02&#45;06 | 2 | 3 |

<a id="fffeda9b0fe18141af6ef1786e0d0a7f"></a>

<strong>Customers</strong> 테이블&#58;

| CustomerID | CustomerName | Country |
| --- | --- | --- |
| 1 | Alice | USA |
| 2 | Bob | UK |
| 3 | Charlie | USA |

<a id="fffeda9b0fe181ada049ec641d68d945"></a>

### 요구사항&#58;

1. 각 고객이 구매한 모든 제품의 총 금액을 계산하고, 고객 이름, 총 구매 금액, 주문 수를 출력하는 SQL 쿼리를 작성해주세요&#46;
    | CustomerName | TotalAmount | OrderCount |
    | --- | --- | --- |
    | Alice | 2600 | 3 |
    | Bob | 950 | 2 |
    | Charlie | 800 | 2 |

1. 각 제품 카테고리별로 가장 많이 팔린 제품의 이름과 총 판매량을 조회하는 SQL 쿼리를 작성해주세요&#46;
    | Category | Top&#95;Product | TotalSold |
    | --- | --- | --- |
    | Electronics | Laptop | 3 |
    | Home | Coffee Maker | 3 |

<a id="fffeda9b0fe1818bbc78e7187c645d7b"></a>

### 제약사항&#58;

- 두 쿼리 모두 서브쿼리, <code>JOIN</code>, <code>GROUP BY</code>, <code>HAVING</code> 등의 SQL 기능을 사용해 문제를 풀어야 합니다&#46;

- 여러 테이블 간의 관계를 명확히 이해하고, 데이터를 효율적으로 결합하는 것이 중요해요&#33;

> 🔥 <strong>완료하셨다면?</strong>

- <strong>원활하게 작동되는 정답코드를 퀘스트로 제출해주세요 👉 </strong><strong><a href="https://forms.gle/pomadzyiNKAyw4CB8">https&#58;//forms&#46;gle/pomadzyiNKAyw4C</a></strong>
