---
order: 33
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81f4-bfb3-fffdbbdcd64f
title: 리포지토리 지원 - QuerydslRepositorySupport
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-81f4-bfb3-fffdbbdcd64f
    title: 리포지토리 지원 - QuerydslRepositorySupport
excerpt: "QuerydslRepositorySupport --- 📖 이전 버전에서 사용한 방법으로 버전이 업데이트된 현재는 사용 ❌ 장점 - getQuerydsl().applyPagination() 스프링 데이터가 제공하는 페이징을 Querydsl로 편리하게 변환 가능 - 단, Sort는 오류 발생 - from()으로 시작 가능 "
cover: null
icon: null
notionProperties:
  중요도: No
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.116Z
updated: 2025-03-27T07:53:11.116Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/리포지토리 지원 - QuerydslRepositorySupport-fffdbbdcd64f/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181f4bfb3fffdbbdcd64f
---
<a id="1c3eda9b0fe181d784b9d2322ad61d10"></a>

## QuerydslRepositorySupport

---

> 📖 
> 
> <a id="1c3eda9b0fe1818b969cdedd7bd2b285"></a>
> 
> 이전 버전에서 사용한 방법으로 버전이 업데이트된 현재는 사용 ❌

<details>
<summary><strong>장점</strong></summary>

- <code>getQuerydsl()&#46;applyPagination()</code> 스프링 데이터가 제공하는 페이징을 Querydsl로 편리하게 변환 가능 
    - 단, Sort는 오류 발생

- <code>from()</code>으로 시작 가능
    - 최근에는 QueryFactory를 사용해서 <code>select()</code> 로 시작하는 것이 더 명시

- EntityManager 제공

</details>

<details>
<summary>한계</summary>

- Querydsl 3&#46;x 버전을 대상으로 만듬

- Querydsl 4&#46;x에 나온 JPAQueryFactory로 시작할 수 없음

- select로 시작할 수 없음 (from으로 시작해야함)

- <code>QueryFactory</code> 를 제공하지 않음

- 스프링 데이터 Sort 기능이 정상 동작하지 않음

</details>
