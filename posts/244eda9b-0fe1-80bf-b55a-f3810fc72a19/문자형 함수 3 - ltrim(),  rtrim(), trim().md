---
order: 8
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 244eda9b-0fe1-80bf-b55a-f3810fc72a19
title: 문자형 함수 3 - ltrim(),  rtrim(), trim()
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 244eda9b-0fe1-80bf-b55a-f3810fc72a19
    title: 문자형 함수 3 - ltrim(),  rtrim(), trim()
excerpt: "문자, 공백 제거 1. ltrim()( left trim, 왼쪽부터 검사 시작 ) Case 1 ) 단일 문자 제거 sql SELECT ltrim('xxxYYYZZxYZ', 'x') Oracle SQL Server FROM 출력: YYYZZYZ Case 2) 여러 문자들을 인자로 넘겨 제거할 수 있다. sql SELECT "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-03T07:11:42.145Z
updated: 2025-08-03T07:12:25.486Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/문자형 함수 3 - ltrim(),  rtrim(), trim()-f3810fc72a19/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/244eda9b0fe180bfb55af3810fc72a19
---
<a id="244eda9b0fe180e4a694e920185e5a49"></a>

## 문자, 공백 제거

<a id="244eda9b0fe1801fb760f95d5a486ac2"></a>

### 1&#46; <code>ltrim()</code>( left trim,  왼쪽부터 검사 시작 ) 

<details>
<summary>Case 1 ) 단일 문자 제거</summary>

<a id="244eda9b0fe180169dcef891d183cb2e"></a>

```sql
SELECT
	ltrim('xxxYYYZZxYZ', 'x')     # Oracle  # SQL Server
FROM

# 출력: YYYZZYZ
```

</details>

<details>
<summary>Case 2) 여러 문자들을 인자로 넘겨 제거할 수 있다&#46; </summary>

<a id="244eda9b0fe180488ac9c67e28052818"></a>

```sql
SELECT
	ltrim('xxxYYYZZxYZ', 'xYZ')     # Oracle
FROM

# 출력: NULL
```

</details>

<details>
<summary>Case 3 ) 인자가 없는 경우, 공백을 제거한다&#46;</summary>

<a id="244eda9b0fe18025872bd49f1a244690"></a>

```sql
SELECT
	ltrim('   xxxx')     # Oracle, SQL Server
FROM
# 출력: xxxxx
```

</details>

<a id="244eda9b0fe1802a8cb1cc769727821f"></a>

### 2&#46; <code>rtrim()</code> ( right trim, 오른쪽부터 검사 시작 )

<details>
<summary>Case 1) 여러 문자들을 인자로 넘겨 제거할 수 있다&#46; </summary>

<a id="244eda9b0fe180248ec2c522ab5fef4b"></a>

```sql
SELECT
	rtrim('xxxYYYZZxYZ', 'ZY')     # Oracle
FROM

# 출력: xxxx
```

</details>

<details>
<summary>Case 2 ) 인자가 없는 경우, 공백을 제거한다&#46;</summary>

<a id="244eda9b0fe18078a78ec244d4cf146f"></a>

```sql
SELECT
	rtrim('xxxx   ')     # Oracle, SQL Server
FROM
# 출력: xxxxx
```

</details>

<a id="244eda9b0fe1800c9e9ac29ea26abbf3"></a>

### 3&#46; <code>trim()</code> ( both, 양쪽에서 검사 시작 )

<details>
<summary>Case 1) 여러 문자들을 인자로 넘겨 제거할 수 있다&#46; </summary>

<a id="244eda9b0fe180e2a94adaf6bd6e8fcf"></a>

```sql
SELECT
	# Oracle, SQL Server
	trim((BOTH) 'x' FROM 'xxxYYYZZxYZxxx')   # 지정 문자 2개 이상 사용할 수 없다 
	trim(LEADING 'x' FROM 'xxxYYYZZxYZxxx')   # ltrim() 동일
	trim(TRAILING 'x' FROM 'xxxYYYZZxYZxxx')   # rtrim() 동일
FROM

# 출력: xxxx
```

</details>
