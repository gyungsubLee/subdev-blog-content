---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8103-b16c-ff13884ad0ba
title: 자바 ORM 표준 JPA 프로그래밍 - 기본
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8103-b16c-ff13884ad0ba
    title: 자바 ORM 표준 JPA 프로그래밍 - 기본
excerpt: 🪴 ⌜인프런 - 자바 ORM 표준 JPA 프로그래밍 (기본)⌟ 강의 정리본 JPA는 자바와 객체 지향 패러다임을 가지고 DB(DDL, DML, DCL) 구현하는 하는 도구이다. → ORM, Object Relational Mapping, ‘객체를 연결 해준다.’ Chapter 1. JPA 소개 2. 프로젝트 세팅 및 객
cover: null
icon: d1b6c0a520088550.png
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
created: 2025-03-27T07:47:30.936Z
updated: 2026-04-04T15:00:31.797Z
legacy_path: Main/Spring ( Java )-cd1f71740107/자바 ORM 표준 JPA 프로그래밍 - 기본-ff13884ad0ba/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18103b16cff13884ad0ba
---
> 🪴 <a href="https://www.inflearn.com/course/ORM-JPA-Basic/dashboard">⌜인프런 &#45; 자바 ORM 표준 JPA 프로그래밍 (기본)⌟</a> 강의 정리본 

> JPA는 자바와 객체 지향 패러다임을 가지고 DB(<code>DDL</code>, <code>DML</code>, <code>DCL</code>) 구현하는 하는 도구이다&#46;<br>→ <strong>ORM</strong>, Object Relational Mapping, ‘객체를 연결 해준다&#46;’

<a id="1c3eda9b0fe181358e5fc85b63946f30"></a>

## Chapter

[1. JPA 소개](#/post/1c3eda9b-0fe1-8128-99be-c40565fc0a1d)

[2. 프로젝트 세팅 및  객체, DB 매핑](#/post/1c3eda9b-0fe1-814a-86d2-f5c245826638)

[3. 영속성 관리 - 내부 동작 방식](#/post/1c3eda9b-0fe1-8131-8bde-c788a61cf148)

[4. 엔티티 매핑](#/post/1c3eda9b-0fe1-8189-9f31-fb44df5e5970)

[5. 연관관계 매핑(ORM) 기초](#/post/1c3eda9b-0fe1-8135-bcc1-eea78229c464)

[6. 연관관계 매핑 - 다중성](#/post/1c3eda9b-0fe1-81c0-8042-cd1992dc52fd)

[7. 고급 매핑](#/post/1c3eda9b-0fe1-8166-8e97-e7979e3a9461)

[8. 지연로딩, 영속성 전이, 고아객체](#/post/1c3eda9b-0fe1-8190-a480-c8a2753c4b22)

[9. 값 타입](#/post/1c3eda9b-0fe1-8151-b1a2-ff37ca80fa02)

[10. 객체지향 쿼리 언어1 - 기본 문법](#/post/1c3eda9b-0fe1-8171-9cf5-d21ca6bc4dfc)

[11. 객체지향 쿼리 언어2 - 중급 문법](#/post/1c3eda9b-0fe1-8179-8b30-cfb9505dbacd)

<a id="1c3eda9b0fe18160a4d6e54a37055b54"></a>

## 🤔 추가 정리

[[오류] H2 console 실행안됨](#/post/1c3eda9b-0fe1-8136-b23c-db71c6646fee)

[h2 DB 파일 수동 생성 및 연결 설정](#/post/1c3eda9b-0fe1-812f-a219-ed3e704812fb)

[DDL, DML, DCL](#/post/1c3eda9b-0fe1-81d1-803d-e9d68b415784)

[ANSI SQL,  방언(Dialect)?](#/post/1c3eda9b-0fe1-8109-85b9-f247fdd53003)

<a id="1c3eda9b0fe18140a90eecfff9266888"></a>

### template

<details>
<summary><strong>JapMain</strong></summary>

<a id="1c3eda9b0fe181179beed49089fc5741"></a>

```java
public class JapMain {
    public static void main(String[] args) {
        Persistence persistence = new Persistence();
        EntityManagerFactory emf = persistence.createEntityManagerFactory("hello");
        EntityManager em = emf.createEntityManager();

        EntityTransaction tx = em.getTransaction();
        tx.begin();

        try {

            tx.commit();
        } catch (Exception e){
            tx.rollback();
        } finally {
            em.close();
        }
        emf.close();
    }
}
```

</details>
