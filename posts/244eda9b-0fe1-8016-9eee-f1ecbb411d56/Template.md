---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 244eda9b-0fe1-8016-9eee-f1ecbb411d56
title: Template
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 244eda9b-0fe1-8016-9eee-f1ecbb411d56
    title: Template
excerpt: "목차 - 음수, 양수, 0 판단: SIGN() - 나머지 연산: mod(), % - 내림 함수: floor() 음수, 양수, 0 판단: SIGN() ✏️ sql Oracle, SQL Server SELECT SIGN(-15) 결과: -1 SIGN(0) 결과: 0 SIGN(51351) 결과: 1 FROM dual 나머지 연"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-03T07:51:54.540Z
updated: 2025-08-03T07:53:21.781Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/Template-f1ecbb411d56/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/244eda9b0fe180169eeef1ecbb411d56
---
> 
> 
> <a id="244eda9b0fe1808791b2ff74c5f101b2"></a>
> 
> <strong>목차</strong>
> 
> - [음수, 양수, 0 판단: SIGN()](#244eda9b0fe180399f45d2c8277dbe3c)
> - [나머지 연산: mod(), %](#244eda9b0fe180ad9939cd2446ae70b5)
> - [내림 함수: floor()](#244eda9b0fe180f982c9d0a523ce6d82)

<a id="244eda9b0fe180399f45d2c8277dbe3c"></a>

### 음수, 양수, 0 판단&#58; <code>SIGN()</code>

> ✏️ 

<a id="244eda9b0fe180418f54e9596de0f2d7"></a>

```sql
# Oracle, SQL Server
SELECT
	SIGN(-15)        # 결과: -1 
	SIGN(0)          # 결과: 0
	SIGN(51351)      # 결과: 1
FROM dual
```

<a id="244eda9b0fe180ad9939cd2446ae70b5"></a>

### 나머지 연산&#58; <code>mod()</code>, <code>%</code>

<a id="244eda9b0fe180979026f3ca5eb6b218"></a>

```sql
# Oracle
SELECT
	mod(7, 3)   # 결과: 1
FROM dual
```

<a id="244eda9b0fe180a9a1a8cf276c5d5af1"></a>

```sql
# SQL Server
SELECT
	7%4    # 결과: 3
FROM dual
```

<a id="244eda9b0fe180f982c9d0a523ce6d82"></a>

### 내림 함수&#58; <code>floor()</code>

<a id="244eda9b0fe180cf9228c6da9bdec2ad"></a>

```sql
# Oracle, SQL Server
SELECT
	floor(38.123),   # 결과: 38
FROM dual
```
