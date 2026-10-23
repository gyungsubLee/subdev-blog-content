---
order: 19
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1baeda9b-0fe1-80e1-b4d8-cda850397438
title: SQL 구조 2
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 108eda9b-0fe1-8075-8c0d-d40a042cccae
    title: 엑셀보다 쉽고 빠른 SQL
  - id: 1baeda9b-0fe1-80e1-b4d8-cda850397438
    title: SQL 구조 2
excerpt: "SQL 구조 마스터 - where, group by, order by --- SQL 기본 패턴 2 sql SELECT FROM WHERE GROUP BY ORDER BY [ 실습 ] 1. 구조 맞춰보기 ✏️ 1. ORDER BY SUM(delivery_time) desc 1. GROUP BY cuisine_type 1. "
cover: null
icon: null
notionProperties:
  Tags: 패턴
  상태: 완료
schema_version: 1
parent_id: 108eda9b-0fe1-8075-8c0d-d40a042cccae
created: 2025-03-18T16:37:11.389Z
updated: 2025-03-18T16:43:23.766Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/엑셀보다 쉽고 빠른 SQL-d40a042cccae/SQL 구조 2-cda850397438/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/1baeda9b0fe180e1b4d8cda850397438
---
<a id="10aeda9b0fe1806583aed28bd082779e"></a>

## SQL 구조 마스터 &#45; <code>where</code>, <code>group by</code>, <code>order by</code>

---

<a id="10aeda9b0fe1801aab76fafd51e6aac1"></a>

### <strong>SQL 기본 패턴 2</strong>

<a id="08412c5d505a4f7ebd17f3211d5d3533"></a>

```sql
SELECT
FROM
WHERE
GROUP BY
ORDER BY
```

<a id="10aeda9b0fe180d3a8a2c19180eeda74"></a>

### &#91; 실습 &#93; 

<details>
<summary>1&#46; 구조 맞춰보기</summary>

> ✏️ 
> 
> 1. ORDER BY SUM(delivery&#95;time) desc
> 
> 1. GROUP BY cuisine&#95;type
> 
> 1. WHERE day&#95;of&#95;the&#95;week=’Weekend’
> 
> 1. FROM food&#95;orders
> 
> 1. SELECT cuisine&#95;type, SUM(delivery&#95;time) total&#95;delivery&#95;time

<a id="10aeda9b0fe180bdb9abeb8168848c65"></a>

<strong>정답</strong>

<a id="10aeda9b0fe180928cf9d92493ef9ace"></a>

```sql
SELECT cuisine_type, SUM(delivery_time) total_delivery_time
FROM food_orders
WHERE day_of_the_week=’Weekend’
GROUP BY cuisine_type
ORDER BY SUM(delivery_time) DESC;
```

</details>

<details>
<summary>2&#46; 구조 맞춰보기</summary>

> ✏️ 
> 
> 1. where age between 20 and 40
> 
> 1. select age, count(name) count&#95;of&#95;name
> 
> 1. order by age 
> 
> 1. group by age
> 
> 1. from customers

<a id="083d04fb351d48ce9e8ad174c8f8e5bc"></a>

정답

<a id="10aeda9b0fe180968cb2f7bb29a1517b"></a>

```sql
SELECT age, count(name) count_of_name
FROM customers
WHERE age between 20 and 40 // 나이: 20 ~ 40
GROUP BY age
ORDER BY age (ASC) // 오름차순 정렬, 기본 값이기 때문에 생략 가능
```

</details>
