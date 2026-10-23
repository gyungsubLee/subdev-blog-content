---
order: 9
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1baeda9b-0fe1-8088-b0dd-e15be865307f
title: Data Type 오류 해결
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 108eda9b-0fe1-8075-8c0d-d40a042cccae
    title: 엑셀보다 쉽고 빠른 SQL
  - id: 1baeda9b-0fe1-8088-b0dd-e15be865307f
    title: Data Type 오류 해결
excerpt: "Data Type 오류 해결 형변환 ( cast( … as 타입)) sql --숫자 형변환 cast(값 as decimal) --문자 형변환 cast(값 as char)) ex) 형변환( cast() ) - rating: 문자 타입 → ABC sql --숫자로 변경 cast(if(rating='Not given', '1'"
cover: null
icon: null
notionProperties:
  Tags: 형변환
  상태: 완료
schema_version: 1
parent_id: 108eda9b-0fe1-8075-8c0d-d40a042cccae
created: 2025-03-18T17:51:53.713Z
updated: 2025-04-22T15:06:43.374Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/엑셀보다 쉽고 빠른 SQL-d40a042cccae/Data Type 오류 해결-e15be865307f/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/1baeda9b0fe18088b0dde15be865307f
---
<a id="1baeda9b0fe18063a9d0eb2da117a4e0"></a>

### <strong>Data Type 오류 해결 </strong>

<details>
<summary>형변환 ( <code>cast( … as 타입)</code>)</summary>

<a id="1baeda9b0fe1809780b3c7d99ebaa677"></a>

```sql
--숫자 형변환
cast(값 as decimal) 

--문자 형변환
cast(값 as char))
```

<details>
<summary>ex) 형변환( <code>cast()</code> )</summary>

- rating&#58; 문자 타입  → <code>ABC</code>
    ![](3d59510f8728f1d8.webp)

<a id="1baeda9b0fe1803393d8f089c2096ab6"></a>

```sql
--숫자로 변경
cast(if(rating='Not given', '1', rating) as decimal) 

--문자로 변경
concat(restaurant_name, '-', cast(order_id as char))
```

</details>

</details>
