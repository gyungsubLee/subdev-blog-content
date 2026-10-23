---
order: 34
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81b2-a7cb-dfddd1327578
title: Querydsl 지원 클래스 직접 만들기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-81b2-a7cb-dfddd1327578
    title: Querydsl 지원 클래스 직접 만들기
excerpt: Querydsl 지원 클래스 직접 만들기 --- 📖 스프링 데이터가 제공하는 QuerydslRepositorySupport 가 지닌 한계를 극복하기 위해 직접 Querydsl 지원 클 래스를 생성하여 사용할 수 있다. 장점 - 스프링 데이터가 제공하는 페이징을 편리하게 변환 - 페이징과 카운트 쿼리 분리 가능 - 스프링
cover: null
icon: null
notionProperties:
  Point: "Querydsl 4.x 버전에 맞춘 Querydsl 지원 라이브러리 만들기 "
  중요도: Yes
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.116Z
updated: 2025-03-27T07:53:11.116Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/Querydsl 지원 클래스 직접 만들기-dfddd1327578/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181b2a7cbdfddd1327578
---
<a id="1c3eda9b0fe181ff9e9efe40cb3f34bd"></a>

## Querydsl <strong>지원 클래스 직접 만들기</strong>

---

> 📖 
> 
> <a id="1c3eda9b0fe181f8abf3ca568a47a405"></a>
> 
> 스프링 데이터가 제공하는 <code>QuerydslRepositorySupport</code> 가 지닌 한계를 극복하기 위해 직접 Querydsl 지원 클<br>래스를 생성하여 사용할 수 있다&#46;

<details>
<summary><strong>장점</strong></summary>

- 스프링 데이터가 제공하는 페이징을 편리하게 변환

- 페이징과 카운트 쿼리 분리 가능

- 스프링 데이터 Sort 지원

- <code>select()</code> , <code>selectFrom()</code> 으로 시작 가능

- <code>EntityManager</code> , <code>QueryFactory</code> 제공

</details>

<details>
<summary><strong>Querydsl4RepositorySupport</strong></summary>



</details>
