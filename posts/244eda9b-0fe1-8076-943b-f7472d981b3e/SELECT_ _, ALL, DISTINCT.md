---
order: 17
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 244eda9b-0fe1-8076-943b-f7472d981b3e
title: "SELECT: *, ALL, DISTINCT"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 244eda9b-0fe1-8076-943b-f7472d981b3e
    title: "SELECT: *, ALL, DISTINCT"
excerpt: "* sql SELECT FROM emp; - * : 애스터리스크, 모든 열을 선택하는 키워드이다. ALL sql SELECT empno, ename, job, sal FROM emp; SELECT ALL empno, ename, job, sal FROM emp; - ALL은 default 값으로 모든 열을 가져온다는 의미"
cover: 6c32cc3a416f135a.jpg
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-03T02:32:27.339Z
updated: 2025-08-03T05:56:15.940Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/SELECT- -, ALL, DISTINCT-f7472d981b3e/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/244eda9b0fe18076943bf7472d981b3e
---
<details>
<summary><code>&#42;</code> </summary>

<a id="244eda9b0fe1804daa25d758c49ba85d"></a>

```sql
SELECT * FROM emp;
```

- <code>&#42;</code> &#58; 애스터리스크, 모든 열을 선택하는 키워드이다&#46;

</details>

<details>
<summary><code>ALL</code></summary>

<a id="244eda9b0fe18047b0a0c3b4184839db"></a>

```sql
SELECT empno, ename, job, sal 
FROM emp;

SELECT ALL
	empno, ename, job, sal 
FROM emp;
```

- <code>ALL</code>은 default 값으로 모든 열을 가져온다는 의미 인다&#46; 

- <code>DISTINCT</code> 와 대비되는 의미를 가진다&#46;

</details>

<details>
<summary><code>DISTINCT</code></summary>

<a id="244eda9b0fe1802e9dd8db0aabcb920c"></a>

```sql
SELECT DISTINCT empno, job 
FROM emp 
ORDER BY 1, 2;
```

- <code>DISTINCT</code>는 중복된 값을 제거하여 조회한다&#46;

</details>
