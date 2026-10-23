---
order: 17
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8190-b18d-d6153b6c76ad
title: 조인  - on 절
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-8190-b18d-d6153b6c76ad
    title: 조인  - on 절
excerpt: 조인 - on절 --- 📖 ON 절을 활용한 조인 ( JPA 2.1부터 지원 ) - 조인 대상 필터링 - 연관관계 없는 엔티티 외부 조인 조인 대상 필터링 ex) 회원과 팀을 조인하면서, 팀 이름이 teamA인 팀만 조인, 회원은 모두 조회 SQL sql SELECT m., t. FROM Member m LEFT JOI
cover: null
icon: null
notionProperties:
  ZOVW: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.118Z
updated: 2025-03-27T07:53:11.118Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/조인  - on 절-d6153b6c76ad/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18190b18dd6153b6c76ad
---
<a id="1c3eda9b0fe1813a9512f76b8c2f3c32"></a>

## <strong>조인 </strong>&#45; on<strong>절</strong>

---

> 📖 
> 
> <a id="1c3eda9b0fe181cb8f42c4d6845ab420"></a>
> 
> <code>ON</code> 절을 활용한 조인 ( JPA 2&#46;1부터 지원 )
> 
> -  조인 대상 필터링
> 
> - 연관관계 없는 엔티티 외부 조인

<details>
<summary>조인 대상 필터링</summary>

<details>
<summary>ex) 회원과 팀을 조인하면서, 팀 이름이 teamA인 팀만 조인, 회원은 모두 조회</summary>

<details>
<summary>SQL</summary>

<a id="1c3eda9b0fe181989dbcdd9a2b68dc77"></a>

```sql
SELECT m.*, t.*
FROM Member m
LEFT JOIN Team t
ON m.TEAM_ID=t.id  -- (and t.name='teamA'), WHERE 절 대신 and로 조건 설정 가능
WHERE t.name = 'teamA'
```

</details>

<a id="1c3eda9b0fe18140beeddbf5b8395053"></a>

```java
/**
* 예) 회원과 팀을 조인하면서, 팀 이름이 teamA인 팀만 조인, 회원은 모두 조회
* JPQL: SELECT m, t FROM Member m LEFT JOIN m.team t on t.name = 'teamA'
* SQL: SELECT m.*, t.* FROM Member m LEFT JOIN Team t ON m.TEAM_ID=t.id and
 t.name='teamA'
*/

@Test
public void join_on_filtering() throws Exception {

	   List<Tuple> result = queryFactory
	           .select(member, team)
	           .from(member)
	           .leftJoin(member.team, team).on(team.name.eq("teamA"))
	           .fetch();
	   
	   for (Tuple tuple : result) {
	       System.out.println("tuple = " + tuple);
	   }
}
```

- 결과
    <a id="1c3eda9b0fe181b0baeece1e1aa7fd7c"></a>

    ```plaintext
     t=[Member(id=3, username=member1, age=10), Team(id=1, name=teamA)]
     t=[Member(id=4, username=member2, age=20), Team(id=1, name=teamA)]
     t=[Member(id=5, username=member3, age=30), null]
     t=[Member(id=6, username=member4, age=40), null]
    ```

</details>

> ✏️ 
> 
> <a id="1c3eda9b0fe181d68083d166807fa655"></a>
> 
> <code>on 절</code>을 활용해 조인 대상을 필터링 할 때, 외부조인이 아니라 <u>내부조인(inner join)</u><u>을 사용</u>하면, <u>where 절 에서 필터링 하는 것과 기능이 동일</u>하다&#46;
> 
> -  <u>on 절을 활용한 조인 대상 필터링을 사용</u>할 때,
>     - <u>내부조인</u>이면 익숙한 <code>where 절</code>로 해결
> 
>     - 정말 <u>외부조인이 필요한 경우</u>에만  <u><code>ON 절을</code></u><u> 사용한 필터링</u> 사용

</details>

<details>
<summary>연관관계 없는 엔티티 외부 조인</summary>

<details>
<summary>ex) 회원의 이름과 팀 이름이 같은 대상 &#45; 외부 조인</summary>

<details>
<summary>JPQL</summary>

<a id="1c3eda9b0fe181e6a56be01a432fc175"></a>

```sql
SELECT m, t FROM Member m
LEFT JOIN Team t
ON m.username = t.name
```

</details>

<details>
<summary>SQL</summary>

<a id="1c3eda9b0fe181eebf4fcfe539d29cfc"></a>

```sql
SELECT m.*, t.*
FROM Member m
LEFT JOIN Team t
ON m.username = t.name;
```

</details>

<a id="1c3eda9b0fe181a0ba41dce4efd4e787"></a>

```java
/**
* 2. 연관관계 없는 엔티티 외부 조인
* 예) 회원의 이름과 팀의 이름이 같은 대상 외부 조인
* JPQL: SELECT m, t FROM Member m LEFT JOIN Team t on m.username = t.name
* SQL: SELECT m.*, t.* FROM Member m LEFT JOIN Team t ON m.username = t.name 
*/
@Test
public void join_on_no_relation() throws Exception {

		em.persist(new Member("teamA"));
		em.persist(new Member("teamB"));
		
		List<Tuple> result = queryFacory
						.select(member, team)
						.from(member)
						.left join(team).on(member.username.eq(team.name))
						.fetch();
		       
		for (Tuple tuple : result) {
		   System.out.println("t=" + tuple);
		}
}
```

- 하이버네이트 5&#46;1부터 <code>on</code>을 사용해서 서로 관계가 없는 필드로 외부 조인하는 기능이 추가되었다&#46;
    - 내부 조인도 가능

- 결과
    <a id="1c3eda9b0fe18121b494d4a741dd5eb9"></a>

    ```java
     t=[Member(id=3, username=member1, age=10), null]
     t=[Member(id=4, username=member2, age=20), null]
     t=[Member(id=5, username=member3, age=30), null]
     t=[Member(id=6, username=member4, age=40), null]
     t=[Member(id=7, username=teamA, age=0), Team(id=1, name=teamA)]
     t=[Member(id=8, username=teamB, age=0), Team(id=2, name=teamB)]
    ```

> ☝🏻 
> 
> <a id="1c3eda9b0fe18197b165fcf802449413"></a>
> 
> 주의) <code>leftJoin()</code>은 <code>일반 조인</code>과 달리  <u><code>on 조인</code></u><u> 시 엔티티 </u><strong><u>하나</u></strong><u>만 들</u>어간다&#46;
> 
> - 일반조인&#58; <code>leftJoin(member&#46;team, team)</code>
> 
> - on조인&#58; <code>from(member)&#46;leftJoin(team)&#46;on(xxx)</code>

</details>

</details>
