---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8100-b401-c34b7d4d3e1c
title: JPQL vs QueryDSL
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-8100-b401-c34b7d4d3e1c
    title: JPQL vs QueryDSL
excerpt: 기본 테스트 코드 java @SpringBootTest @Transactional public class QuerydslBasicTest { @PersistenceContext EntityManager em; @BeforeEach public void before() { Team teamA = new Team("teamA
cover: null
icon: null
notionProperties:
  Point: JPQL, QueryDSL 비교, 동시성 문제
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.119Z
updated: 2025-03-27T07:53:11.119Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/JPQL vs QueryDSL-c34b7d4d3e1c/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18100b401c34b7d4d3e1c
---
<details>
<summary>기본 테스트 코드 </summary>

<a id="1c3eda9b0fe181d1b458ea4c5576419e"></a>

```java
 @SpringBootTest
 @Transactional
 public class QuerydslBasicTest {
 
     @PersistenceContext
     EntityManager em;
     
     @BeforeEach
     public void before() {
         Team teamA = new Team("teamA");
         Team teamB = new Team("teamB");
         
         em.persist(teamA);
         em.persist(teamB);
         
         Member member1 = new Member("member1", 10, teamA);
         Member member2 = new Member("member2", 20, teamA);
         Member member3 = new Member("member3", 30, teamB);
         Member member4 = new Member("member4", 40, teamB);
         em.persist(member1);
         em.persist(member2);
         em.persist(member3);
         em.persist(member4);
		} 
}
```

</details>

<a id="1c3eda9b0fe181e99053ec10b16c5530"></a>

## JPQL vs QueryDSL 

---

<a id="1c3eda9b0fe181dd872bc44ad964a1a9"></a>

### JPQL

<a id="1c3eda9b0fe1815bb7d1fc60fc0bbd0f"></a>

```java
//JPQL 
@Test
public void startJPQL() {
		//member1 조회
		String qlString =
           "select m from Member m " +
           "where m.username = :username";
    
    Member findMember = em.createQuery(qlString, Member.class)
             .setParameter("username", "member1")
             .getSingleResult();
    
    assertThat(findMember.getUsername()).isEqualTo("member1");
}
```

<a id="1c3eda9b0fe18129aa40f88839686c9e"></a>

### QueryDSL

<details>
<summary>QueryDSL 문법</summary>

- <code>queryFactory</code>

- <code>&#46;select(Q클래스)</code>

- <code>&#46;from(Q클래스)</code>

- <code>&#46;where(Q클래스&#46;필드&#46;eq( {조건값} ))</code>

- <code>&#46;fetchOne();</code>

</details>

<a id="1c3eda9b0fe181f7b1b3fb1770e9d0ce"></a>

```java
// QueryDSL
@Test
public void startQuerydsl() {
			//member1 조회
			JPAQueryFactory queryFactory = new JPAQueryFactory(em); 
			
			QMember m = new QMember("m");
	    Member findMember = queryFactory
	             .select(m)
							 .from(m)
							 .where(m.username.eq("member1"))//파라미터 바인딩 처리 
							 .fetchOne();
			
	    assertThat(findMember.getUsername()).isEqualTo("member1");
 }
```

- JPAQueryFactory<strong> 필드</strong>

<a id="1c3eda9b0fe181a3a934d0ed6500dba5"></a>

```java

JPAQueryFactory queryFactory;

@BeforeEach
public void before() {
    queryFactory = new JPAQueryFactory(em);
    
    ...
}

@Test
public void startQuerydsl2() {
    //member1 조회
    QMember m = new QMember("m");
    Member findMember = queryFactory
            .select(m)
            .from(m)
            .where(m.username.eq("member1"))
            .fetchOne();

    assertThat(findMember.getUsername()).isEqualTo("member1");
}
```

<a id="1c3eda9b0fe181f7a5d0f84d4f041a24"></a>

### 동시성 문제

---

> 🧐 
> 
> <a id="1c3eda9b0fe181c3bc9cd72a66afcde8"></a>
> 
> JPAQueryFactory를 필드로 제공하면 동시성 문제는 어떻게 될까? 
> 
> <a id="1c3eda9b0fe18180a023d19cc1078498"></a>
> 
> 동시성 문제는 <u>JPAQueryFactory를 생성</u> 할 때 제공하는 <u>EntityManager(em)</u>에 달려있다&#46; <br>스프링 프레임워크는 <u>여러 쓰레드에서 동시에 같은 EntityManager에 접근</u>해도, 트랜잭션 마다 별도의 영속성 컨텍스트를 제공하기 때문에, <u>동시성 문제는 걱정하지 않</u>아도 된다&#46;
