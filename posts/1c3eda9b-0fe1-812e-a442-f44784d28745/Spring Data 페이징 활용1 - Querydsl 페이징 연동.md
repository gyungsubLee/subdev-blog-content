---
order: 10
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-812e-a442-f44784d28745
title: Spring Data 페이징 활용1 - Querydsl 페이징 연동
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-812e-a442-f44784d28745
    title: Spring Data 페이징 활용1 - Querydsl 페이징 연동
excerpt: "Spring Data 페이징 활용1 - Querydsl 페이징 연동 --- 📖 - offset(): 몇번 부터 시작할 거냐? - limit(): 한번 조회할 때 몇 개 가져올거야? - fetchResults(): 컨텐츠용 쿼리, 카운트 쿼리 2번을 날림 사용자 정의 인터페이스에 페이징 메서드 정의 - import org"
cover: null
icon: null
notionProperties:
  Point: "`pageable.getOffset()`, `pageable.getPageSize()`"
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.117Z
updated: 2025-04-30T02:45:16.552Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/Spring Data 페이징 활용1 - Querydsl 페이징 연동-f44784d28745/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1812ea442f44784d28745
---
<a id="1c3eda9b0fe1813ebfc0d1af732a0ae7"></a>

## Spring Data 페이징 활용1 &#45; Querydsl 페이징 연동

---

> 📖 
> 
> - <code>offset()</code>&#58; 몇번 부터 시작할 거냐?
> 
> - <code>limit()</code>&#58; 한번 조회할 때 몇 개 가져올거야? 
> 
> - <code>fetchResults()</code>&#58; 컨텐츠용 쿼리, 카운트 쿼리 2번을 날림

<details>
<summary><u>사용자 정의 인터페이스</u>에 <strong>페이징 메서드 정의</strong></summary>

- <code> import org&#46;springframework&#46;data&#46;domain&#46;Page;</code>

- <code> import org&#46;springframework&#46;data&#46;domain&#46;Pageable;</code>

<a id="1c3eda9b0fe1814e8609f118a9327471"></a>

```java
 public interface MemberRepositoryCustom {
     List<MemberTeamDto> search(MemberSearchCondition condition);
     Page<MemberTeamDto> searchPageSimple(MemberSearchCondition condition,Pageable pageable);
     Page<MemberTeamDto> searchPageComplex(MemberSearchCondition condition,Pageable pageable);
 }
```

</details>

<details>
<summary>전체 카운트를 한번에 조회하는 단순한 방법 &#45; <code>fetchResults()</code></summary>

<a id="1c3eda9b0fe18108973ad223090120e6"></a>

```java
/**
* 단순한 페이징, fetchResults() 사용
*/
@Override
public Page<MemberTeamDto> searchPageSimple(MemberSearchCondition condition,Pageable pageable) {
	   QueryResults<MemberTeamDto> results = queryFactory
	           .select(new QMemberTeamDto(
	                   member.id,
	                   member.username,
	                   member.age,
	                   team.id,
	                   team.name))
	           .from(member)
	           .leftJoin(member.team, team)
	           .where(usernameEq(condition.getUsername()),
	                   teamNameEq(condition.getTeamName()),
	                   ageGoe(condition.getAgeGoe()),
	                   ageLoe(condition.getAgeLoe()))
	           .offset(pageable.getOffset())
	           .limit(pageable.getPageSize())
	           .fetchResults();
	           
	   List<MemberTeamDto> content = results.getResults();
	   
	   long total = results.getTotal();
	   
	   return new PageImpl<>(content, pageable, total);
}
```

- Querydsl이 제공하는 <code>fetchResults()</code> 를 사용하면 내용과 전체 카운트를 한번에 조회할 수 있다 (실제 쿼리 는 2번 호출)

- <code>fetchResult()</code> 는 카운트 쿼리 실행시 필요없는 <code>order by</code> 는 제거한다&#46;

</details>

<details>
<summary>데이터 내용과 <u>전체 카운트를 별도로 조회</u>하는 방법  &#45; 직접 카운트 쿼리 작성</summary>

<a id="1c3eda9b0fe1812a99a3e2a59d0b17d2"></a>

```java
/**
* 복잡한 페이징
* 데이터 조회 쿼리와, 전체 카운트 쿼리를 분리 
*/
@Override
public Page<MemberTeamDto> searchPageComplex(MemberSearchCondition condition,Pageable pageable) {

		List<MemberTeamDto> content = queryFactory
            .select(new QMemberTeamDto(
                    member.id,
                    member.username,
                    member.age,
                    team.id,
                    team.name))
            .from(member)
            .leftJoin(member.team, team)
            .where(usernameEq(condition.getUsername()),
                    teamNameEq(condition.getTeamName()),
                    ageGoe(condition.getAgeGoe()),
                    ageLoe(condition.getAgeLoe()))
            .offset(pageable.getOffset())
            .limit(pageable.getPageSize())
            .fetch();
           
		long total = queryFactory
            .select(member)
            .from(member)
            .leftJoin(member.team, team)
            .where(usernameEq(condition.getUsername()),
                    teamNameEq(condition.getTeamName()),
                    ageGoe(condition.getAgeGoe()),
                    ageLoe(condition.getAgeLoe()))
            .fetchCount();
		
		return new PageImpl<>(content, pageable, total);
}

```

- 전체 카운트를 조회 하는 방법을 최적화 할 수 있으면 위와 같이 분리하는 것이 좋다&#46; 
    - ex) 전체 카운트를 조회할 때 조인 쿼리를 줄일 수 있다면 상당한 효과가 있다&#46; 

- 코드를 리펙토링해서 내용 쿼리와 전체 카운트 쿼리를 읽기 좋게 분리하면 좋다&#46; 

<details>
<summary>🧐 <strong>페이징</strong> ( <strong>Pageable</strong> )</summary>

<a id="1c3eda9b0fe181d1b82aef36c30f9e1e"></a>

Pageable에는 유저로부터 입력받은 페이징 숫자, 내부 엔티티 개수, 정렬 정보 등을 받아와 저장한다&#46; 

- Controller &#45; Pageable
    <a id="1c3eda9b0fe181469bcffc48a095063e"></a>

    ```java
    @GetMapping("/cards")
    public Page<Card> getCards(
            @RequestParam(required = false) Long cardId,
            @RequestParam(required = false) String title,
            Pageable pageable) {
        return cardService.findCardsByIdOrTitleOrderByCreatedAtDesc(cardId, title, pageable);
    }
    ```

- page 와 size를 받아 직접 생성
    <a id="1c3eda9b0fe181fab21ce0b778b4971a"></a>

    ```java
    PageRequest pageable = PageRequest.of(page, size, Sort.by("createdAt").descending());
    ```

    <details>
    <summary>&#91; 코드 &#93; Controller</summary>

    <a id="1e5eda9b0fe180818407cfbd0ae0880f"></a>

    ```java
    @RestController
    @RequiredArgsConstructor
    @RequestMapping("/posts")
    public class PostController {

        private final PostService postService;

        @GetMapping
        public ResponseEntity<Page<Post>> getPosts(
                @RequestParam(defaultValue = "0") int page,
                @RequestParam(defaultValue = "10") int size
        ) {
            Page<Post> result = postService.getPosts(page, size);
            return ResponseEntity.ok(result);
        }
    }
    ```

    </details>

    <details>
    <summary>&#91; 코드 &#93; Service</summary>

    <a id="1e5eda9b0fe180778268df97b3708a3b"></a>

    ```java
    @Service
    @RequiredArgsConstructor
    public class PostService {

        private final PostRepository postRepository;

        public Page<Post> getPosts(int page, int size) {
            PageRequest pageable = PageRequest.of(page, size, Sort.by("createdAt").descending());
            return postRepository.findAll(pageable);
        }
    }
    ```

    </details>

</details>

<details>
<summary>🧐 전체 카운트, 카운트 쿼리가 뭐지? </summary>

> ✏️ 
> 
> <a id="1e5eda9b0fe18014882ac10bfa5568f8"></a>
> 
> 페이징 처리에서 <strong>전체 카운트 쿼리(count query)</strong> 가 필요한 이유
> 
> <a id="1e5eda9b0fe1809e9db4e7b7be65e288"></a>
> 
> <strong>→ 전체 페이지 수 계산을 위해서</strong>

<a id="1e5eda9b0fe1807a9776f71d06ca5f70"></a>

페이징 처리 시, Spring Data JPA의 <code>Page&#60;T&#62;</code>는 단순히 해당 페이지 데이터만 조회하는 것이 아니라

<a id="1e5eda9b0fe180ee8c58c15739c90058"></a>

아래의 정보도 함께 제공한다&#46; 

| <strong>정보</strong> | <strong>설명</strong> |
| --- | --- |
| <code>getTotalElements()</code> | • 전체 데이터 개수 |
| <code>getTotalPages()</code> | • 전체 페이지 수 |
| <code>hasNext()</code> <br><code>hasPrevious()</code> | • 다음 페이지<br>• 이전 페이지 존재 여부 |
| <code>isFirst()</code><br><code>isLast()</code>  | • 첫 번째 페이지 여부<br>• 마지막 페이지 여부 |

<a id="1e5eda9b0fe180bcbf18d04c333abba1"></a>

위 에 대한 정보를 계산하려면 <u>전체 행의 개수가 필요</u>하다&#46; <br>따라서 <strong><u>JPA는 페이징</u></strong><strong> 시 </strong><strong>자동으로 count 쿼리도 실행</strong><strong>한다&#46;</strong>

<details>
<summary>예시) 실제 실행 쿼리 ( 데이터 조회 &#43; 전체 카운팅 )</summary>

<a id="1e5eda9b0fe180da9e5fcdfbf8c182ff"></a>

```sql
-- 실제 데이터 조회 (LIMIT + OFFSET)
SELECT * FROM post ORDER BY created_at DESC LIMIT 10 OFFSET 0;

-- 전체 개수 조회
SELECT COUNT(*) FROM post;
```

</details>

> 🚨 
> 
> <a id="1e5eda9b0fe180f68756ccc0aa31881a"></a>
> 
> <strong>&#91; 성능 이슈 &#93;</strong><strong>  Count 쿼리는 </strong><strong><u>느릴 수 있</u></strong><strong>다</strong>
> 
> ---
> 
> <a id="1e5eda9b0fe1808e9c97f56ab31d199b"></a>
> 
> 조인이 복잡하거나, 조건이 많거나, 테이블이 크면 COUNT(&#42;) 도 <strong>성능 병목이 된다&#46; </strong>
> 
> - 위 경우 모든 쿼리는 다 병목이 된다&#46;

<a id="1e5eda9b0fe180ada968decc2091aeca"></a>

따라서 실무에서는 아래과 같은 방법을 고려한다&#46;

| <strong>전략</strong> | <strong>설명</strong> |
| --- | --- |
| <strong><code>Slice</code></strong><code> 사용</code> | Page 대신 Slice를 사용하면 count 쿼리를 생략할 수 있음 (hasNext만 판단) |
| <strong><code>커스텀 쿼리 분리</code></strong> | 데이터 조회 쿼리와 count 쿼리를 따로 최적화 |
| <strong><code>카운트를 캐싱</code></strong> | 자주 안 바뀌는 목록이라면 Redis나 DB에 미리 계산해두기 |
| <strong><code>서브쿼리 제거</code></strong> | 복잡한 count 쿼리를 단순화하거나 native SQL로 분리 |

<details>
<summary>ex) <strong><code>Slice&#60;T&#62;</code></strong><strong> (Spring Data JPA 지원)</strong></summary>

> ✏️ 
> 
> <a id="1e5eda9b0fe1808fa210c5da4a5c7b87"></a>
> 
> <code>Page&#60;T&#62;</code> 대신 <code>Slice&#60;T&#62;</code>를 사용하면 <strong>count 쿼리를 실행하지 않는다&#46;</strong>
> 
> - Slice는 <strong>“다음 페이지가 있는지 여부만 알려주는 방식”</strong> 으로 동작한다&#46; 

- <code>COUNT(&#42;)</code> 쿼리가 안 나가서 <strong>성능이 훨씬 좋음</strong>

- 무한 스크롤(인스타, 유튜브)처럼 ‘더보기’ 방식에 적합

- 전체 페이지 수, 전체 항목 수를 알 수 없음

- <code>getTotalPages()</code> 불가능

</details>

</details>

</details>
