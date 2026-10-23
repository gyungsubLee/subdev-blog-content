---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 249eda9b-0fe1-80d2-9774-cb60cf663503
title: 변환형 함수 2 ( SQL Server ) - CAST, CONVERT
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 249eda9b-0fe1-80d2-9774-cb60cf663503
    title: 변환형 함수 2 ( SQL Server ) - CAST, CONVERT
excerpt: 목차 - 변환형 함수 ( SQL Server ) - 1. CAST() - 2. CONVERT(Type, Target) - 3. 합성 변환형 함수 ( SQL Server ) ✏️ 1. CAST ( expression AS data_type [ ( length ) ] 1. CONVERT ( data_type [ ( lengt
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-08T11:55:25.419Z
updated: 2025-08-08T12:27:18.995Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/변환형 함수 2 ( SQL Server ) - CAST, CONVERT-cb60cf663503/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/249eda9b0fe180d29774cb60cf663503
---
> 
> 
> <a id="249eda9b0fe1815d999ffbb3bc41b021"></a>
> 
> <strong>목차</strong>
> 
> - [ 변환형 함수 ( SQL Server )](#249eda9b0fe181e198cad9a964a95954)
> - [1.  CAST()](#249eda9b0fe18025823ef3ba26c62264)
> - [2.  CONVERT(Type, Target)](#249eda9b0fe1809caebfe786728ddb64)
> - [3.  합성](#249eda9b0fe180e69d44c82442685ff3)

<a id="249eda9b0fe181e198cad9a964a95954"></a>

##  변환형 함수 ( SQL Server )

> ✏️ 
> 
> 1. <code>CAST ( expression AS data&#95;type &#91; ( length ) &#93;</code>
> 
> 1. <code>CONVERT ( data&#95;type &#91; ( length ) &#93;, expression &#91; , style &#93; )</code>

<a id="249eda9b0fe18025823ef3ba26c62264"></a>

### 1&#46;  <code>CAST()</code>

<a id="249eda9b0fe1817786cae30edac61e60"></a>

```sql
# SQL Server
SELECT
	CAST('20.99' as float),       # 결과: 20.99 
	CAST(20 as vachar(2)),        # 결과: '20'
	CAST(getdate() AS char),      # 결과: 'Agu 8 2025 21:09PM'
FROM dual
```

<a id="249eda9b0fe1809caebfe786728ddb64"></a>

### 2&#46;  <code>CONVERT(Type, Target)</code>

<a id="249eda9b0fe180428e4ee069e238e445"></a>

```sql
# SQL Server
SELECT
	CONVERT(varchar, getdate(), 14)                  # 결과: '21:08:25' ( 시간만 표시 )
	CONVERT(varchar, getdate(), 1)                   # 결과: '2025-08-08' ( 날짜만 표시 )
	CONVERT(varchar, getdate(), 120)                 # 결과: '2025-08-08 21:08:25' ( ODBC 표준 )
	CONVERT(int, '20')                    # 결과:  20
	CONVERT(float, '20.99')               # 결과:  20.99
	CONVERT(varchar, 20)       # 결과: '20'
FROM dual
```

<a id="249eda9b0fe180e69d44c82442685ff3"></a>

### 3&#46;  합성

<a id="249eda9b0fe180dd89ece4f2e9263faf"></a>

```sql
# SQL Server
SELECT
	CONVERT(datetime, CAST(getdate() AS char)),      # 결과: '2025-08-08 21:08:25'
	CAST( CAST(getdate() AS char) as datetime)       # 결과: '2025-08-08 21:08:25'
FROM dual
```
