---
order: 8
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8114-b53e-f893101592e8
title: Spring Data 페이징 활용3 - 컨트롤러 개발
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-8114-b53e-f893101592e8
    title: Spring Data 페이징 활용3 - 컨트롤러 개발
excerpt: "스프링 데이터 페이징 활용3 - 컨트롤러 개발 --- 📖 paging 로직을 호출할 API 개발 Controller: MemberController ✏️ 호출 url --- - http://localhost:8080/v2/members?size=5&page=2 - http://localhost:8080/v3/member"
cover: null
icon: null
notionProperties:
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.117Z
updated: 2025-04-30T02:54:58.061Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/Spring Data 페이징 활용3 - 컨트롤러 개발-f893101592e8/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18114b53ef893101592e8
---
<a id="1c3eda9b0fe18165a6ddf3b2e20654f3"></a>

## <strong>스프링 데이터 페이징 활용</strong>3 &#45; <strong>컨트롤러 개발</strong>

---

> 📖 
> 
> <a id="1c3eda9b0fe181109b5bc12198ca66fb"></a>
> 
> paging 로직을 호출할 API 개발

<details>
<summary><code>Controller</code>&#58;  MemberController</summary>

> ✏️ 
> 
> <a id="1e5eda9b0fe1803794b5ed9fc25c29c1"></a>
> 
> <strong>호출 url</strong>
> 
> ---
> 
> - <code>http&#58;//localhost&#58;8080/v2/members?size=5&#38;page=2</code>
> 
> - <code>http&#58;//localhost&#58;8080/v3/members?size=5&#38;page=2</code>

<a id="1c3eda9b0fe181c7a462e6e6af84d426"></a>

```java
 @RestController
 @RequiredArgsConstructor
 public class MemberController {
 
     private final MemberJpaRepository memberJpaRepository;
     private final MemberRepository memberRepository;
     
     @GetMapping("/v1/members")
     public List<MemberTeamDto> searchMemberV1(MemberSearchCondition condition) {
         return memberJpaRepository.search(condition);
     }
     
     @GetMapping("/v2/members")
     public Page<MemberTeamDto> searchMemberV2(MemberSearchCondition condition, Pageable pageable) {
         return memberRepository.searchPageSimple(condition, pageable);
     }
     
     @GetMapping("/v3/members")
     public Page<MemberTeamDto> searchMemberV3(MemberSearchCondition condition, Pageable pageable) {
         return memberRepository.searchPageComplex(condition, pageable);
     }
}
```

</details>

<details>
<summary>스프링 데이터 정렬(Sort)</summary>

> ☝🏻 
> 
> <a id="1c3eda9b0fe181f3b2a1dfaef994536b"></a>
> 
> 정렬( <code>Sort</code> )은 조건이 조금만 복잡해져도 <code>Pageable</code> 의 <code>Sort</code> 기능을 사용하기 어렵다&#46; <u>루트 엔티티 범위를 넘어가는 동적 정렬 기능이 필요</u>하면 스프링 데이터 페이징이 제공하는 <code>Sort</code> 를 사용하기 보다는 <strong><u>파라미터를 받아서 직접 처리하는 것을 권장</u></strong>한다&#46;

<a id="1c3eda9b0fe181148c3bce27237d2483"></a>

스프링 데이터 JPA는 자신의 정렬(Sort)을 Querydsl의 정렬(OrderSpecifier)로 편리하게 변경하는 기능을 제공한다,

- 스프링 데이터 JPA가 제공하는 Querydsl 기능 참고

> ✏️ 
> 
> <a id="1e5eda9b0fe18024bc04fad4e5cc7158"></a>
> 
> <strong>스프링 데이터 </strong><strong><code>Sort</code></strong><strong>를 Querydsl의 </strong><strong><code>OrderSpecifier</code></strong><strong>로 변환</strong>
> 
> - 스프링 데이터의 정렬을 Querydsl의 정렬로 직접 전환하는 방법

<a id="1c3eda9b0fe18199ac7ef5e9cfaf7ea8"></a>

```java
JPAQuery<Member> query = queryFactory
					.selectFrom(member);

for (Sort.Order o : pageable.getSort()) {
		 PathBuilder pathBuilder = new PathBuilder(member.getType(), member.getMetadata());
		 query.orderBy(new OrderSpecifier(o.isAscending() ? Order.ASC : Order.DESC, pathBuilder.get(o.getProperty())));
}

List<Member> result = query.fetch();
```

</details>
