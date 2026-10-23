---
order: 18
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 244eda9b-0fe1-8019-a8b9-ea6ffb494c1e
title: ALIAS
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
    title: 8시간 완성 SQLD ( 2 과목 )
  - id: 244eda9b-0fe1-8019-a8b9-ea6ffb494c1e
    title: ALIAS
excerpt: "AS 키워드 sql SELECT empno AS 사원번호, ename AS 이름, deptno AS 부서번호, job AS 직책 FROM emp; AS 키워드 생략 가능 sql SELECT empno 사원번호, ename 이름, deptno 부서번호, job 직책 FROM emp; 문법 ✏️ 불가능 - 앞에 숫자 ❌ - "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 23eeda9b-0fe1-8059-b8a9-ca53c645ad77
created: 2025-08-03T02:39:23.384Z
updated: 2025-08-03T05:56:15.940Z
legacy_path: Main/DBMS-e8c2debc9fa0/8시간 완성 SQLD ( 2 과목 )-ca53c645ad77/ALIAS-ea6ffb494c1e/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/244eda9b0fe18019a8b9ea6ffb494c1e
---
<details>
<summary><code>AS</code>  키워드</summary>

<a id="244eda9b0fe180ed8eddf661d345f684"></a>

```sql
SELECT 
		empno AS 사원번호, 
		ename AS 이름, 
		deptno AS 부서번호, 
		job AS 직책 
FROM emp;
```

</details>

<details>
<summary><code>AS</code>  키워드 <strong><u>생략 가능</u></strong></summary>

<a id="244eda9b0fe18010a714c80a123d862b"></a>

```sql
SELECT 
		empno 사원번호, 
		ename 이름, 
		deptno 부서번호, 
		job 직책 
FROM emp;
```

</details>

<a id="244eda9b0fe180baa501f8c9cd8b9175"></a>

### 문법

> ✏️ 
> 
> <details>
> <summary>불가능</summary>
> 
> - <strong>앞에 숫자 ❌</strong>
>     - ex)  <code>empno AS </code><u><code>0</code></u><code>사원번호</code>
> 
> - <strong>중간 특수문자 ❌</strong>
>     - ex)  <code>empno AS 사원</code><u><code>&#45;</code></u><code>번호</code>
> 
> - <strong>중간 띄어쓰기 ❌</strong>
>     - ex)  <code>empno AS 사원 번호</code>
> 
> </details>
> 
> <details>
> <summary>가능</summary>
> 
> - <strong>가능한 특수문자</strong>&#58; <code>&#95;</code>, <code>&#36;</code>, <code>&#35;</code> 
>     - ex)  <code>empno AS 사원&#95;&#36;&#35;번호</code>
> 
> - <strong>큰따옴표</strong>(<code>””</code>)<strong>&#58;</strong>
>     - 큰따옴표를 통해 문자열로 사용 시, 모든 내용 표기 가능하다&#46;  <br>( 문자열로 인식함)
> 
>     - ex) <code>empno AS &#34;0사원 &#45;%번호&#34;</code>
> 
> </details>

<details>
<summary>큰 따옴표(<code>””</code>)</summary>

> ✏️ 
> 
> <a id="244eda9b0fe1809eacc6f51289ad0538"></a>
> 
> 큰따옴표를 사용 시, 모든 내용 표기 가능하다&#46;  ( 문자열로 인식)

<a id="244eda9b0fe1802c9ec1e732555a1bd8"></a>

```sql
SELECT 
		empno AS "사원 번호", 
		ename AS "123이름", 
		deptno AS "부서-번호", 
		job AS 직책 
FROM emp;
```

</details>

<details>
<summary>대소문자 구분 ❌</summary>

<a id="244eda9b0fe1808db299d1ba961113c0"></a>

```sql
SELECT 
		empno AS "사원 번호", 
		ename AS "123이름", 
		deptno AS "부서-번호", 
		job AS Job 
FROM emp;
```

- <code>Job</code> → <code>JOB</code> 으로 표기됨

- 따라서 대소문자 구분 필요 시, <code>“Job”</code>  큰따옴표를 통해 문자열로 표기해야 한다&#46;

</details>
