---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 249eda9b-0fe1-8019-9379-e51c2d4d9048
title: CASE 문
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 249eda9b-0fe1-8019-9379-e51c2d4d9048
    title: CASE 문
excerpt: "목차 - 1. CASE 문 - 2. Case 문 축약: DECODE() 1. CASE 문 sql Oracle, SQL Server SELECT loc, CASE WHEN loc='NEW YORK' THEN 'EAST' WHEN loc='CHICAGO' THEN 'CENTER' ELSE 'ETC' END AS area, 공"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-08T12:28:12.342Z
updated: 2025-08-08T12:36:00.016Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/CASE 문-e51c2d4d9048/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/249eda9b0fe180199379e51c2d4d9048
---
> 
> 
> <a id="249eda9b0fe181dfb0f5c8003a73f40d"></a>
> 
> <strong>목차</strong>
> 
> - [1. CASE 문 ](#249eda9b0fe181148b1ed18a36d1a5f0)
> - [2. Case 문 축약: DECODE() ](#249eda9b0fe1805c8f06d9c9617ef37e)

<a id="249eda9b0fe181148b1ed18a36d1a5f0"></a>

### 1&#46; CASE 문 

<a id="249eda9b0fe181cda0b5df77a237f93a"></a>

```sql
# Oracle, SQL Server
SELECT
	loc,
	CASE WHEN loc='NEW YORK' THEN 'EAST'
			 WHEN loc='CHICAGO' THEN 'CENTER'
			 ELSE 'ETC' END AS area,
			 
	# 공통된 변수 - 앞으로 추출하여 중복 제거 가능
 	CASE loc WHEN 'NEW YORK' THEN 'EAST'
			     WHEN'CHICAGO' THEN 'CENTER'
					 ELSE 'ETC' END AS area2,
FROM dual
```

![](042aaeb1ca8df14f.webp)

<a id="249eda9b0fe1805c8f06d9c9617ef37e"></a>

### 2&#46; Case 문 축약&#58; <code>DECODE()</code> 

<a id="249eda9b0fe180d4bac4e392177003ec"></a>

```sql
# Oracle
SELECT
	# DECODE(변수, CASE1=('NEW YORK', 'EAST'), CASE2=('CHICAGO', 'CENTER'), ELSE)
	DECODE(loc, 'NEW YORK', 'EAST', 'CHICAGO', 'CENTER', 'ETC')
FROM dual
```

![](99b02a589d6eef33.webp)
