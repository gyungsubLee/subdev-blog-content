---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 246eda9b-0fe1-80f2-a905-e36795a2ffee
title: 날짜형 함수 - SYADATE, EXTRACT, TO_NUMBER(TO_CHAR(date_expr)), 날짜 연산
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 246eda9b-0fe1-80f2-a905-e36795a2ffee
    title: 날짜형 함수 - SYADATE, EXTRACT, TO_NUMBER(TO_CHAR(date_expr)), 날짜 연산
excerpt: "목차 - 현재 날짜: SYSDATE, GETDATE() - 현재 날짜 필터링 1: extract('포맷' FROM SYSDATE), DATEPART(포맷, GETDATE()), 포맷(GETDATE()) - 현재 날짜 필터링 2: extract('포맷' FROM SYSDATE), DATEPART(포맷, GETDATE()),"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-05T11:14:21.783Z
updated: 2025-08-05T12:07:27.486Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/날짜형 함수 - SYADATE, EXTRACT, TO_NUMBER(TO_CHAR(-e36795a2ffee/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/246eda9b0fe180f2a905e36795a2ffee
---
> 
> 
> <a id="246eda9b0fe1803aab4af1ec7dfdcdd9"></a>
> 
> <strong>목차</strong>
> 
> - [현재 날짜: SYSDATE, GETDATE()](#246eda9b0fe1806495a7c128590747c0)
> - [현재 날짜 필터링 1: extract('포맷' FROM SYSDATE), DATEPART(포맷, GETDATE()), 포맷(GETDATE())](#246eda9b0fe18096a8aecc15d8bfd3c2)
> - [현재 날짜 필터링 2: extract('포맷' FROM SYSDATE), DATEPART(포맷, GETDATE()), 포맷(GETDATE())](#246eda9b0fe180e88e72e7f9c1d82e00)
> - [날짜 연산: TO_DATE(), convert(), dateadd()](#246eda9b0fe180dab7deef1fad82bcf5)

<a id="246eda9b0fe1806495a7c128590747c0"></a>

### 현재 날짜&#58; <code>SYSDATE</code>, <code>GETDATE()</code>

<a id="246eda9b0fe18065a16af31fedbbb583"></a>

```sql
# Oracle
SELECT
	SYSDATE  # 결과: 2025-08-05 11:16:58.000 ( 현재 시간 )
FROM dual
```

![](ba954e2459dbaed7.webp)

<a id="246eda9b0fe180a19697cf2f780a93e9"></a>

```sql
# SQL Server
SELECT
	GETDATE()  # 결과: 현재 시간
```

<a id="246eda9b0fe18096a8aecc15d8bfd3c2"></a>

### 현재 날짜 필터링 1&#58; <code>extract(&#39;포맷&#39; FROM SYSDATE)</code>, <code>DATEPART(포맷, GETDATE())</code>, <code>포맷(GETDATE())</code>

<a id="246eda9b0fe180b68401d84b78d8ad6e"></a>

```sql
# Oracle
SELECT
	SYSDATE,
	extract(DAY FROM SYSDATE),
	extract(MONTH FROM SYSDATE),
	extract(YEAR FROM SYSDATE)
FROM dual
```

![](a34700eae72526a3.webp)

<a id="246eda9b0fe180f88ccfd05da6c8373c"></a>

```sql
# SQL Server
SELECT
	# DATEPART(포맷, GETDATE())
	DATEPART(DAY, GETDATE()),
	DATEPART(MONTH, GETDATE()),
	DATEPART(YEAR, GETDATE()),
	
	# 포맷(GETDATE())
	DAY(GETDATE()),
	MONTH(GETDATE()),
	YEAR(GETDATE()),
	GETDATE()
```

![](b100b7530885b033.webp)

<a id="246eda9b0fe180e88e72e7f9c1d82e00"></a>

### 현재 날짜 필터링 2&#58; <code>extract(&#39;포맷&#39; FROM SYSDATE)</code>, <code>DATEPART(포맷, GETDATE())</code>, <code>포맷(GETDATE())</code>

<a id="246eda9b0fe1800792eec6ace53cad26"></a>

```sql
SELECT
	TO_CHAR(SYSDATE, 'YYYY-MM-DD'),
	TO_CHAR(SYSDATE, 'YYYY-MM'),
	TO_CHAR(SYSDATE, 'YYYY'),
	TO_NUMBER(TO_CHAR(SYSDATE, 'YYYY'))
FROM dual
```

![](4197893bcd89374c.webp)

<a id="246eda9b0fe180f4ba75f088cd3daa82"></a>

```sql
# SQL Server
SELECT
	# DATEPART(포맷, GETDATE())
	DATEPART(DAY, GETDATE()),
	DATEPART(MONTH, GETDATE()),
	DATEPART(YEAR, GETDATE()),
	
	# 포맷(GETDATE())
	DAY(GETDATE()),
	MONTH(GETDATE()),
	YEAR(GETDATE()),
	GETDATE()
```

![](b100b7530885b033.webp)

<a id="246eda9b0fe180dab7deef1fad82bcf5"></a>

### 날짜 연산&#58; <code>TO&#95;DATE()</code>, <code>convert()</code>, <code>dateadd()</code>

<a id="246eda9b0fe180898e49d262d4fe375c"></a>

```sql
SELECT
	TO_DATE('2025-08-05', 'YYYY-MM-DD'),
	TO_DATE('2025-08-05', 'YYYY-MM-DD')+1,        # + 날짜
	TO_DATE('2025-08-05', 'YYYY-MM-DD')+1/24,     # + 시간
	TO_DATE('2025-08-05', 'YYYY-MM-DD')+1/24/60   # + 분
FROM dual
```

![](4197893bcd89374c.webp)

<a id="246eda9b0fe18034b9d8e290b55ff5a7"></a>

```sql
# SQL Server
SELECT
	# convert(DATETIME, 날짜)
	convert(DATETIME, '2025-08-05'),
	convert(DATETIME, '2025-08-05')+1,        # + 날짜
	convert(DATETIME, '2025-08-05')+1/24,     # + 시간
	convert(DATETIME, '2025-08-05')+1/24/60,   # + 분
	
	# dateadd()
	dateadd(hour, 3, convert(DATETIME, '2025-08-05'))
```

![+ 1시간: 1/24](8ef2e61217c70f7a.webp)

![+ 1분: 1/24/60](66cd932cb8b728a2.webp)

![+ 4분: 1/24/15](f1abbe2300ac1b36.webp)

![+ 1초: 1/24/60/60](9a5e985987c30e18.webp)
