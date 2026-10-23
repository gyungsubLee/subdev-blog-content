---
order: 9
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81aa-a138-db36b214b1ef
title: Spring Data 페이징 활용2 - CountQuery 최적화
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-81aa-a138-db36b214b1ef
    title: Spring Data 페이징 활용2 - CountQuery 최적화
excerpt: Spring Data 페이징 활용2 - CountQuery 최적화 --- 📖 PageableExecutionUtils.getPage() --- PageableExecutionUtils에서 제공하는 getPage() 메서드 사용 시, count 쿼리가 생략 가능한 경우 생략해서 처리한다. - 마지막 페이지이면서 컨텐츠 사
cover: null
icon: null
notionProperties:
  Point: CountQuery 최적화
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.117Z
updated: 2025-04-30T02:48:21.619Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/Spring Data 페이징 활용2 - CountQuery 최적화-db36b214b1ef/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181aaa138db36b214b1ef
---
<a id="1c3eda9b0fe1815d8c1bf2bee7212e0e"></a>

## Spring Data 페이징 활용2 &#45; CountQuery 최적화

---

> 📖 
> 
> <a id="1e5eda9b0fe180bc90d0c86ead240fc5"></a>
> 
> <code>PageableExecutionUtils&#46;getPage()</code>
> 
> ---
> 
> <a id="1c3eda9b0fe1817697b8ca4ca095418e"></a>
> 
> <code>PageableExecutionUtils</code>에서 제공하는 <code>getPage()</code> 메서드 사용 시, count 쿼리가 생략 가능한 경우 생략해서 처리한다&#46; 
> 
> -  마지막 페이지이면서 컨텐츠 사이즈가 페이지 사이즈보다 작을 때 생략 가능
> 
> - <strong>offset &#43; 컨텐츠 사이즈</strong>  로 마지막 페이지 크기를 구함

<details>
<summary><code>PageableExecutionUtils&#46;getPage()</code>로 최적화</summary>

<a id="1c3eda9b0fe18166885dcb832a28ee0a"></a>

```java
JPAQuery<Member> countQuery = queryFactory
        .select(member)
        .from(member)
        .leftJoin(member.team, team)
        .where(usernameEq(condition.getUsername()),
                teamNameEq(condition.getTeamName()),
                ageGoe(condition.getAgeGoe()),
                ageLoe(condition.getAgeLoe()));
                
// return new PageImpl<>(content, pageable, total);
return PageableExecutionUtils.getPage(content, pageable, countQuery::fetchCount);
```

- 스프링 데이터 라이브러리에서 제공된다&#46; 

- count 쿼리가 생략 가능한 경우, 생략해서 처리한다&#46; 
    - 페이지 시작이면서 컨텐츠 사이즈가 페이지 사이즈보다 작을 때

    - 마지막 페이지 일 때
        - offset &#43; 컨텐츠 사이즈를 더해서 전체 사이즈 구함

        - 더 정확히는 마지막 페이지이면서 컨텐츠 사이즈가 페이지 사이즈보다 작을 때 

</details>
