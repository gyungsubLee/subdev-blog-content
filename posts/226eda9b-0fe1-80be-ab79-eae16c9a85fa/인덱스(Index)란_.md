---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 226eda9b-0fe1-80be-ab79-eae16c9a85fa
title: 인덱스(Index)란?
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 226eda9b-0fe1-80be-80bb-ca65a5c45f49
    title: 비전공자도 이해할 수 있는 MySQL 성능 최적화 입문/실전 (SQL 튜닝편)
  - id: 226eda9b-0fe1-80be-ab79-eae16c9a85fa
    title: 인덱스(Index)란?
excerpt: "목차 - 1. 인덱스(Index) - ex) 인덱스 이해 1. 인덱스(Index) --- 📖 인덱스(Index)는 DB 테이블에 대한 검색 성능 속도를 높여주는 자료 구조를 뜻한다. - B+ Tree구조를 가지며 트리의 높이만큼 즉, O(logn) 시간복잡도 만큼의 탐색 속도를 가진다 - ‣ ✏️ 인덱스(Index): "
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 226eda9b-0fe1-80be-80bb-ca65a5c45f49
created: 2025-07-04T15:34:01.780Z
updated: 2025-07-05T09:49:00.707Z
legacy_path: Main/DBMS-e8c2debc9fa0/비전공자도 이해할 수 있는 MySQL 성능 최적화 입문-실전 (SQL 튜닝편)-ca65a5c45f49/인덱스(Index)란--eae16c9a85fa/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/226eda9b0fe180beab79eae16c9a85fa
---
> 
> 
> <a id="226eda9b0fe1800e8ad0f4fbd326b76f"></a>
> 
> <strong>목차</strong>
> 
> - [1. 인덱스(Index)](#226eda9b0fe180ee9a3efe8b6e7b428a)
> - [ex) 인덱스 이해](#226eda9b0fe1805b8bd9e55a7f09e34e)

<a id="226eda9b0fe180ee9a3efe8b6e7b428a"></a>

## 1&#46; 인덱스(Index)

---

> 📖 
> 
> <a id="226eda9b0fe1805f82c7f74d0d5bf9d7"></a>
> 
> <code>인덱스(Index)</code>는 DB 테이블에 대한 <strong><u>검색 성능 속도를 높</u></strong>여주는 자료 구조를 뜻한다&#46; 
> 
> - <code>B&#43; Tree</code>구조를 가지며 트리의 높이만큼 즉, <code>O(logn)</code> 시간복잡도 만큼의 탐색 속도를 가진다
> 
> - ‣

> ✏️ 
> 
> <a id="226eda9b0fe180fe8ef3fb972436f022"></a>
> 
> <code>인덱스(Index)</code>&#58; <strong><u>데이터를 빨리 찾</u></strong><strong>기 위해 </strong><strong>특정 컬럼을 기준으로 미리 정렬해놓은 표</strong>

<a id="226eda9b0fe1805b8bd9e55a7f09e34e"></a>

### ex) 인덱스 이해

![• USER 테이블](2fe90db1a9c59a6a.webp)

<a id="226eda9b0fe180d3a330db44064cac8f"></a>

만약 USER 테이블 내부에 1만개의 데이터가 존재하고, 그중 23살인 사용자를 전부 직접 찾으려고 한다면? 

<a id="226eda9b0fe180d0b77bcc09c4f67423"></a>

나이에 대한 정렬을 하지 않았기 때문에 모든 행을 일일이 검사해 23살인 사용자를 탐색해야 한다&#46;

- 1만 개의 데이터를 일일이 다 확인해야 하므로 시간이 오래 걸릴 수 밖에 없다&#46; → <code>O(n)</code>의 시간 복잡도

![](a61274b8b0ca0da3.webp)

<a id="226eda9b0fe1805daacfed6eed618f12"></a>

하지만 왼쪽과 같이 나이 순으로 정렬된 표가 있다면 

<a id="227eda9b0fe18055990ed7c2cde489f2"></a>

아래와 같이 빠르게 탐색할 수 있다

![](4c05d46255200673.webp)

- 나이가 23살인 사용자를 뽑아내려면 위의 표에서 <strong><u>23살로 시작하는 지점</u></strong>과 <strong><u>24살로 시작되는 지점</u></strong>만 찾은 뒤 그 사이에 있는 모든 값을 가져오면 된다

- 모든 데이터를 일일이 다 확인할 필요가 없이 훨씬 더 빠르게 데이터 조회가 가능하다&#46;

> 
> 
> <a id="226eda9b0fe180a4b6a3dada60305373"></a>
> 
> 위의 예시에서 <strong><u>나이 순으로 정렬된 표</u></strong>가 <strong>인덱스</strong>이다&#46; 정확히 말하자면 <strong>나이 컬럼을 기준으로 인덱스를 생성한 것</strong>이다&#46; 
> 
> <a id="226eda9b0fe1809c9c91e5637a768b02"></a>
> 
> 이러한 특징 때문에 <strong><u>데이터를 찾는 속도를 빠르게 만들기 위해서 인덱스를 많이 활용</u></strong>한다&#46; 

- 참고로 실제 DB에서는 인덱스를 생성한다고 해서 정렬된 표를 직접 눈으로 확인할 수는 없다&#46; <br>시스템 내부적으로 생성될 뿐이다&#46;
