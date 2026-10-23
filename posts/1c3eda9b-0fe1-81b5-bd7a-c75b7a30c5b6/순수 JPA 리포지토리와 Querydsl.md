---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81b5-bd7a-c75b7a30c5b6
title: 순수 JPA 리포지토리와 Querydsl
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-81b5-bd7a-c75b7a30c5b6
    title: 순수 JPA 리포지토리와 Querydsl
excerpt: "순수 JPA 리포지토리와 Querydsl --- 📖 순수 JPA [ 코드 ] Repository: MemberJpaRepository java package com.example.lectureprac.repository; import com.example.lectureprac.entity.Member; import co"
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.117Z
updated: 2025-05-18T13:41:30.812Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/순수 JPA 리포지토리와 Querydsl-c75b7a30c5b6/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181b5bd7ac75b7a30c5b6
---
<a id="1c3eda9b0fe1810cbc87cb1e4bbe0df3"></a>

## 순수 JPA 리포지토리와 Querydsl

---

> 📖 

<details>
<summary>순수 JPA</summary>

<details>
<summary>&#91; 코드 &#93; <code>Repository</code>&#58; MemberJpaRepository</summary>

<a id="1c3eda9b0fe181d39e8cf150ad17481c"></a>

```java
package com.example.lectureprac.repository;

import com.example.lectureprac.entity.Member;
import com.querydsl.jpa.impl.JPAQueryFactory;
import jakarta.persistence.EntityManager;
import org.springframework.stereotype.Repository;

import java.util.List;
import java.util.Optional;

@Repository
public class MemberJpaRepository {

    private final EntityManager em;
    private final JPAQueryFactory queryFactory;

    public MemberJpaRepository(EntityManager em) {
        this.em = em;
        this.queryFactory = new JPAQueryFactory(em);
    }

    public void save(Member member) {
        em.persist(member);
    }

    public Optional<Member> findById(Long id) {
        Member findMember = em.find(Member.class, id);
        return Optional.ofNullable(findMember);
    }

    public List<Member> findAll() {
        return em.createQuery("SELECT m from Member m", Member.class)
                .getResultList();
    }

    public List<Member> findByUsername(String username) {
        return em.createQuery("select m from Member m where m.username = :username", Member.class)
                .setParameter("username", username)
                .getResultList();
    }
}

```

</details>

<details>
<summary>&#91; 코드 &#93; 테스트 코드</summary>

<a id="1c3eda9b0fe181af81f0ecf801c46223"></a>

```java
package com.example.lectureprac.repository;

import com.example.lectureprac.entity.Member;
import jakarta.persistence.EntityManager;
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

import static org.assertj.core.api.Assertions.assertThat;

@SpringBootTest
@Transactional
class MemberJpaRepositoryTest {

        @Autowired
        EntityManager em;
        @Autowired
        MemberJpaRepository memberJpaRepository;

        @Test
        public void basicTest() {

            Member member = new Member("member1", 10);
            memberJpaRepository.save(member);

            Member findMember = memberJpaRepository.findById(member.getId()).get();
            assertThat(findMember).isEqualTo(member);

            List<Member> result1 = memberJpaRepository.findAll();
            assertThat(result1).containsExactly(member);

            List<Member> result2 = memberJpaRepository.findByUsername("member1");
            assertThat(result2).containsExactly(member);

      }
}
```

<a id="1c3eda9b0fe18139a6dad8ba3155444e"></a>

<br>

<details>
<summary>쿼리 확인</summary>

<a id="1c3eda9b0fe181209f0dc938c50078b2"></a>

```sql
Hibernate: 
    /* insert for
        com.example.lectureprac.entity.Member */insert 
    into
        member (age, team_id, username) 
    values
        (?, ?, ?)
Hibernate: 
    /* SELECT
        m 
    from
        Member m */ select
            m1_0.id,
            m1_0.age,
            m1_0.team_id,
            m1_0.username 
        from
            member m1_0
Hibernate: 
    /* select
        m 
    from
        Member m 
    where
        m.username = :username */ select
            m1_0.id,
            m1_0.age,
            m1_0.team_id,
            m1_0.username 
        from
            member m1_0 
        where
            m1_0.username=?

```

</details>

</details>

</details>

<details>
<summary>Querydls</summary>

<details>
<summary>Querydsl로 변경</summary>

- <code>findAll()</code>
    <a id="1c3eda9b0fe18168a00ddde789332296"></a>

    ```java
    public List<Member> findAll_Querydsl() {
        return queryFactory
                .selectFrom(member).fetch();
    }
    ```

- <code>findByUsername()</code>
    <a id="1c3eda9b0fe18177a88af4a6a1a52bdc"></a>

    ```java
    public List<Member> findByUsername_Querydsl(String username) {
        return queryFactory
                .selectFrom(member)
                .where(member.username.eq(username))
                .fetch();
    }
    ```

</details>

<details>
<summary>&#91; 코드 &#93; 테스트 코드</summary>

<a id="1c3eda9b0fe181e98682de8912571f9d"></a>

```java
@Test
public void basicTest_Querydsl() {

    Member member = new Member("member1", 10);
    memberJpaRepository.save(member);

    List<Member> result1 = memberJpaRepository.findAll_Querydsl();
    assertThat(result1).containsExactly(member);

    List<Member> result2 = memberJpaRepository.findByUsername_Querydsl("member1");
    assertThat(result2).containsExactly(member);
}
```

<details>
<summary>쿼리 확인</summary>

<a id="1c3eda9b0fe181358923d3c958194ff5"></a>

```java
Hibernate: 
    /* insert for
        com.example.lectureprac.entity.Member */insert 
    into
        member (age, team_id, username) 
    values
        (?, ?, ?)
Hibernate: 
    /* select
        member1 
    from
        Member member1 */ select
            m1_0.id,
            m1_0.age,
            m1_0.team_id,
            m1_0.username 
        from
            member m1_0
Hibernate: 
    /* select
        member1 
    from
        Member member1 
    where
        member1.username = ?1 */ select
            m1_0.id,
            m1_0.age,
            m1_0.team_id,
            m1_0.username 
        from
            member m1_0 
        where
            m1_0.username=?
```

</details>

</details>

---

- Querydsl은 기본적으로 조건(<code>&#46;where()</code>)에서 파라미터 바인딩 처리를 해준다&#46; 

- 컴파일에서 문법 오류를 잡아준다&#46; 
    - JPQL은 런타임 시에 확인 가능하다&#46; 

</details>

<details>
<summary><code>JPAQueryFactory</code>  의존성 주입 방법</summary>

> <code>JPAQueryFactory</code> 생성 시, <code>EntityManager</code>를 인자로 넣어줘야 한다&#46; 

<details>
<summary>1&#46; <code>JPAQueryFactory</code>를 생성자에서 인스턴스를 생성</summary>

<a id="1c3eda9b0fe181ea8c05c6135803aa46"></a>

```java
@Repository
public class MemberJpaRepository {

    private final EntityManager em;
    private final JPAQueryFactory queryFactory;

    public MemberJpaRepository(EntityManager em) {
        this.em = em;
        this.queryFactory = new JPAQueryFactory(em);
    }
    
    . . .
```

- 테스트 코드 작성 시, <code>JPAQueryFactory</code>를 주입하지 않아도 된다&#46;
    - MemberJpaRepository 의존성 주입 시, 내부에서 인스턴스를 생성하기 때문에<br><code>JPAQueryFactory</code>의 의존성을 따로 주입하지 않아도 된다&#46; 

    <a id="1c3eda9b0fe18175a3b0f5c5001f06c3"></a>

    ```java
    @SpringBootTest
    @Transactional
    class MemberJpaRepositoryTest {

            @Autowired
            EntityManager em;
            @Autowired
            MemberJpaRepository memberJpaRepository;
    ```

</details>

<details>
<summary>2&#46; <u>bean으로 등록</u>해서 주입해도 된다&#46; </summary>

- root 클래스에 bean 선언
    - config로 따로 빼줘도 된다&#46; 

    <a id="1c3eda9b0fe181ccab64c01c6050772e"></a>

    ```java
    @SpringBootApplication
    public class LecturePracApplication {

        public static void main(String[] args) {
            SpringApplication.run(LecturePracApplication.class, args);
        }
    		
    		// 빈 등록
        @Bean
        JPAQueryFactory jpaQueryFactory(EntityManager em) {
            return new JPAQueryFactory(em);
        }
    }
    ```

- 생성자 주입
    <a id="1c3eda9b0fe181ddb98fe18c82bbcf7c"></a>

    ```java
    @Repository
    public class MemberJpaRepository {

        private final EntityManager em;
        private final JPAQueryFactory queryFactory;

        public MemberJpaRepository(EntityManager em, JPAQueryFactory queryFactory) {
            this.em = em;
            this.queryFactory = queryFactory;
        }
        
        . . .
    ```

- 테스트 코드 작성 시, <code>JPAQueryFactory</code>를 주입해야 된다&#46;&#46;<code> </code>

</details>

</details>

<details>
<summary>🧐 위 처럼 사용 시, 멀티스레딩 환경에서의 동시성 문제가 발생되지 않는가?</summary>

<a id="1c3eda9b0fe1817c9738eb0fc9a56dc0"></a>

엔티티 매니저가 스프링이랑 엮어서 쓰면 동시성 문제랑 전혀 관계없이 트랜잭션 단위로 다 따로따로 분리해서 동작한다&#46; 

<a id="1c3eda9b0fe181569d78fa5aa0f69b68"></a>

EntityManager 사용 시, 진짜 EntityManager가 아닌 프록시  객체인 가짜 객체를 주입한다&#46;

<a id="1c3eda9b0fe1819ea147eb1be6f2a2dd"></a>

따라서 멀티쓰레딩 환경에서 동시성문제를 걱정하지 않아도 된다&#46; 

</details>

- 자세한 내용은 자바 ORM 표준 JPA 책 13&#46;1 트랜잭션 범위의 영속성 컨텍스트 참고
