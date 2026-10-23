---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 226eda9b-0fe1-80be-80bb-ca65a5c45f49
title: 비전공자도 이해할 수 있는 MySQL 성능 최적화 입문/실전 (SQL 튜닝편)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 226eda9b-0fe1-80be-80bb-ca65a5c45f49
    title: 비전공자도 이해할 수 있는 MySQL 성능 최적화 입문/실전 (SQL 튜닝편)
excerpt: "[인프런] 비전공자도 이해할 수 있는 MySQL 성능 최적화 입문/실전 (SQL 튜닝편) - 기간: 25.07.04(금) - 강의: ‣ - reference - 페이지 목차 - 1. 학습 전, 기본 환경 설정 및 개념 - 2. 인덱스(Index) 기본 개념 / 실전 활용법 - 3. 실행 계획(EXPLAIN)을 활용해 성능"
cover: d3a0ed6133df8341.webp
icon: a65c1d0f4b243670.webp
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
created: 2025-07-04T13:21:55.780Z
updated: 2026-03-27T15:28:11.526Z
legacy_path: Main/DBMS-e8c2debc9fa0/비전공자도 이해할 수 있는 MySQL 성능 최적화 입문-실전 (SQL 튜닝편)-ca65a5c45f49/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/226eda9b0fe180be80bbca65a5c45f49
---
> 
> 
> <a id="226eda9b0fe181988bbdcdcde4cc05fa"></a>
> 
> &#91;인프런&#93; <strong>비전공자도 이해할 수 있는 MySQL 성능 최적화 입문/실전 (SQL 튜닝편)</strong>
> 
> - 기간&#58; 25&#46;07&#46;04(금) 
> 
> - 강의&#58; ‣
> 
> - reference
>     - <a href="https://beautiful-college-c84.notion.site/f21dbca617364a34ab05d26bfa4fe43a">페이지</a> 

> 
> 
> <a id="227eda9b0fe1809b9ab6d7fd3ef86d24"></a>
> 
> <strong>목차</strong>
> 
> - [1. 학습 전, 기본 환경 설정 및 개념](#226eda9b0fe181469d4dc35a4e313e45)
> - [2. 인덱스(Index) 기본 개념 / 실전 활용법](#226eda9b0fe18061aab7d764c468c3c0)
> - [3. 실행 계획(EXPLAIN)을 활용해 성능 저하 요인 찾기](#226eda9b0fe18054a0d0d051a71d3c06)
> - [4. SQL문 튜닝 연습](#226eda9b0fe1805c8accfc39cb2766ba)
> - [5. SQL문 튜닝 실전](#226eda9b0fe180ad9d08f87c974e3c80)

<details>
<summary>Template</summary>

> 

> ✏️ 

> 📖 

> 
> 
> <a id="227eda9b0fe1801991c2fa4d460afa70"></a>
> 
> <strong>목차</strong>
> 
> - [1. 학습 전, 기본 환경 설정 및 개념](#226eda9b0fe181469d4dc35a4e313e45)
> - [2. 인덱스(Index) 기본 개념 / 실전 활용법](#226eda9b0fe18061aab7d764c468c3c0)
> - [3. 실행 계획(EXPLAIN)을 활용해 성능 저하 요인 찾기](#226eda9b0fe18054a0d0d051a71d3c06)
> - [4. SQL문 튜닝 연습](#226eda9b0fe1805c8accfc39cb2766ba)
> - [5. SQL문 튜닝 실전](#226eda9b0fe180ad9d08f87c974e3c80)

> 
> 
> <a id="227eda9b0fe180989eabed3d8bffabbf"></a>
> 
> <strong>정리</strong>
> 
> - 

[제목 없음](#/post/226eda9b-0fe1-8102-82c5-f816ea0eb8ee)

[[ 실습 ]](#/post/226eda9b-0fe1-8144-b000-cd138461494b)

</details>

<a id="226eda9b0fe181469d4dc35a4e313e45"></a>

### 1&#46; 학습 전, 기본 환경 설정 및 개념

[기본 환경 설정](#/post/227eda9b-0fe1-8045-83c3-f4888f0eb1e6)

[신입 백엔드 면접에서 자주 물어보는 ‘DB 성능 최적화’ 경험](#/post/226eda9b-0fe1-8011-a5ed-c382a6e4bb5c)

[DB 성능 개선 시, ‘SQL 튜닝’을 가장 먼저 해야 하는 이유](#/post/226eda9b-0fe1-8023-a9b1-e0309b9acf58)

[성능 개선을 위한 MySQL 구조 파악 / SQL 튜닝의 핵심](#/post/226eda9b-0fe1-8050-8ead-d33b1b928d53)

<a id="226eda9b0fe18061aab7d764c468c3c0"></a>

### 2&#46; <strong>인덱스(Index) 기본 개념 / 실전 활용법</strong>

[인덱스(Index)란?](#/post/226eda9b-0fe1-80be-ab79-eae16c9a85fa)

[[ 실습 ] 인덱스 설정 및 성능 측정](#/post/226eda9b-0fe1-8012-9a6f-fd701d98b3d1)

[기본으로 설정되는 인덱스 - PK](#/post/227eda9b-0fe1-804d-b328-f97bdd3b8169)

[제약 조건 추가 시, 자동 생성되는 인덱스 - UNIQUE](#/post/227eda9b-0fe1-80d9-88b1-f107a01de58e)

[[ 실습 ] 많은 인덱스 생성 후, 성능 비교](#/post/227eda9b-0fe1-8023-9959-c943973240b3)

[멀티 컬럼 인덱스 (Mulitple-Column Index)](#/post/227eda9b-0fe1-801b-84fd-cdc3b483ac3e)

[[ 실습 ] 멀티 컬럼( 복합키 )  인덱스  설정 및 작동 방식 이해 ( 의문점 해결 필요 )](#/post/256eda9b-0fe1-8091-b06a-d5ee351ef917)

<a id="226eda9b0fe18054a0d0d051a71d3c06"></a>

### 3&#46; 실행 계획(EXPLAIN)을 활용해 성능 저하 요인 찾기

<a id="226eda9b0fe1805c8accfc39cb2766ba"></a>

### 4&#46; SQL문 튜닝 연습

<a id="226eda9b0fe180ad9d08f87c974e3c80"></a>

### 5&#46; SQL문 튜닝 실전
