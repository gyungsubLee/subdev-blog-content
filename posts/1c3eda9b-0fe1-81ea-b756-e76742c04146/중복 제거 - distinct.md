---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81ea-b756-e76742c04146
title: 중복 제거 - distinct
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-81ea-b756-e76742c04146
    title: 중복 제거 - distinct
excerpt: 중복 제거 - distinct --- 📖 Querydsl에서 SQL에서 중복 제거 시 사용하는 distinct를 지원한다. - .distinct() - select() 뒤에 명시한다. - JPQL의 distinct와 동일하다. 예시 java List result = queryFactory .select(member.us
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.119Z
updated: 2025-10-21T15:54:37.739Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/중복 제거 - distinct-e76742c04146/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181eab756e76742c04146
---
<a id="1c3eda9b0fe1816caa42fce436253410"></a>

## 중복 제거 &#45; <code>distinct</code>

---

> 📖 
> 
> <a id="1c3eda9b0fe18114b9d4fe7e129f85aa"></a>
> 
>  Querydsl에서 SQL에서 중복 제거 시 사용하는 <code>distinct</code>를 지원한다&#46;
> 
> - <code>&#46;distinct()</code>
>     - <code>select()</code> 뒤에 명시한다&#46;
> 
>     - JPQL의 distinct와 동일하다&#46;

<details>
<summary>예시 </summary>

<a id="1c3eda9b0fe1811e9503fbf0da4ed3bd"></a>

```java
List<String> result = queryFactory
         .select(member.username).distinct()
         .from(member)
         .fetch();
```

</details>
