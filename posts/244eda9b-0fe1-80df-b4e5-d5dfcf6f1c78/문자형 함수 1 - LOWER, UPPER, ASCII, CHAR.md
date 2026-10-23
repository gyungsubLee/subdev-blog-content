---
order: 9
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 244eda9b-0fe1-80df-b4e5-d5dfcf6f1c78
title: 문자형 함수 1 - LOWER, UPPER, ASCII, CHAR
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 244eda9b-0fe1-80df-b4e5-d5dfcf6f1c78
    title: 문자형 함수 1 - LOWER, UPPER, ASCII, CHAR
excerpt: "소문자, 대분자 변환 --- 소문자 변환: lower() sql SELECT lower('SQL Expert') Oracle, SQL Server FROM 출력: sql expert 대문자 변환: upper() sql SELECT upper('SQL Expert') Oracle, SQL Server FROM 출력: SQL"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-03T05:56:53.562Z
updated: 2025-08-03T07:12:06.804Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/문자형 함수 1 - LOWER, UPPER, ASCII, CHAR-d5dfcf6f1c78/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/244eda9b0fe180dfb4e5d5dfcf6f1c78
---
<a id="244eda9b0fe1803a9b27ee334955bef8"></a>

## 소문자, 대분자 변환

---

<a id="244eda9b0fe1809ba5b2de6a4ee94d2a"></a>

### 소문자 변환&#58; <code>lower()</code>

<a id="244eda9b0fe1802e89a6d274b2d5335f"></a>

```sql
SELECT
	lower('SQL Expert')     # Oracle, SQL Server
FROM
# 출력: sql expert
```

<a id="244eda9b0fe1803eb40ee7ec12fbbb5d"></a>

### 대문자 변환&#58; <code>upper()</code> 

<a id="244eda9b0fe18093a995cca4df6c52ee"></a>

```sql
SELECT
	upper('SQL Expert')     # Oracle, SQL Server
FROM

# 출력: SQL EXPERT
```

<a id="244eda9b0fe180948c07e21c6eba8849"></a>

## ASCII 

---

[ASCII]()

<a id="244eda9b0fe180608dace2f36affc6ef"></a>

### 문자열 → ASCII &#58; <code>ascii()</code>

<a id="244eda9b0fe1805cba43da0cc2778692"></a>

```sql
SELECT
	ascii('A')        # Oracle, SQL Server
	ascii('Aasfafea') # 첫번쨰 글자만 인식
FROM

# 출력: 65
```

<a id="244eda9b0fe18017bf0dfe6e42ba58d3"></a>

### ASCII → 문자열&#58; <code>chr()</code>, <code>char()</code>

<a id="244eda9b0fe18084ba85dfecd13a7dad"></a>

```sql
SELECT
	chr(65)    # Oracle
	char(65)   # SQL Server
FROM 

# 출력: A
```
