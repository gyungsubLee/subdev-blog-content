---
order: 31
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-811f-bf24-d8256c8eccec
title: 인터페이스 지원 - QuerydslPredicateExecutor
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-811f-bf24-d8256c8eccec
    title: 인터페이스 지원 - QuerydslPredicateExecutor
excerpt: 인터페이스 지원 - QuerydslPredicateExecutor --- 📖 공식 사이트 [Spring Data JPA - Reference Documentation]() QuerydslPredicateExecutor 적용 및 사용 - QuerydslPredicateExecutor 인터페이스 java public int
cover: null
icon: null
notionProperties:
  중요도: No
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.116Z
updated: 2025-03-27T07:53:11.116Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/인터페이스 지원 - QuerydslPredicateExecutor-d8256c8eccec/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1811fbf24d8256c8eccec
---
<a id="1c3eda9b0fe1813eaab7d87aeb102fc2"></a>

## <strong>인터페이스 지원 </strong>&#45; QuerydslPredicateExecutor

---

> 📖 

<details>
<summary>공식 사이트</summary>

[Spring Data JPA &#45; Reference Documentation]()

</details>

<details>
<summary>QuerydslPredicateExecutor  적용 및 사용</summary>

-  QuerydslPredicateExecutor 인터페이스
    <a id="1c3eda9b0fe1816cb1e0de163d6c6f7a"></a>

    ```java
    public interface QuerydslPredicateExecutor<T> {

    		Optional<T> findById(Predicate predicate);
    		Iterable<T> findAll(Predicate predicate);
    		long count(Predicate predicate);
    		boolean exists(Predicate predicate);
    		
    		// ... more functionality omitted.
    }

    ```

- 리포지토리에 적용
    <a id="1c3eda9b0fe18101bd44fddeed4d7840"></a>

    ```java
    interface MemberRepository extends 
    					JpaRepository<User, Long>, 
    					QuerydslPredicateExecutor<User> {
    }
    ```

- 서비스에서 사용
    <a id="1c3eda9b0fe1813c9134ec1901b50e5e"></a>

    ```java
    Iterable result = memberRepository.findAll(
             member.age.between(10, 40)
    				 .and(member.username.eq("member1"))         
    );
    ```

</details>

> ☝🏻 
> 
> <a id="1c3eda9b0fe1811ba47ed96a3ab7d49d"></a>
> 
> 한계점
> 
> - 조인X (묵시적 조인은 가능하지만 left join이 불가능)
> 
> - 클라이언트가 Querydsl에 의존해야 한다&#46; <br>서비스 클래스가 Querydsl이라는 구현 기술에 의존해야 한다&#46;
> 
> - 복잡한 실무환경에서 사용하기에는 한계가 명확하다&#46;

> 참고&#58; <code>QuerydslPredicateExecutor</code> 는 Pagable, Sort를 모두 지원하고 정상 동작한다&#46;
