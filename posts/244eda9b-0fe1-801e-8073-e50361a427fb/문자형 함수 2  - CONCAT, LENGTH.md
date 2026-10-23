---
order: 10
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 244eda9b-0fe1-801e-8073-e50361a427fb
title: 문자형 함수 2  - CONCAT, LENGTH
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 244eda9b-0fe1-801e-8073-e50361a427fb
    title: 문자형 함수 2  - CONCAT, LENGTH
excerpt: "목차 - 문자 합성: concat() - 길이 계산: length() , len() 문자 합성: concat() sql SELECT Oracle concat('SQL', 'Expert') 2개 인자 제한 SQL Server concat('SQL', 'Expert', 'sefaef', 'feag' ...) 인자 3개 이상 "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-03T06:07:40.581Z
updated: 2025-08-03T07:12:01.390Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/문자형 함수 2  - CONCAT, LENGTH-e50361a427fb/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/244eda9b0fe1801e8073e50361a427fb
---
> 
> 
> <a id="244eda9b0fe180aaa4ebf9f4bcf4fffe"></a>
> 
> <strong>목차</strong>
> 
> - [문자 합성: concat()](#244eda9b0fe1806d9c38cfee9b7fe4dc)
> - [길이 계산:  length() , len()](#244eda9b0fe180dbadbfe2c8e82448fa)

<a id="244eda9b0fe1806d9c38cfee9b7fe4dc"></a>

### 문자 합성&#58; <code>concat()</code>

<a id="244eda9b0fe1807c9373ee9fbdf86e7d"></a>

```sql
SELECT
	# Oracle
	concat('SQL', 'Expert')  # 2개 인자 제한
	
	# SQL Server
	concat('SQL', 'Expert', 'sefaef', 'feag' ...) # 인자 3개 이상 가능
	
FROM 
# 출력: SQL Expert
# 출력2: SQL Expert sefaeffeag ...
```

<a id="244eda9b0fe180dbadbfe2c8e82448fa"></a>

### 길이 계산&#58;  <code>length()</code> , <code>len()</code>

<a id="244eda9b0fe18005bf2feb0b90befd45"></a>

```sql
SELECT
	length('SQL Expert')     # Oracle
	len('SQL Expert')        # SQL Server
FROM

# 출력: 10
```
