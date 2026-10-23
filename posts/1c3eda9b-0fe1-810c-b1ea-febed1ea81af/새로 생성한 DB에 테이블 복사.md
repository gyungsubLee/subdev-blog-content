---
order: 12
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-810c-b1ea-febed1ea81af
title: 새로 생성한 DB에 테이블 복사
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
    title: MySQL
  - id: 1c3eda9b-0fe1-810c-b1ea-febed1ea81af
    title: 새로 생성한 DB에 테이블 복사
excerpt: ✏️ 다른 DB에 테이블 스키마 및 데이터 복제 방법 정리 1. 복제할 DB 생성 sql CREATE DATABASE newdbname; 2. 테이블 복사 ( 데이터까지 복사한다. ) sql RENAME TABLE olddbname.table1 TO newdbname.table1; 3. 기존 DB 삭제 ( 선택 ) sql
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
created: 2025-03-27T07:47:52.775Z
updated: 2025-03-27T07:47:52.775Z
legacy_path: Main/DBMS-e8c2debc9fa0/MySQL-cdc300921ef3/새로 생성한 DB에 테이블 복사-febed1ea81af/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1810cb1eafebed1ea81af
---
> ✏️ 
> 
> <a id="1c3eda9b0fe1816790ecea7d1ed7c17f"></a>
> 
> 다른 DB에 <strong><u>테이블 스키마 및 데이터 복제</u></strong> 방법 정리

<a id="1c3eda9b0fe181a48409f49fb835f1f5"></a>

1&#46; 복제할 DB 생성

<a id="1c3eda9b0fe181a29106e9143d1ccb92"></a>

```sql
CREATE DATABASE new_db_name;
```

<a id="1c3eda9b0fe181aaa4fff1764b3606e2"></a>

2&#46; 테이블 복사 ( 데이터까지 복사한다&#46; )

<a id="1c3eda9b0fe18156b096ddfff00ed030"></a>

```sql
RENAME TABLE old_db_name.table1 TO new_db_name.table1;
```

<a id="1c3eda9b0fe181968f98e4733d969191"></a>

3&#46; 기존 DB 삭제 ( 선택 )

<a id="1c3eda9b0fe181c3939edc13e95aec0a"></a>

```sql
DROP DATABASE old_db_name;
```
