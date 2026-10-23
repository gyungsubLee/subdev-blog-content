---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 227eda9b-0fe1-801b-84fd-cdc3b483ac3e
title: 멀티 컬럼 인덱스 (Mulitple-Column Index)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 226eda9b-0fe1-80be-80bb-ca65a5c45f49
    title: 비전공자도 이해할 수 있는 MySQL 성능 최적화 입문/실전 (SQL 튜닝편)
  - id: 227eda9b-0fe1-801b-84fd-cdc3b483ac3e
    title: 멀티 컬럼 인덱스 (Mulitple-Column Index)
excerpt: 목차 - 멀티 컬럼 인덱스 (Mulitple-Column Index) - 예시를 통한 멀티 컬럼 인덱스 이해 멀티 컬럼 인덱스 (Mulitple-Column Index) --- 📖 멀티 컬럼 인덱스 (Mulitple-Column Index) --- - 2개 이상의 컬럼을 묶어서 설정하는 인덱스 - 데이터를 빨리 찾기 위
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 226eda9b-0fe1-80be-80bb-ca65a5c45f49
created: 2025-07-05T13:48:44.367Z
updated: 2025-08-21T04:52:21.317Z
legacy_path: Main/DBMS-e8c2debc9fa0/비전공자도 이해할 수 있는 MySQL 성능 최적화 입문-실전 (SQL 튜닝편)-ca65a5c45f49/멀티 컬럼 인덱스 (Mulitple-Column Index)-cdc3b483ac3e/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/227eda9b0fe1801b84fdcdc3b483ac3e
---
> 
> 
> <a id="227eda9b0fe18126b5a4f8bcd9a59869"></a>
> 
> <strong>목차</strong>
> 
> - [멀티 컬럼 인덱스 (Mulitple-Column Index)](#227eda9b0fe1817aa2c8fae450fe5b3a)
> - [ 예시를 통한 멀티 컬럼 인덱스 이해](#227eda9b0fe180d28b37ebd6425f69e6)

<a id="227eda9b0fe1817aa2c8fae450fe5b3a"></a>

## 멀티 컬럼 인덱스 (Mulitple&#45;Column Index)

---

> 📖 
> 
> <a id="227eda9b0fe1802b9a01eeaaf948cf96"></a>
> 
> <strong><code>멀티 컬럼 인덱스</code></strong><strong> (</strong><strong><code>Mulitple&#45;Column Index</code></strong><strong>)</strong>
> 
> ---
> 
> - <strong>2개 이상의 컬럼을 묶어서 설정하는 인덱스</strong>
> 
> - <em><strong>데이터를 빨리 찾</strong></em><em><strong>기</strong></em><strong> 위해 </strong><strong><u>2개 이상의 컬럼을 기준</u></strong><strong>으로 미리 </strong><strong><u>정렬해놓은 표</u></strong>이다

<a id="227eda9b0fe180d28b37ebd6425f69e6"></a>

###  예시를 통한 멀티 컬럼 인덱스 이해

![users 테이블](6e468688db4b2059.webp)

<a id="227eda9b0fe18015aceed9b8cae38753"></a>

위와 같이 <code>users</code> 테이블이 있다고 가정한다면

![](21ea9f5e22a7eb5d.webp)

<a id="227eda9b0fe180a297a1fe6745ce8110"></a>

이때, <code>부서</code>, <code>이름</code> 컬럼들을 활용해 멀티 컬럼 인덱스를 생성하면 위와 같은 표가 시스템 내부에 생성된다&#46; 

1. <code>부서</code>를 기준으로 먼저 오름차순 정렬

1. 같은 <code>부서</code>의 값을 가진 데이터들 사이에서 <code>이름</code>을 기준으로 오름차순 정렬

<a id="227eda9b0fe18020acc4f9865395c1de"></a>

  

> ✏️ 
> 
> <a id="227eda9b0fe180259e2ffe38036aceab"></a>
> 
> 위 예시는 2개의 컬럼을 가지고 인덱스를 생성했지만,
> 
> <a id="227eda9b0fe1806582dfcfb6077c17af"></a>
> 
> 2개 이상의 컬럼들을 가지고도 생성 가능하다&#46;
