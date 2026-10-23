---
order: 23
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81e5-a30a-dbc65bd17de5
title: Spring Data JPA repository
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-81e5-a30a-dbc65bd17de5
    title: Spring Data JPA repository
excerpt: Spring Data JPA repository --- 📖 Spring Data JPA 사용 시, 간단하게 repository계층을 설계할 수 있다. - JpaRepository를 상속하여 구현한다. - 대부분의 기본 crud 메서드를 지원한다. - 순수 JPA에서 Spring Data JPA로 변경 MemberRepo
cover: null
icon: null
notionProperties:
  중요도: No
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.117Z
updated: 2025-03-27T07:53:11.117Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/Spring Data JPA repository-dbc65bd17de5/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181e5a30adbc65bd17de5
---
<a id="1c3eda9b0fe181bb85cee3ca7eb8faf6"></a>

## Spring Data JPA repository

---

> 📖 
> 
> <a id="1c3eda9b0fe181668533eb8db6e7f675"></a>
> 
> Spring Data JPA 사용 시, 간단하게 repository계층을 설계할 수 있다&#46; 
> 
> - JpaRepository를 상속하여 구현한다&#46;
> 
> - 대부분의 기본 crud 메서드를 지원한다&#46; 

- 순수 JPA에서 <code>Spring Data JPA</code>로 변경
    <details>
    <summary><strong>MemberRepository</strong></summary>

    <a id="1c3eda9b0fe181e2bab9c470e501165c"></a>

    ```java
    public interface MemberRepository extends JpaRepository<Member, Long> {
    		List<Member> findByUsername(String username);
    }
    ```

    </details>

    <details>
    <summary>테스트 </summary>

    <a id="1c3eda9b0fe181478bced6bdb3c88555"></a>

    ```java
    @SpringBootTest
    @Transactional
    class MemberRepositoryTest {

        @Autowired
        EntityManager em;
        @Autowired
        MemberRepository memberRepository;
        
        @Test
        public void basicTest() {
            Member member = new Member("member1", 10);
            memberRepository.save(member);
            
            Member findMember = memberRepository.findById(member.getId()).get();
            assertThat(findMember).isEqualTo(member);
            
            List<Member> result1 = memberRepository.findAll();
            assertThat(result1).containsExactly(member);
            
            List<Member> result2 = memberRepository.findByUsername("member1");
            assertThat(result2).containsExactly(member);
        }
    }
    ```

    </details>

> ✏️ 
> 
> <a id="1c3eda9b0fe1812ba822feeea2c5ae22"></a>
> 
> Sprin Data JPA로 Repository를 설계 시, 내부에서 Querydsl 메서드를 작성할 없다&#46; 
> 
> <a id="1c3eda9b0fe1810e8210d9d181bd501b"></a>
> 
> → 사용자 정의 repository를 만들어 상속처리한다&#46;
