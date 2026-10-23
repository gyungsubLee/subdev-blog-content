---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 246eda9b-0fe1-80e5-95cf-fc179155eef4
title: 변환형 함수 1 ( Oracle )  - TO_CHAR, TO_NUMBER, TO_DATE
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 246eda9b-0fe1-80e5-95cf-fc179155eef4
    title: 변환형 함수 1 ( Oracle )  - TO_CHAR, TO_NUMBER, TO_DATE
excerpt: "목차 - 문자 변환: TOCHAR() - 숫자 변환: TONUMBER() - 숫자 변환: TODATE() 문자 변환: TO_CHAR() sql Oracle TOCHAR(numericexpr | date [, format]) SELECT tochar(10), 결과: '10' tochar(sysdate, 'YYYY-MM-DD"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-05T12:07:20.786Z
updated: 2025-08-08T12:27:14.521Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/변환형 함수 1 ( Oracle )  - TO_CHAR, TO_NUMBER, TO-fc179155eef4/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/246eda9b0fe180e595cffc179155eef4
---
> 
> 
> <a id="246eda9b0fe1815db0c8d7c4094ae16d"></a>
> 
> <strong>목차</strong>
> 
> - [문자 변환: TO_CHAR()](#246eda9b0fe18163b3b8c90fa5aa04a1)
> - [숫자 변환: TO_NUMBER()](#249eda9b0fe180eb89eef7dd800aac7b)
> - [숫자 변환: TO_DATE()](#249eda9b0fe1809b9d53f9db5d5caceb)

<a id="246eda9b0fe18163b3b8c90fa5aa04a1"></a>

### 문자 변환&#58; <code>TO&#95;CHAR()</code>

<a id="246eda9b0fe18129953ee8f4efbc611b"></a>

```sql
# Oracle
# TO_CHAR(numeric_expr | date [, format])
SELECT
	to_char(10),  # 결과: '10'
	to_char(sysdate, 'YYYY-MM-DD'),  # 결과: '2025-08-08'
	to_char(sysdate, 'YYYY/MM/DD'),  # 결과: '2025/08/08'
	to_char(sysdate, 'YYYY'),  # 결과: '2025'
	to_char(sysdate, 'MM'),  # 결과: '08'
	to_char(sysdate, 'DD'),  # 결과: '08'
FROM dual;
```

<a id="249eda9b0fe180eb89eef7dd800aac7b"></a>

### 숫자 변환&#58; <code>TO&#95;NUMBER()</code>

<a id="249eda9b0fe180b29182d12c2e56b9f1"></a>

```sql
# Oracle
# TO_NUMBER(char_expr)
SELECT
	to_number('11')  # 결과: 11
FROM dual;
```

<a id="249eda9b0fe1809b9d53f9db5d5caceb"></a>

### 숫자 변환&#58; <code>TO&#95;DATE()</code>

<a id="249eda9b0fe180c7b40df0adba130224"></a>

```sql
# Oracle
# TO_DATE(char_expr [, format])
SELECT
	to_date('2025.08.08', 'YYYY.MM.DD')  # 결과: 2025-08-08 00:00:00.000
FROM dual;
```

![](046aca63a0f6540c.webp)
