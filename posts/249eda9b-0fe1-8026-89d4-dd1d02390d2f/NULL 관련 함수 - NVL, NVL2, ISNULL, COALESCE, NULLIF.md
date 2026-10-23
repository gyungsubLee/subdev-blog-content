---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 249eda9b-0fe1-8026-89d4-dd1d02390d2f
title: NULL 관련 함수 - NVL, NVL2, ISNULL, COALESCE, NULLIF
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 249eda9b-0fe1-8026-89d4-dd1d02390d2f
    title: NULL 관련 함수 - NVL, NVL2, ISNULL, COALESCE, NULLIF
excerpt: "목차 - 음수, 양수, 0 판단: SIGN() - 나머지 연산: mod(), % - 내림 함수: floor() 음수, 양수, 0 판단: SIGN() ✏️ sql Oracle, SQL Server SELECT SIGN(-15) 결과: -1 SIGN(0) 결과: 0 SIGN(51351) 결과: 1 FROM dual 나머지 연"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-08T12:37:20.048Z
updated: 2025-08-08T12:38:00.149Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/NULL 관련 함수 - NVL, NVL2, ISNULL, COALESCE, NUL-dd1d02390d2f/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/249eda9b0fe1802689d4dd1d02390d2f
---
> 
> 
> <a id="249eda9b0fe1814cb528e3e046fbcc53"></a>
> 
> <strong>목차</strong>
> 
> - [음수, 양수, 0 판단: SIGN()](#249eda9b0fe181079d60fea1182577fd)
> - [나머지 연산: mod(), %](#249eda9b0fe18146845adf1179c1f457)
> - [내림 함수: floor()](#249eda9b0fe181de911fe5a18f325ead)

<a id="249eda9b0fe181079d60fea1182577fd"></a>

### 음수, 양수, 0 판단&#58; <code>SIGN()</code>

> ✏️ 

<a id="249eda9b0fe181a69347c00d1e11c138"></a>

```sql
# Oracle, SQL Server
SELECT
	SIGN(-15)        # 결과: -1 
	SIGN(0)          # 결과: 0
	SIGN(51351)      # 결과: 1
FROM dual
```

<a id="249eda9b0fe18146845adf1179c1f457"></a>

### 나머지 연산&#58; <code>mod()</code>, <code>%</code>

<a id="249eda9b0fe1810ea267c196e3fac7eb"></a>

```sql
# Oracle
SELECT
	mod(7, 3)   # 결과: 1
FROM dual
```

<a id="249eda9b0fe18138b347e654251b0b85"></a>

```sql
# SQL Server
SELECT
	7%4    # 결과: 3
FROM dual
```

<a id="249eda9b0fe181de911fe5a18f325ead"></a>

### 내림 함수&#58; <code>floor()</code>

<a id="249eda9b0fe181569281c95228d0618e"></a>

```sql
# Oracle, SQL Server
SELECT
	floor(38.123),   # 결과: 38
FROM dual
```
