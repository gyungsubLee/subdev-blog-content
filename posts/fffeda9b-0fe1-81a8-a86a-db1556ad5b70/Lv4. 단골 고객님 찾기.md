---
order: 97
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: fffeda9b-0fe1-81a8-a86a-db1556ad5b70
title: Lv4. 단골 고객님 찾기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: fffeda9b-0fe1-81a8-a86a-db1556ad5b70
    title: Lv4. 단골 고객님 찾기
excerpt: 📖 SQL의 기본적인 쿼리문을 작성할 수 있다면, 달리기반 과제에 도전해보아요. 단순 문법을 사용하는 것 뿐 아니라 내가 정말 원하는 데이터를 출력하기 위한 한 걸음이 될 거예요! 💪🏻과제를 수행하고나 나면 할 수 있어요! - LEFT JOIN을 사용해 기본 테이블에 결합하고, 주문이 없는 고객도 포함하는 방법을 익
cover: null
icon: 🛍️
notionProperties: {}
schema_version: 1
parent_id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
created: 2024-09-23T11:03:34.061Z
updated: 2024-09-23T11:04:12.791Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/Lv4. 단골 고객님 찾기-db1556ad5b70/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/fffeda9b0fe181a8a86adb1556ad5b70
---
> 📖 SQL의 기본적인 쿼리문을 작성할 수 있다면, 달리기반 과제에 도전해보아요&#46; <br>단순 문법을 사용하는 것 뿐 아니라 내가 정말 원하는 데이터를 출력하기 위한 한 걸음이 될 거예요&#33; 

<a id="fffeda9b0fe1815186c2cfca153bd800"></a>

### 💪🏻과제를 수행하고나 나면 할 수 있어요&#33;

- <code>LEFT JOIN</code>을 사용해 기본 테이블에 결합하고, 주문이 없는 고객도 포함하는 방법을 익힐 수 있다&#46;

- 고객별로 주문 건수 및 총 주문 금액을 계산할 수 있으며, 이를 <code>GROUP BY</code>와 <code>COUNT</code>, <code>SUM</code>을 사용해 처리할 수 있다&#46;

- 나라별로 가장 많은 주문 금액을 사용한 고객을 찾기 위해 서브쿼리와 <code>HAVING</code>을 결합해 조건부 집계를 수행할 수 있다&#46;

- <code>JOIN</code>, 서브쿼리, <code>GROUP BY</code>, <code>HAVING</code> 등을 조합해 복잡한 쿼리 요구사항을 해결할 수 있다&#46;

> ⚡ <strong>Notification&#58; 과제 시작 전 확인할 내용&#33;</strong>

<a id="fffeda9b0fe18108968fd4a63fbbc555"></a>

### ✅ 과제 시작 전 다음 내용을 셀프 체크해보세요&#46; 

- [ ] <code>SELECT</code>, <code>FROM</code>, <code>WHERE</code>, <code>JOIN</code> 등의 기본 문법

- [ ] <code>LEFT JOIN</code>과 <code>INNER JOIN</code>의 차이를 이해하고, 이를 활용해 테이블을 결합하는 방법

- [ ] <code>COUNT</code>, <code>SUM</code> 등의 집계 함수를 사용해 데이터를 요약하는 방법을 이해

<a id="fffeda9b0fe1812a8ba3d55b09389eca"></a>

<a href="https://beautiful-college-c84.notion.site/6969102902394ba3998014546ede7e9f">페이지</a> 

> 🍀 <strong>본격적으로 시작해 볼까요?</strong>

<a id="fffeda9b0fe181b1acd2d03f7e131410"></a>

### 문제&#58;

<a id="fffeda9b0fe1811188e9fa287304794f"></a>

<strong>Orders</strong> 테이블&#58;

| OrderID | CustomerID | OrderDate | TotalAmount |
| --- | --- | --- | --- |
| 101 | 1 | 2024&#45;01&#45;01 | 150 |
| 102 | 2 | 2024&#45;01&#45;03 | 200 |
| 103 | 1 | 2024&#45;01&#45;04 | 300 |
| 104 | 3 | 2024&#45;01&#45;04 | 50 |
| 105 | 2 | 2024&#45;01&#45;05 | 80 |
| 106 | 4 | 2024&#45;01&#45;06 | 400 |

<a id="fffeda9b0fe181b486b8e4c321df2cab"></a>

<strong>Customers</strong> 테이블&#58;

| CustomerID | CustomerName | Country |
| --- | --- | --- |
| 1 | Alice | USA |
| 2 | Bob | UK |
| 3 | Charlie | USA |
| 4 | David | Canada |

<a id="fffeda9b0fe18163971ddfa9f31b6dc8"></a>

### 요구사항&#58;

1. 고객별로 주문 건수와 총 주문 금액을 조회하는 SQL 쿼리를 작성해주세요&#46; 
    1. 출력 결과에는 고객 이름, 주문 건수, 총 주문 금액이 포함되어야 합니다&#46; 단, 주문을 한 적이 없는 고객도 결과에 포함되어야 합니다&#46;

    1. 기대결과
        | CustomerName | OrderCount | TotalSpent |
        | --- | --- | --- |
        | Alice | 2 | 450 |
        | Bob | 2 | 280 |
        | Charlie | 1 | 50 |
        | David | 1 | 400 |

1. 나라별로 총 주문 금액이 가장 높은 고객의 이름과 그 고객의 총 주문 금액을 조회하는 SQL 쿼리를 작성해주세요&#46;
    1. 기대결과
        | Country | Top&#95;Customer | Top&#95;Spent |
        | --- | --- | --- |
        | USA | Alice | 450 |
        | UK | Bob | 280 |
        | Canada | David | 400 |

<a id="fffeda9b0fe181c59c5bce093b244aa7"></a>

### 제약사항&#58;

- 두 쿼리 모두 서브쿼리, <code>JOIN</code>, <code>GROUP BY</code>, <code>HAVING</code> 등을 사용해 풀 수 있어야 한다&#46;

- 주문을 한 적이 없는 고객도 첫 번째 쿼리 결과에 포함되어야 한다&#46;

> 🔥 <strong>완료하셨다면?</strong>

- <strong>원활하게 작동되는 정답코드를 퀘스트로 제출해주세요 👉 </strong><strong><a href="https://forms.gle/pomadzyiNKAyw4CB8">https&#58;//forms&#46;gle/pomadzyiNKAyw4C</a></strong>
