---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 23aeda9b-0fe1-800d-b284-d277ec4a8086
title: 데이터베이스 모델링 ( Database Modeling )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23aeda9b-0fe1-80e8-a9d6-eef83f4e0193
    title: 비전공자도 이해할 수 있는 DB 설계 입문/실전
  - id: 23aeda9b-0fe1-800d-b284-d277ec4a8086
    title: 데이터베이스 모델링 ( Database Modeling )
excerpt: 목차 - 데이터베이스 모델링 ( Database Modeling ) 데이터베이스 모델링 ( Database Modeling ) --- 📖 데이터 모델링은 영속성을 갖는 데이터에 대한 시스템 구조를 사람이 이해할 수 있도록 형상화하는 과정이다 - 데이터 모델은 현실 세계의 정보나 데이터를 시스템으로 구축하기 위해 추상화하
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 23aeda9b-0fe1-80e8-a9d6-eef83f4e0193
created: 2025-07-24T09:36:26.904Z
updated: 2025-07-24T10:14:00.024Z
legacy_path: Main/DBMS-e8c2debc9fa0/비전공자도 이해할 수 있는 DB 설계 입문-실전-eef83f4e0193/데이터베이스 모델링 ( Database Modeling )-d277ec4a8086/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/23aeda9b0fe1800db284d277ec4a8086
---
> 
> 
> <a id="23aeda9b0fe1810f99d0e719d4995a1d"></a>
> 
> <strong>목차</strong>
> 
> - [데이터베이스 모델링 ( Database Modeling )](#23aeda9b0fe181b1a7f4d8700a1a8ec8)

<a id="23aeda9b0fe181b1a7f4d8700a1a8ec8"></a>

## 데이터베이스 모델링 ( Database Modeling )

---

> 📖 
> 
> <a id="23aeda9b0fe18070935cdbb5be249dab"></a>
> 
> <code>데이터 모델링</code>은 <strong><u>영속성을 갖는 데이터에 대한 시스템 구조를 사람이 이해할 수 있도록 형상화하는 과정</u></strong>이다 
> 
> - <code>데이터 모델</code>은 <strong>현실 세계의 정보나 데이터를 시스템으로 구축하기 위해 </strong><strong><u>추상화하여 체계적으로 표현한 모형</u></strong>이다&#46; 
> 
> - 표준국어사전에서는 <code>모델</code>을 <strong><u>“작품을 만들기 전에 미리 만든 물건, 또 완성된 작품의 대표적인 보기”</u></strong>로 정의한다&#46; 
> 
> <a id="23aeda9b0fe18058be98d8de6a499647"></a>
> 
> 사람이 <strong><u>정보로서 의미있는 대상을 인지하고, 식별</u></strong>하는 과정(<code>개념적</code>)을 거쳐 <strong><u>식별한 것을 기호 등를 통해 추상화</u></strong>하여 표현(<code>논리적</code>)하고, 정보시스템에 데이터베이스로 구축하기 위해 <strong><u>추상화된 모델을 구체화된 형태로 변환</u></strong>한다&#46;(<code>물리적</code>)

<a id="23aeda9b0fe1804a9da3c2ef10a52a3c"></a>

<strong><u>데이터를 어떻게 분류해서 저장할 지를 설계하는 행위</u></strong>를 <code>데이터베이스 모델링(Database Modeling)</code> 이라고 표현한다&#46;  

- 데이터 모델링, 데이터베이스 설계(DB 설계) 라고도 부른다&#46; 

> 🧐 
> 
> <a id="23aeda9b0fe1800a9598ed87b0c6dfab"></a>
> 
> <strong>왜 </strong><strong><code>데이터 모델링</code></strong><strong>을 배워야 하는가?</strong>
> 
> <a id="23aeda9b0fe180f68a4bfed0d9cafe6b"></a>
> 
> 사람들마다 정리에 대한 기준이 다르다&#46; 
> 
> <a id="23aeda9b0fe1804cbd1fc23ee59a4b83"></a>
> 
> 옷을 예시로 들자면 누군가는 외출복과 일상복을 기준으로 옷을 구분해 분류하기도 하며, <br>누군가는 상의와 하의를 기준으로 구분하기도 하며, 또다른 누군가는 색깔을 기준으로 옷을 구분해 관리하기도 한다&#46; 
> 
> <a id="23aeda9b0fe1805eb956f5e06c5474e1"></a>
> 
> 만약 데이터들로 이렇게 개인의 기준에 따라 분류가 된다면 어떨까?
> 
> <a id="23aeda9b0fe180819705ca9f5a001c4c"></a>
> 
> 이렇게 아무런 규칙없이 개인의 기준대로 데이터를 저장하면, 필요한 데이터를 찾기 매우 어렵다&#46;  이러한 비효율을 해결하기 위해 ‘<strong><u>공통의 기준’을 정해 분류</u></strong>하는 방법이 데이터 모델링이다&#46; 
> 
> <a id="23aeda9b0fe180758fb1c3d9c055b101"></a>
> 
> 이를 통해 <strong><u>특정 규칙을 가지고 일관되게 데이터를 저장</u></strong>할 수 있다&#46; 이렇게 일관되게 데이터를 저장하다보니 <strong><u>데이터도 쉽게 찾을 수 있</u></strong>다&#46; 
> 
> <a id="23aeda9b0fe180808956f47058bbd316"></a>
> 
> 실제 운영 상황에서는 매우 많은 데이터들을 관리해야한다&#46; 이를 데이터 모델링을 통해 일관되게 관리하여 효율적으로 데이터들을 처리할 수 있다&#46;

---
