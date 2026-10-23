---
order: 12
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 226eda9b-0fe1-8011-a5ed-c382a6e4bb5c
title: 신입 백엔드 면접에서 자주 물어보는 ‘DB 성능 최적화’ 경험
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 226eda9b-0fe1-80be-80bb-ca65a5c45f49
    title: 비전공자도 이해할 수 있는 MySQL 성능 최적화 입문/실전 (SQL 튜닝편)
  - id: 226eda9b-0fe1-8011-a5ed-c382a6e4bb5c
    title: 신입 백엔드 면접에서 자주 물어보는 ‘DB 성능 최적화’ 경험
excerpt: 목차 - 1. ‘DB 성능 최적화 경험’ - 2. DB 성능 개선은 DBA가 하는 일 아닌가요? 1. ‘DB 성능 최적화 경험’ --- 1. 동시 사용자 수의증가 1. 데이터 양의 증가 1. 비효율적인 SQL문 작성 MySQL과 같은 DB를 개인 프로젝트나 토이 프로젝트에서 사용하는 경우, DB 성능이 느려지는 경우는 거
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 226eda9b-0fe1-80be-80bb-ca65a5c45f49
created: 2025-07-04T13:33:20.654Z
updated: 2025-07-04T14:15:00.636Z
legacy_path: Main/DBMS-e8c2debc9fa0/비전공자도 이해할 수 있는 MySQL 성능 최적화 입문-실전 (SQL 튜닝편)-ca65a5c45f49/신입 백엔드 면접에서 자주 물어보는 ‘DB 성능 최적화’ 경험-c382a6e4bb5c/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/226eda9b0fe18011a5edc382a6e4bb5c
---
> 
> 
> <a id="226eda9b0fe181ba9906ced88cb2274d"></a>
> 
> <strong>목차</strong>
> 
> - [1. ‘DB 성능 최적화 경험’](#226eda9b0fe181128a95d81ef7fe76c0)
> - [2. DB 성능 개선은 DBA가 하는 일 아닌가요?](#226eda9b0fe180f688d5df12839a2e60)

<a id="226eda9b0fe181128a95d81ef7fe76c0"></a>

## 1&#46; ‘DB 성능 최적화 경험’

---

> 
> 
> 1. 동시 사용자 수의증가
> 
> 1. 데이터 양의 증가
> 
> 1. <strong>비효율적인 SQL문 작성</strong>

<a id="226eda9b0fe180518563ce79d68ed5dd"></a>

MySQL과 같은 DB를 개인 프로젝트나 토이 프로젝트에서 사용하는 경우, DB 성능이 느려지는 경우는 거의 없다&#46; 

<a id="226eda9b0fe180e5bbc8e911ecbaa884"></a>

그러나 실제 현업에서 DB를 사용하다보면 성능이 느려지는 경우를 한 번씩 만나게 되는데, 크게 위 3가지가 원인이다&#46;

<a id="226eda9b0fe180008924e49cff67141f"></a>

DB 성능이 떨어졌다면 서비스 이용 시 가정 먼저 체감할 수 있다&#46; 

- 실제 서비스를 사용하다보면 데이터 자체가 늦게 로딩되는 걸 확인할 수&#46; 있다&#46;

<a id="226eda9b0fe18072b50ed70ecfa58110"></a>

서비스를 사용하는 입장에서 조금만 답답하게 느껴지면 바로 이탈하게 되고, 사용자 이탈은 회사에 큰 손실로 이어진다&#46; 

<a id="226eda9b0fe180368abdd9fcb1fbe6d9"></a>

그러다보니 <u>기술 면접에서</u><strong><u> DB 성능 개선 시 필요한 기초 개념(인덱스, 실행 계획 등)과 성능 개선 경험</u></strong><u>을 자주 물어보는 추세</u>이다&#46; 

<a id="226eda9b0fe180f688d5df12839a2e60"></a>

## 2&#46; DB 성능 개선은 DBA가 하는 일 아닌가요?

---

> ✏️ 
> 
> <a id="226eda9b0fe180d0adc1dafe8082cae6"></a>
> 
> 최근 많은 IT 서비스 기업의 회사 트렌드를 보면, 백엔드 개발자는 DB를 설계하는 것부터 성능 개선 까지 기본소양으로 여겨지고 있다&#46; 
> 
> - 인덱스, 트랜잭션, SQL 튜닝, 실행계획, 레플리케이션, 샤딩 등
> 
> <a id="226eda9b0fe180a1ba99e16c73866435"></a>
> 
> 따라서 <strong><u>경쟁력 있는 개발자가 되려면 DB 성능 개선에 관련된 개념을 배우고, DB 성능 개선 경험을 쌓을 필요가 있다&#46;</u></strong>
> 
> - <del>시간이 가면 갈수록 수준이 올라간다&#46; 특히 지금은… 장난없다&#46;&#46;</del>

<a id="226eda9b0fe1807d8a6efdbc847b0ab7"></a>

DB 성능 개선은 회사에서 DBA(데이터베이스 관리자)가 맡아서 하는게 아닌가? 하는 의문점이 들 수도 있다&#46;  

- 실제 규모가 큰 경우, 그렇게 역할을 나눠 업무를 한다&#46; 

<a id="226eda9b0fe1804b9af2f3032363de5d"></a>

하지만 DBA 없는 소규모 회사나 아니면 DBA가 있더라도 백엔드 개발자가 DB 관련 업무를 안 하는 게 아니다&#46;

<a id="226eda9b0fe18064a7e3c441fb46040a"></a>

백엔드 개발자와 DBA가 같이 협업을 진행하는 경우도 있고, 기본적인 DB 성능 개선 작업은 백엔드 개발자가 직접하는 경우도 있다&#46;
