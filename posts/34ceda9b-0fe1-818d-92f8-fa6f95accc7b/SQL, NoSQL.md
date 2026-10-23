---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 34ceda9b-0fe1-818d-92f8-fa6f95accc7b
title: SQL, NoSQL
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 328eda9b-0fe1-8016-bbca-ca913bc597bc
    title: 데이터 분석
  - id: 34ceda9b-0fe1-8078-af62-d55dce35db3b
    title: "[패스트캠퍼스] 2025 데이터분석 Master Class"
  - id: 34ceda9b-0fe1-808e-814d-f5cdd85c7f3b
    title: CH2. SQL
  - id: 34ceda9b-0fe1-818d-92f8-fa6f95accc7b
    title: SQL, NoSQL
excerpt: "[DB-Engines Ranking]() RDBMS (Relational Database Management System) --- ✏️ 관계형 데이터 모델 RDBMS 종류 오라클 MySQL SQL Server PostgreSQL MariaDB IBM DB2 NoSQL --- ✏️ 비 관계형 데이터 모델 NoSQL 같은 경"
cover: null
icon: null
notionProperties:
  AE<<: 🧐 질문,복습
  상태: 완료
schema_version: 1
parent_id: 34ceda9b-0fe1-808e-814d-f5cdd85c7f3b
created: 2026-04-24T00:37:52.652Z
updated: 2026-04-24T01:05:55.044Z
legacy_path: Main/데이터 분석-ca913bc597bc/[패스트캠퍼스] 2025 데이터분석 Master Class-d55dce35db3b/CH2. SQL-f5cdd85c7f3b/SQL, NoSQL-fa6f95accc7b/index.md
legacy_category: 데이터 분석
source_url: https://beautiful-college-c84.notion.site/34ceda9b0fe1818d92f8fa6f95accc7b
---
[DB&#45;Engines Ranking]()

<a id="34ceda9b0fe180e881d1de8f859d4021"></a>

## RDBMS (Relational Database Management System)

---

![](4d4851b3d7147074.webp)

![](cdaf34d35f01f2ef.webp)

> ✏️ 
> 
> <a id="34ceda9b0fe180699e58e892a420782e"></a>
> 
> 관계형 데이터 모델

<a id="34ceda9b0fe1804cbc78e2b288eff364"></a>

RDBMS 종류

<details>
<summary>오라클</summary>

![](72ee79b64ec2dc76.webp)

</details>

<details>
<summary>MySQL</summary>

![](eb3f3562257a674d.webp)

</details>

<details>
<summary>SQL Server</summary>

![](9bc2cadef38a3026.webp)

</details>

<details>
<summary>PostgreSQL</summary>

![](1b3c446cbff963c8.webp)

</details>

<details>
<summary>MariaDB</summary>

![](2cf25b4ea33eaf44.webp)

</details>

<details>
<summary>IBM DB2</summary>

![](ac74b0d2e2ca9556.webp)

</details>

<a id="34ceda9b0fe1802c899cf7df24c5d83d"></a>

## NoSQL

---

> ✏️ 
> 
> <a id="34ceda9b0fe180619d49d0f43b2b8e68"></a>
> 
> 비 관계형 데이터 모델

<a id="34ceda9b0fe18097b50acd65c7d0329e"></a>

NoSQL 같은 경우 <strong><u>빠르게 변화에 대응</u></strong>해야 하는 프로그램이나 <strong><u>빅데이터를 다루는 서비스</u></strong>에 적합한 DBMS라 할 수 있다&#46; 

- 스키마 유연성
    - 컬럼 추가/삭제가 자유로움

    - 빠른 실험/변화에 대응함

- JOIN 제거
    - 한 번에 읽기 가능 (JOIN 없음)

    - 읽기 성능 매우 빠름

- 수평 확장(Scale&#45;out)
    - NoSQL은 처음부터 분산을 고려

    - 노드 추가 → 성능 증가

    - 빅데이터 처리에 적합

<a id="34ceda9b0fe180758766e637263f6b35"></a>

실제로 Netflix, Facebook, Google 과 같은 기업에서 NoSQL을 사용하고 있다&#46; 

<a id="34ceda9b0fe180dfb653d19d9a6978f6"></a>

NoSQL 종류

<details>
<summary>mongoDB</summary>

![](98b65b677805363f.webp)

</details>

<details>
<summary>MariaDB</summary>

![](b91a14a2e79f088b.webp)

</details>

<details>
<summary>amazon DynamoDB</summary>

![](c462c6d5b2981633.webp)

</details>

<details>
<summary>cassandra</summary>

![](d7c086a74a218ad9.webp)

</details>

<details>
<summary>apache HBASE</summary>

![](643904b61e7bb75f.webp)

</details>

| <strong>요구사항</strong> | <strong>RDB</strong> | <strong>NoSQL</strong> |
| --- | --- | --- |
| 트랜잭션 중요 (금융) | ✅ | ❌ |
| 스키마 자주 변경 | ❌ | ✅ |
| 대규모 트래픽 | ❌ | ✅ |
| 복잡한 관계 | ✅ | ❌ |
| 빠른 개발/실험 | ❌ | ✅ |
